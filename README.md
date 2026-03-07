# Adversarial World Agents

**Configurable adversarial simulation where two AI agents (Gemini-powered) fight in a visual environment. All actions recorded as structured multimodal training data.**

Built at the **YC x Google DeepMind Multimodal Frontier Hackathon** — March 7, 2026, San Francisco.

---

## The Hackathon

The **YC x Google DeepMind Multimodal Frontier Hackathon** brought together builders in SF to create projects using Google's latest multimodal AI APIs. Teams had access to cutting-edge models and were judged on creativity, technical execution, and real-world impact.

### Available APIs

| API | Description |
|-----|-------------|
| **Gemini 3.1** | Google's latest multimodal foundation model — vision, reasoning, structured output, function calling |
| **Lyria** | Google DeepMind's music/audio generation model — generates ambient audio from text descriptions |
| **NanoBanana 2** | Image generation model with character consistency — generates visual environments and consistent unit frames |

---

## The Idea

**Adversarial World Agents** is a configurable adversarial simulation platform where two Gemini-powered AI agents engage in combat within a visual physics environment. One agent attacks, one defends. Every decision, action, and outcome is recorded as **structured multimodal training data** — visual frames (NanoBanana 2), audio (Lyria), and reasoning chains (Gemini 3.1).

### The Core Insight

Current world models (Cosmos, Genie, Sora) train on passive video with text captions. They have:
- No structured reasoning data
- No adversarial multi-agent interactions
- No causal chains explaining *why* things happen

We generate **active adversarial decision-making data with causal reasoning chains** across all modalities — visual, audio, and structured text.

### Multimodal Training Data Factory

This isn't just a Gemini project. All 3 APIs are **core** to the output:

| API | Role | Output |
|-----|------|--------|
| **Gemini 3.1** | Drives adversarial agent reasoning | Structured JSON with observation → strategy → risk → action chains |
| **NanoBanana 2** | Renders each game state as a photorealistic frame | Visual training data with character consistency across frames |
| **Lyria** | Generates spatially-aware audio per scene state | Audio training data aligned frame-by-frame |

**Result**: A complete multimodal training dataset — annotated video frames + audio + reasoning chains + game state — all aligned and structured.

### How It Works

```
User configures scenario (text prompt)
        |
        v
Environment generated (NanoBanana 2 for terrain/units, Lyria for ambient audio)
        |
        v
Two Gemini agents spawned (attacker + defender)
        |
        v
Simultaneous action loop (every 1-2 seconds):
  1. Physics engine snapshots state → JSON
  2. Both agents receive state simultaneously
  3. Both return structured actions with reasoning
  4. Actions applied to physics engine
  5. NanoBanana 2 renders frame from game state
  6. Lyria generates audio for scene
  7. Structured logger records everything
        |
        v
Winner announced → Full multimodal dataset exported
```

---

## Architecture Summary

1. **Visual engine** runs at 60fps in the browser (Babylon.js + Havok physics recommended)
2. Every **1-2 seconds**: snapshot game state to JSON, send to both Gemini agents simultaneously
3. Both agents return **structured actions** with full reasoning chains
4. Actions applied to physics engine; loop continues
5. **NanoBanana 2** renders photorealistic frames from game states (character consistency keeps units visually coherent)
6. **Lyria** generates spatially-aware audio per scene
7. **Structured logger** records every turn — the complete multimodal training dataset

---

## Structured Output Format

Every turn produces a structured JSON record capturing the full adversarial interaction:

```json
{
  "turn": 14,
  "timestamp_ms": 23400,
  "game_state": {
    "attacker_units": [
      {"id": "r1", "x": 340, "y": 220, "hp": 72, "status": "advancing"}
    ],
    "defender_units": [
      {"id": "b1", "x": 680, "y": 290, "hp": 85, "status": "intercepting"}
    ],
    "environment": {
      "obstacles": [{"x": 500, "y": 250, "w": 80, "h": 20}],
      "base_position": {"x": 860, "y": 290},
      "base_integrity": 100
    }
  },
  "attacker_reasoning": {
    "observation": "Two defenders are clustered near the base. Gap on the north side.",
    "strategy": "Send flanking unit through northern gap while main force engages defenders.",
    "risk_assessment": "High risk on main force, but flanking unit has 70% chance of reaching base.",
    "selected_action": "split_and_flank"
  },
  "defender_reasoning": {
    "observation": "Attacker formation is splitting. One unit breaking north.",
    "strategy": "Dispatch fastest unit to intercept flanker, maintain defensive line with remaining units.",
    "risk_assessment": "If flanker is not intercepted, base will be reached in ~4 turns.",
    "selected_action": "intercept_and_hold"
  },
  "actions": {
    "attacker": [
      {"unit": "r1", "action": "move", "target": {"x": 380, "y": 160}},
      {"unit": "r2", "action": "attack", "target_unit": "b2"},
      {"unit": "r3", "action": "move", "target": {"x": 420, "y": 300}}
    ],
    "defender": [
      {"unit": "b1", "action": "move", "target": {"x": 500, "y": 170}},
      {"unit": "b2", "action": "defend", "position": {"x": 700, "y": 290}},
      {"unit": "b3", "action": "attack", "target_unit": "r3"}
    ]
  },
  "multimodal_outputs": {
    "frame": "nanobanana_frame_014.png",
    "audio_clip": "lyria_audio_014.wav",
    "frame_description": "Red units splitting formation near northern gap, blue defenders repositioning"
  },
  "outcome": {
    "damage_dealt": {"attacker": 12, "defender": 8},
    "units_lost": {"attacker": 0, "defender": 0},
    "base_damage": 0,
    "territory_change": 0.05
  }
}
```

### Why This Data Matters

This structured output captures something no existing dataset provides:

- **Strategic reasoning with causal chains** — not just "what happened" but "why each agent decided what it did"
- **Adversarial multi-agent interactions** — two intelligent agents reasoning about each other's behavior
- **Multimodal alignment** — visual frames, audio, and structured reasoning all aligned per-turn
- **Counterfactual reasoning** — the risk assessments capture what agents considered but rejected

---

## Validation

### Browser Use Hackathon (1st Place)

The winning team at the **Browser Use hackathon** built the exact same concept: adversarial browser agents with structured output for training data. They won **1st place**. This independently validates the adversarial agent + structured output paradigm.

### Judge Feedback

> **"Even blobs on a cube would be amazing"** — a judge emphasizing that the adversarial agent interaction and structured data output matter more than visual fidelity.

### PhysicsBox Comparison

We also explored **PhysicsBox** (extracting physics from video → modifying → re-rendering). While PhysicsBox uses all 3 APIs more naturally, the demo risk is higher (NanoBanana must convincingly re-render modified physics). Adversarial Agents wins on demo impact with the "multimodal training data factory" framing making all 3 APIs genuinely essential.

---

## Training Data: The Gap We Fill

### Current World Models

| Model | Training Data | What's Missing |
|-------|--------------|----------------|
| **NVIDIA Cosmos** | Raw video pixels + text captions | No structured reasoning |
| **Google Genie** | Gameplay video + action labels | No strategic reasoning chains |
| **OpenAI Sora** | Video + text descriptions | No multi-agent adversarial data |
| **DeepMind Genie 2** | 3D environment trajectories | No causal reasoning annotations |

### What We Generate

- **Active adversarial decision-making data** (not passive observation)
- **Causal reasoning chains** per agent per turn
- **Multi-agent strategic interaction** with structured labels
- **Photorealistic visual frames** with character consistency (NanoBanana 2)
- **Spatially-aware audio** aligned to visual frames (Lyria)
- **Counterfactual analysis** (what was considered, what was rejected, why)

---

## Demos

See the [`demos/`](demos/) folder for **10 interactive visual engine prototypes** exploring different rendering approaches:

### Original Prototypes
- **`matter_demo.html`** — Matter.js 2D physics, arena combat, collision damage
- **`threejs_demo.html`** — Three.js + cannon-es 3D, cinematic camera, shadows
- **`p5_demo.html`** — p5.js bioluminescent deep-sea swarm warfare
- **`canvas_demo.html`** — Pure Canvas 2D, zero dependencies, projectiles, minimap

### Advanced Engine Comparisons
- **`babylon_demo.html`** — Babylon.js 8.0 + Havok physics, PBR materials, particles, post-processing
- **`threejs_advanced_demo.html`** — Advanced Three.js with terrain, water, sky, bloom, instanced units
- **`playcanvas_demo.html`** — PlayCanvas engine with Ammo.js physics, shadows, skybox
- **`webgpu_demo.html`** — WebGPU compute shaders, 5000 particles, GPU-driven N-body simulation
- **`pixi_demo.html`** — PixiJS military C4ISR command center, radar sweep, fog of war, hex grid
- **`isometric_demo.html`** — Pure Canvas isometric strategy game, terrain types, day/night cycle

Open any HTML file in your browser. No build step needed.

### Recommended Stack

Based on research: **Babylon.js 8.0 + Havok Physics + Yuka.js Game AI** — best visual quality, AAA physics, built-in pathfinding, all from CDN in a single HTML file.

---

## Documentation

- [`docs/architecture.md`](docs/architecture.md) — Technical architecture & multimodal pipeline
- [`docs/ideas.md`](docs/ideas.md) — Visual environment options explored (10 engines compared)
- [`docs/scenarios.md`](docs/scenarios.md) — Example configurable scenarios
- [`docs/research.md`](docs/research.md) — Research findings, validation, and multimodal strategy

---

## Team

- **Ayush Kumar** — [@ayushkumarcode](https://github.com/ayushkumarcode)
- **Harsh Savergaonkar** — [@harshsaver](https://github.com/harshsaver)

### Harsh's Existing Canvases
- [Polytopia Clone](https://polytopia-seven.vercel.app) — Three.js isometric hex terrain strategy game ([repo](https://github.com/harshsaver/polytopia))
- [IsoCity](https://isometric-city-swart.vercel.app) — Next.js isometric city builder with simulation ([repo](https://github.com/harshsaver/isometric-city))

---

## License

MIT
