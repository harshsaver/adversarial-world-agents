# Visual Environment Options Explored

During ideation, we explored many different visual environment approaches for the adversarial simulation. We built **10 interactive demos** across different engines to compare visual quality, performance, and AI-hookability side by side.

---

## Engine Comparison Matrix

| Engine | File | Size | Visual Quality | AI Hookability | Physics | Performance |
|--------|------|------|---------------|----------------|---------|-------------|
| **Babylon.js + Havok** | `babylon_demo.html` | 44KB | Excellent | Excellent | AAA (Havok WASM) | 60fps, 1000+ units |
| **Three.js Advanced** | `threejs_advanced_demo.html` | 62KB | Excellent | Good | cannon-es | 60fps |
| **PlayCanvas** | `playcanvas_demo.html` | 48KB | Very Good | Good | Ammo.js | 60fps |
| **WebGPU Compute** | `webgpu_demo.html` | 35KB | Stunning | Poor (no game structure) | GPU compute | 60fps, 5000 particles |
| **PixiJS Tactical** | `pixi_demo.html` | 29KB | Very Good (2D) | Good | None (manual) | 60fps |
| **Isometric Canvas** | `isometric_demo.html` | 42KB | Good | Good | None (manual) | 60fps |
| **Three.js Basic** | `threejs_demo.html` | 26KB | Good | Good | cannon-es | 60fps |
| **p5.js Swarm** | `p5_demo.html` | 25KB | Beautiful | Medium | Steering only | 60fps |
| **Matter.js** | `matter_demo.html` | 23KB | Medium | Easy | Matter.js 2D | 60fps |
| **Pure Canvas** | `canvas_demo.html` | 24KB | Medium | Easy | None (manual) | 60fps |

---

## Recommended: Babylon.js 8.0 + Havok + Yuka.js

Based on extensive research, **Babylon.js 8.0** is the best choice for the hackathon:

- **Havok Physics** — Same engine behind Halo, Half-Life 2, Skyrim. Runs as WASM.
- **1000+ animated soldiers at 144fps** via instanced meshes
- **Built-in Recast pathfinding** with crowd navigation
- **PBR materials, area lights, WebGPU native shaders**
- **All from CDN** — single HTML file, zero build step
- **Built-in GUI system** for HUD overlays

Add **Yuka.js** for game AI:
- Steering behaviors: pursuit, evade, flee, arrive, wander, formation control
- State machines and behavior trees
- Engine-agnostic — plug in Gemini at the decision layer

---

## Detailed Engine Assessments

### 1. Babylon.js + Havok (RECOMMENDED)

**File:** `demos/babylon_demo.html` (44KB)

Features built:
- PBR materials with metallic/roughness
- Havok physics for projectile ballistics and collision
- Particle systems for explosions, trails, death effects
- Post-processing: bloom, tone mapping, vignette
- Dynamic lighting with shadow casting
- Cinematic auto-orbit camera
- HUD with team scores and battle timer
- 8v8 unit combat with AI behaviors

**Why it wins:** Most complete out-of-the-box. Havok physics, Recast pathfinding, GUI system, area lights — all built in. The API surface for hooking AI agents is clean.

### 2. Advanced Three.js

**File:** `demos/threejs_advanced_demo.html` (62KB, largest demo)

Features built:
- Procedural terrain with vertex displacement (perlin noise)
- Reflective water plane with custom shader
- Procedural sky with sun position
- GPU instanced meshes (InstancedMesh) for 10v10 teams
- Projectile system with gravity arcs and trail particles
- Post-processing: UnrealBloomPass, SMAAPass, vignette
- Exponential fog atmosphere
- Dynamic point lights on explosions
- Cinematic camera with vertical bob
- HUD with kill feed and minimap

**Why it's strong:** Most flexible, largest ecosystem, best documentation. But requires more manual assembly than Babylon.js.

### 3. PlayCanvas

**File:** `demos/playcanvas_demo.html` (48KB)

Features built:
- Built-in Ammo.js physics
- 6v6 unit combat
- Particle trails and bloom
- Skybox and shadows
- Clean entity-component architecture

**Why it's worth considering:** Console-quality visuals. Powers commercial browser games (Robostorm, Mini Royale). But less documentation than Babylon.js/Three.js.

### 4. WebGPU Compute Shaders

**File:** `demos/webgpu_demo.html` (35KB)

Features built:
- Pure WebGPU with WGSL shaders (no libraries)
- GPU compute for 5000 particles with full N-body interactions
- Flocking behaviors: separation, alignment, cohesion
- Combat system resolved entirely on GPU
- Additive blending for nebula/glow effects
- Ping-pong texture trail system
- Instanced rendering (30,000 vertices/frame)

**Why it's stunning:** Visually the most impressive — 5000 glowing particles fighting with trails and glow. But no game structure (no units, health, strategy). Best as a visual layer, not a game engine.

### 5. PixiJS Military Tactical Display

**File:** `demos/pixi_demo.html` (29KB)

Features built:
- Military C4ISR command center aesthetic
- Radar sweep effect with fading trail
- Hex grid overlay
- Fog of war with radial gradient cutouts
- 12v12 units with military NATO-style icons
- Targeting lines, threat circles, engagement effects
- Scanline CRT overlay
- Status panels, combat log, sector control display
- Minimap with real-time unit tracking

**Why it's unique:** Completely different aesthetic — looks like a NORAD war room display. Would make a striking demo for judges. Good for the "strategic command" angle.

### 6. Isometric Canvas Strategy

**File:** `demos/isometric_demo.html` (42KB)

Features built:
- Pure Canvas 2D, zero dependencies
- 20x20 isometric tile map
- Multiple terrain types: grass, water, mountains, forest, desert
- Buildings: barracks, towers, walls, HQ
- Unit types: infantry, cavalry, archers
- Day/night cycle
- Fog of war, minimap, battle log
- Camera scrolling and zoom

**Why it's relevant:** Closest to the Polytopia/Civilization aesthetic. Harsh's existing canvases (Polytopia clone, IsoCity) could be adapted to this style.

---

## Harsh's Existing Canvases

### Polytopia Clone
- **Repo:** [github.com/harshsaver/polytopia](https://github.com/harshsaver/polytopia)
- **Deployed:** [polytopia-seven.vercel.app](https://polytopia-seven.vercel.app)
- **Tech:** Pure JS + Three.js, isometric hex terrain, 3 unit types, 16x16 grid
- **Status:** Would need refactoring to add programmatic API (currently click-driven)

### IsoCity
- **Repo:** [github.com/harshsaver/isometric-city](https://github.com/harshsaver/isometric-city)
- **Deployed:** [isometric-city-swart.vercel.app](https://isometric-city-swart.vercel.app)
- **Tech:** Next.js + TypeScript, ~90 building types, full simulation
- **Status:** Has clean programmatic API via `setTool()` + `placeAtTile(x, y)`. Good candidate for "one builds, one destroys" scenario.

---

## Other Engines Considered but Not Built

### Minecraft via Mineflayer
- Judges approved this approach but setup complexity is too high for a hackathon
- Rich 3D environment but hard to snapshot state cleanly

### Turn-based (Polytopia-style)
- **Rejected** — real life is simultaneous, not turn-based. The whole point is both agents act at the same time.

---

## Relevant Open-Source Projects

| Project | Description | Relevance |
|---------|-------------|-----------|
| [WarAgent](https://github.com/agiresearch/WarAgent) | LLM-based multi-agent war simulation | Exact same concept, Apache 2.0 |
| [wargame-agents](https://www.seangoedecke.com/wargame-agents/) | RTS with text orders to AI generals | Directly relevant to LLM agent concept |
| [Kiomet](https://github.com/SoftbearStudios/kiomet) | Rust+WASM hex-grid multiplayer RTS | Polished visual reference |
| [Freeciv-web](https://github.com/freeciv/freeciv-web) | Full Civilization game in Three.js+WebGL | AI opponent reference |
| [Yuka.js](https://github.com/Mugen87/yuka) | Game AI: steering, state machines, pursuit/evade | Agent behavior layer |
| [AgentScript](https://agentscript.org/) | NetLogo-like ABM with Three.js 3D viz | Agent-based modeling reference |
