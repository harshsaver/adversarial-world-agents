# Technical Architecture

## System Overview

```
+-------------------+       +-------------------+
|                   |       |                   |
|   NanoBanana 2    |       |      Lyria        |
|  (terrain gen)    |       |   (audio gen)     |
|                   |       |                   |
+--------+----------+       +--------+----------+
         |                           |
         v                           v
+------------------------------------------------+
|                                                |
|           Visual Environment                   |
|        (Physics Engine @ 60fps)                |
|                                                |
|   - HTML Canvas / Three.js / p5.js / Matter.js |
|   - Obstacles, terrain, units, projectiles     |
|   - Real-time physics simulation               |
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
|   - Resolves conflicts                         |
|                                                |
+-----+------------------------------------------+
      |
      v
+------------------------------------------------+
|                                                |
|         Structured Logger                      |
|   - Records game_state per turn                |
|   - Records agent reasoning                    |
|   - Records actions + outcomes                 |
|   - Exports labeled training data              |
|                                                |
+------------------------------------------------+
```

## Core Loop

### 1. Physics Engine (60fps)

The physics engine runs continuously in the browser at 60 frames per second. It handles:

- Unit movement and velocity
- Collision detection (unit-unit, unit-obstacle, unit-boundary)
- Projectile physics (if applicable)
- Damage calculation
- Death/removal of units
- Visual rendering

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

### 5. Structured Logging

Every turn is logged with full context:

- Complete game state before actions
- Both agents' reasoning chains
- Both agents' selected actions
- Outcome after actions are applied
- Damage dealt, units lost, territory changed

This log is the primary output -- the structured training data.

## Environment Generation

### NanoBanana 2 (Terrain)

When a user configures a new scenario, NanoBanana 2 generates:

- Background textures appropriate to the scenario (urban, naval, forest, etc.)
- Obstacle placement suggestions
- Visual theming (color palettes, atmospheric effects)

### Lyria (Audio)

Lyria generates ambient audio per scenario:

- Urban warfare: distant gunfire, sirens, radio chatter
- Naval battle: waves, wind, ship engines
- Cyber attack: electronic hums, data transfer sounds, alarm tones
- Forest: wildlife, rustling, stream sounds

The audio runs continuously during simulation and adapts to combat intensity.

## Data Pipeline

```
Simulation Run
      |
      v
Turn-by-turn JSON logs
      |
      v
Post-processing
  - Validate all fields
  - Calculate derived metrics
  - Add outcome attribution
      |
      v
Training dataset (JSONL)
  - One line per turn
  - Full reasoning + actions + outcomes
  - Ready for fine-tuning or RLHF
```

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Physics Engine | Matter.js / Three.js + cannon-es / p5.js / Pure Canvas |
| AI Agents | Gemini 3.1 (structured output mode) |
| Terrain Generation | NanoBanana 2 |
| Audio Generation | Lyria |
| Frontend | Vanilla HTML/JS (no framework) |
| Data Export | JSON/JSONL |
