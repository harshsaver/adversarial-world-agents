# Technical Architecture

## System Overview

```
+-------------------+       +-------------------+
|                   |       |                   |
|   NanoBanana 2    |       |      Lyria        |
| (frame rendering) |       |   (audio gen)     |
|                   |       |                   |
+--------+----------+       +--------+----------+
         |                           |
         v                           v
+------------------------------------------------+
|                                                |
|           Visual Environment                   |
|     (Babylon.js + Havok Physics @ 60fps)       |
|                                                |
|   - PBR materials, shadows, particles          |
|   - Havok physics (AAA-quality WASM)           |
|   - Recast crowd navigation/pathfinding        |
|   - Instanced meshes (1000+ units at 144fps)   |
|                                                |
+-----+-------------------+---------------------+
      |                   |
      | State snapshot    | State snapshot
      | (every 1-2 sec)   | (every 1-2 sec)
      |                   |
      v                   v
+------------+    +-------------+
|            |    |             |
| Gemini 3.1 |    | Gemini 3.1  |
| (Attacker) |    | (Defender)  |
|            |    |             |
+-----+------+    +------+------+
      |                  |
      | Actions JSON     | Actions JSON
      |                  |
      v                  v
+------------------------------------------------+
|                                                |
|          Action Resolver                       |
|   - Validates actions                          |
|   - Applies to physics engine                  |
|   - Resolves conflicts simultaneously          |
|                                                |
+-----+------------------------------------------+
      |
      v
+------------------------------------------------+
|                                                |
|    Multimodal Training Data Pipeline           |
|                                                |
|   1. Structured Logger                         |
|      - game_state per turn (JSON)              |
|      - agent reasoning chains                  |
|      - actions + outcomes                      |
|                                                |
|   2. NanoBanana 2 Frame Renderer               |
|      - Renders game state as photorealistic    |
|        frame with character consistency         |
|      - Creates visual training data            |
|                                                |
|   3. Lyria Audio Generator                     |
|      - Generates spatially-aware audio         |
|      - Creates audio training data             |
|                                                |
|   OUTPUT: Aligned multimodal dataset           |
|   (visual + audio + structured reasoning)      |
|                                                |
+------------------------------------------------+
```

## Core Loop

### 1. Visual Engine (60fps)

The visual engine runs continuously in the browser at 60fps. Recommended stack: **Babylon.js 8.0 + Havok Physics**.

It handles:
- Unit movement and velocity
- Collision detection (unit-unit, unit-obstacle, unit-boundary)
- Projectile physics with gravity arcs
- Damage calculation
- Death/removal of units
- Visual rendering with PBR materials, shadows, particles, post-processing

The physics engine is the source of truth for all world state. It runs independently of the AI agents.

### 2. State Snapshot (every 1-2 seconds)

Every 1-2 seconds, the system captures a JSON snapshot of the current game state:

```json
{
  "turn": 14,
  "timestamp_ms": 23400,
  "attacker_units": [...],
  "defender_units": [...],
  "obstacles": [...],
  "base_position": {...},
  "base_integrity": 100,
  "score": {...}
}
```

This snapshot is sent simultaneously to both Gemini agents.

### 3. Gemini Agent Processing (simultaneous)

Both agents receive the same state snapshot at the same time. Each agent:

1. **Observes** the current state (positions, HP, obstacles)
2. **Reasons** about the situation (what is the opponent likely doing?)
3. **Plans** a strategy (what should I do given my objective?)
4. **Selects actions** for each unit under its control
5. **Returns** a structured JSON response with reasoning + actions

The agents use Gemini 3.1's structured output mode to guarantee valid JSON responses.

### 4. Action Resolution

Both agents' actions are resolved simultaneously:

- Move actions: update unit target positions
- Attack actions: initiate combat between specified units
- Defend actions: units take defensive stance (reduced damage, reduced mobility)
- Retreat actions: units move away from threats
- Special actions: scenario-specific (e.g., build, repair, hack)

Conflicts are resolved deterministically (e.g., if both agents try to move a unit to the same position, physics handles the collision).

### 5. Multimodal Data Generation

After each turn, the multimodal pipeline generates aligned training data:

**Structured Data (Gemini 3.1)**:
- Complete game state before/after actions
- Both agents' full reasoning chains
- Actions selected + actions rejected (counterfactuals)
- Outcome measurements

**Visual Data (NanoBanana 2)**:
- Game state rendered as photorealistic frame
- Character consistency maintained across frames (NanoBanana 2's key feature)
- Creates the video component of training data

**Audio Data (Lyria)**:
- Scene-appropriate audio generated per frame
- Spatially aware (explosions, movement, ambient)
- Creates the audio component of training data

## Environment Generation

### NanoBanana 2 (Visuals)

Two roles:

1. **Scenario Setup**: When a user configures a new scenario, NanoBanana 2 generates terrain textures, unit appearances, obstacle art, and atmospheric effects matching the scenario description.

2. **Frame Rendering**: During simulation, NanoBanana 2 renders each game state as a photorealistic frame. Character consistency ensures units look the same across frames, creating coherent visual training data.

### Lyria (Audio)

Two roles:

1. **Ambient Audio**: Generates continuous background audio matching the scenario (urban warfare sounds, naval waves, cyber hums, forest wildlife).

2. **Event Audio**: Generates audio for specific events (explosions, impacts, movement) aligned to the visual frames. This creates paired visual-audio training data.

## Recommended Tech Stack

| Component | Technology | Why |
|-----------|-----------|-----|
| Visual Engine | Babylon.js 8.0 | PBR, area lights, WebGPU native, 1000+ units at 144fps |
| Physics | Havok (via Babylon.js) | AAA quality (Halo, Skyrim), WASM |
| Pathfinding | Recast (via Babylon.js) | Built-in crowd navigation |
| Game AI | Yuka.js | Steering behaviors, state machines, pursuit/evade/flee |
| Agent Reasoning | Gemini 3.1 | Structured output, multimodal vision, long context |
| Visual Generation | NanoBanana 2 | Character consistency, scenario art |
| Audio Generation | Lyria | Scene-appropriate audio |
| Frontend | Single HTML file from CDN | Zero build step |
| Data Export | JSON/JSONL | One line per turn, full multimodal record |

### CDN URLs (no build step)

```html
<!-- Babylon.js -->
<script src="https://cdn.babylonjs.com/babylon.js"></script>
<script src="https://cdn.babylonjs.com/havok/HavokPhysics_umd.js"></script>
<script src="https://cdn.babylonjs.com/babylon.gui.min.js"></script>

<!-- Yuka.js Game AI -->
<script type="module">
import * as YUKA from 'https://cdn.jsdelivr.net/npm/yuka/build/yuka.module.js';
</script>
```

## Data Pipeline

```
Simulation Run
      |
      v
Per-turn multimodal capture:
  - Structured JSON (game state + reasoning)
  - NanoBanana 2 frame (photorealistic render)
  - Lyria audio clip (scene audio)
      |
      v
Post-processing:
  - Validate all fields
  - Align frames + audio + reasoning by timestamp
  - Calculate derived metrics
  - Add outcome attribution
      |
      v
Multimodal training dataset (JSONL + frames + audio)
  - One line per turn
  - Linked visual frames and audio clips
  - Full reasoning + actions + outcomes
  - Ready for world model training, fine-tuning, or RLHF
```

## Alternative Visual Engines Evaluated

See [`ideas.md`](ideas.md) for the full comparison of 10 visual engines tested:
Babylon.js, Three.js (basic + advanced), PlayCanvas, WebGPU, PixiJS, Matter.js, p5.js, Canvas, and Isometric Canvas.
