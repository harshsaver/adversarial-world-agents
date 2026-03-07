# Adversarial World Agents

**Configurable adversarial simulation where two AI agents (Gemini-powered) fight in a visual environment. All actions recorded as structured training data.**

Built at the **YC x Google DeepMind Multimodal Frontier Hackathon** -- March 7, 2026, San Francisco.

---

## The Hackathon

The **YC x Google DeepMind Multimodal Frontier Hackathon** brought together builders in SF to create projects using Google's latest multimodal AI APIs. Teams had access to cutting-edge models and were judged on creativity, technical execution, and real-world impact.

### Available APIs

| API | Description |
|-----|-------------|
| **Gemini 3.1** | Google's latest multimodal foundation model -- vision, reasoning, structured output, function calling |
| **Lyria** | Google DeepMind's music generation model -- generates ambient audio from text descriptions |
| **NanoBanana 2** | Image/terrain generation model -- generates visual environments from scenario descriptions |

---

## The Idea

**Adversarial World Agents** is a configurable adversarial simulation platform where two Gemini-powered AI agents engage in combat within a visual physics environment. One agent attacks, one defends. Every decision, action, and outcome is recorded as structured training data with full reasoning annotations.

The core insight: **current world models (Cosmos, Genie, Sora) train on passive video with text captions. They have no structured reasoning data. We generate active adversarial decision-making data with causal reasoning chains.**

### How It Works

```
User configures scenario
        |
        v
Environment generated (NanoBanana 2 for terrain, Lyria for ambient audio)
        |
        v
Two Gemini agents spawned (attacker + defender)
        |
        v
Simultaneous action loop:
  - Physics engine snapshots state -> JSON
  - Both agents receive state simultaneously
  - Both agents return actions with reasoning
  - Actions applied to physics engine
  - Structured logger records everything
        |
        v
Winner announced
        |
        v
Structured output with reasoning annotations exported
```

### Architecture Summary

1. **Physics engine** runs at 60fps in the browser
2. Every **1-2 seconds**: snapshot game state to JSON, send to both Gemini agents simultaneously
3. Both agents return **structured actions** (move, attack, defend, retreat, etc.)
4. Actions applied to physics engine; loop continues
5. **Structured logger** records every turn with full reasoning chains
6. **NanoBanana 2** generates terrain textures per scenario
7. **Lyria** generates ambient audio per scenario

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
  "outcome": {
    "damage_dealt": {"attacker": 12, "defender": 8},
    "units_lost": {"attacker": 0, "defender": 0},
    "base_damage": 0,
    "territory_change": 0.05
  }
}
```

### Why This Data Matters

This structured output format captures something no existing dataset provides:

- **Strategic reasoning with causal chains** -- not just "what happened" but "why each agent decided what it did"
- **Adversarial multi-agent interactions** -- two intelligent agents reasoning about each other's behavior
- **Labeled training data** -- every field is structured and machine-readable, not raw pixels or free-text captions
- **Counterfactual reasoning** -- the risk assessments capture what agents considered but rejected

---

## Validation: Browser Use Hackathon

The winning team at the **Browser Use hackathon** built the exact same concept: adversarial browser agents with structured output for training data. They won **1st place**.

Their approach:
- Two AI agents in an adversarial setup
- Structured output capturing reasoning and actions
- Training data generation as the primary value proposition

This independently validates the core idea. The adversarial agent + structured output paradigm is what judges and the market want.

---

## Judge Feedback

The hackathon judges were enthusiastic about this concept. Key feedback:

> **"Even blobs on a cube would be amazing"** -- a judge emphasizing that the visual fidelity matters less than the adversarial agent interaction and structured data output.

The judges recognized that the training data angle is the real breakthrough -- generating labeled adversarial reasoning data that current world models completely lack.

---

## Training Data Angle

### The Problem with Current World Models

Every major world model trains on the same limited data:

| Model | Training Data | What's Missing |
|-------|--------------|----------------|
| **NVIDIA Cosmos** | Raw video pixels + text captions | No structured reasoning |
| **Google Genie** | Gameplay video + action labels | No strategic reasoning chains |
| **OpenAI Sora** | Video + text descriptions | No multi-agent adversarial data |
| **DeepMind Genie 2** | 3D environment trajectories | No causal reasoning annotations |

### What Adversarial World Agents Generates

- **Active adversarial decision-making data** (not passive observation)
- **Causal reasoning chains** per agent per turn
- **Multi-agent strategic interaction** with structured labels
- **Counterfactual analysis** (what was considered, what was rejected, why)
- **Outcome attribution** (which decisions led to which results)

This is the data that world models need to go from "predicting what the next frame looks like" to "understanding why agents do what they do."

---

## Demos

See the [`demos/`](demos/) folder for four interactive physics engine prototypes:

- **Matter.js 2D Physics** -- Arena with walls, obstacles, glowing units, collision damage
- **Three.js + cannon-es 3D** -- Cinematic 3D arena with spheres, shadows, fog
- **p5.js Bioluminescent Swarm** -- Deep-sea style, steering behaviors, trails
- **Pure Canvas 2D** -- Zero dependencies, projectiles, minimap, HP bars, 60fps

Open any HTML file in your browser. No build step needed.

---

## Documentation

- [`docs/architecture.md`](docs/architecture.md) -- Technical architecture
- [`docs/ideas.md`](docs/ideas.md) -- Visual environment options explored
- [`docs/scenarios.md`](docs/scenarios.md) -- Example configurable scenarios
- [`docs/research.md`](docs/research.md) -- Research findings and validation

---

## License

MIT
