# Research Findings

Key research findings that inform and validate the Adversarial World Agents approach.

---

## 1. Browser Use Hackathon Validation

The winning team at the **Browser Use hackathon** independently built the exact same concept:

- **Adversarial browser agents** — two AI agents operating in opposition
- **Structured output** — all agent reasoning and actions captured in machine-readable format
- **Training data generation** — the primary value proposition was generating labeled data from adversarial interactions

They won **1st place**.

| Aspect | Browser Use Winner | Our Project |
|--------|-------------------|-------------|
| Agent count | 2 (adversarial) | 2 (adversarial) |
| Output format | Structured JSON | Structured JSON + visual frames + audio |
| Primary value | Training data | Multimodal training data |
| Environment | Browser | Physics simulation |
| Multimodal | No | Yes (Gemini + NanoBanana + Lyria) |

---

## 2. The Structured Reasoning Gap in World Models

### Current State

Every major world model trains on passive observation data:

**NVIDIA Cosmos** — Raw video pixels + text captions. Learns visual dynamics but not *why* things happen.

**Google Genie / Genie 2** — Gameplay video + sparse action labels. Learns action-consequence mapping but not multi-agent strategic reasoning.

**OpenAI Sora** — Video + text descriptions. Learns visual generation but no structured reasoning about agent behavior.

**DeepMind Genie 2** — 3D environment trajectories. Learns consistent 3D world generation but no multi-agent reasoning or causal explanation.

### The Gap

All these models share a fundamental limitation: **they train on what happened, not why it happened.**

- They see pixels changing over time
- They may see action labels (up, down, jump)
- They never see reasoning chains behind decisions
- They never see adversarial strategic thinking
- They never see counterfactual analysis ("I considered X but rejected it because Y")

### Verification

We verified through deep research:
- **SVG2** (Feb 2026) does scene graph extraction from video, but nobody connects it to world model training
- **No system exists** that feeds structured reasoning data into world model training pipelines
- The video decomposition → structured data community and world model training community are **completely disconnected**
- Every researcher we found trains on raw pixels + text captions

### What We Generate

Our structured output fills this gap:

```
Observation → Strategy → Risk Assessment → Action Selection → Outcome
```

For BOTH agents, simultaneously, every turn. Plus aligned visual frames and audio.

---

## 3. Multimodal Strategy: Why All 3 APIs Are Essential

### The Problem

At a **multimodal** hackathon, judges notice which teams use all APIs in a **core** way vs. bolted-on decoration.

For Adversarial Agents, only Gemini is naturally core. NanoBanana and Lyria risk being decorative.

### The Solution: Multimodal Training Data Factory

The framing that makes all 3 APIs genuinely essential:

| API | Role | Why It's Core |
|-----|------|---------------|
| **Gemini 3.1** | Drives adversarial reasoning | Produces structured game state + reasoning chains — the TEXT component of training data |
| **NanoBanana 2** | Renders game states as frames | Creates the VISUAL component of training data. Character consistency keeps units coherent across frames. |
| **Lyria** | Generates scene audio | Creates the AUDIO component of training data. Spatially-aware, aligned per frame. |

**Output**: Not just structured JSON, but a complete multimodal training dataset — annotated video frames + audio + reasoning chains + game state. Every modality aligned frame-by-frame.

This makes NanoBanana core (generating visual training data) and Lyria core (generating audio training data). The pitch: *"We generate complete multimodal world model training data — visual, audio, and structured — all annotated and aligned."*

### Comparison: PhysicsBox Alternative

We also explored **PhysicsBox** (git-for-video): upload a video → Gemini extracts physics → modify physics → NanoBanana re-renders frames → Lyria re-renders audio.

| | PhysicsBox | Adversarial Agents |
|---|---|---|
| **Gemini** | Extract physics (core) | Drive reasoning (core) |
| **NanoBanana** | Re-render frames (core) | Render training frames (core with factory framing) |
| **Lyria** | Re-render audio (core) | Generate training audio (core with factory framing) |
| **All 3 essential?** | Yes naturally | Yes with training data factory framing |
| **Demo risk** | HIGH — can NanoBanana re-render convincing physics? | LOW — live agents fighting is visceral |
| **Derivative?** | No | Somewhat (Browser Brawl did adversarial agents) |
| **Pitch** | "Common Crawl for world models" | "Multimodal training data for world models" |
| **Judge quote** | None | "Even blobs on a cube would be amazing" |

---

## 4. Active vs Passive Data

### Passive Data (What Exists)
- Video recordings of gameplay
- Text descriptions of what happened
- Action logs (button presses, mouse movements)
- Reward signals (score, win/loss)

Like learning to drive by watching dashcam footage.

### Active Data (What We Generate)
- Real-time strategic decisions with full reasoning
- Adversarial planning (reasoning about opponent behavior)
- Risk assessment and uncertainty handling
- Simultaneous multi-agent decision-making
- Causal chains from observation to action to outcome
- Aligned visual frames and audio

Like learning to drive with an instructor explaining every decision.

---

## 5. Why Adversarial Specifically

Adversarial interactions require:

1. **Theory of Mind** — reasoning about what the opponent is thinking
2. **Adaptive Strategy** — changing plans based on opponent behavior
3. **Deception** — considering whether to feint, bluff, or misdirect
4. **Resource Management** — allocating limited resources under threat
5. **Risk/Reward Tradeoff** — every aggressive action creates a vulnerability

These are precisely the capabilities that current AI systems struggle with.

---

## 6. Data Scale Potential

Each simulation run generates ~30-60 turns of fully annotated multimodal data:

| Timeframe | Simulations | Turns | Reasoning Chains | Visual Frames | Audio Clips |
|-----------|-------------|-------|-----------------|---------------|-------------|
| 1 hour | 60 | ~2,700 | ~5,400 | ~2,700 | ~2,700 |
| 1 day | 1,440 | ~64,800 | ~129,600 | ~64,800 | ~64,800 |
| 1 week | 10,080 | ~453,600 | ~907,200 | ~453,600 | ~453,600 |

---

## 7. Related Work

- **Cicero (Meta)** — Diplomacy AI with negotiation. Similar adversarial reasoning but text-only, no visual data.
- **AlphaStar (DeepMind)** — StarCraft II. Self-play but reasoning not structured/exportable.
- **OpenAI Five** — Dota 2. Same limitation as AlphaStar.
- **Voyager (NVIDIA)** — Minecraft LLM agent. Single agent, not adversarial.
- **SPRING (CMU)** — LLM reasoning framework. Single-agent.
- **WarAgent** — LLM multi-agent war simulation. Closest to our concept but no visual/audio data generation.
- **SIM-1 (Fable Studio)** — Multi-agent competition with GPT-4o. Uses Unreal Engine, not browser-native.

Our contribution: **structured adversarial reasoning data from multi-agent visual simulations, with aligned multimodal outputs (visual + audio + structured text)**, which none of the above produce.

---

## 8. Browser Engine Research

### Key Finding

The browser 3D ecosystem underwent a step-change in late 2025 when WebGPU shipped across all major browsers. AAA-quality physics and rendering now runs in a single HTML file from CDN.

### Recommendation: Babylon.js 8.0

- Area lights for cinematic lighting
- WebGPU native shaders (2x smaller bundle)
- Havok Physics running as WASM (same as Halo, Skyrim)
- 1000+ animated soldiers at 144fps via instanced meshes
- Built-in Recast crowd navigation for pathfinding
- Built-in GUI system

See [`ideas.md`](ideas.md) for the full 10-engine comparison and [`browser_game_engine_research.md`](../browser_game_engine_research.md) for the detailed research report.
