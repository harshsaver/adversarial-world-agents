# Browser-Based Game Engines, Physics Simulations & 3D Frameworks
## For Real-Time Adversarial Agent Simulation - Deep Research Report
**Date: 2026-03-07**

---

## Executive Summary

Your current demos (basic Matter.js, basic Three.js, p5.js) are leaving significant visual quality on the table. The browser 3D ecosystem has matured dramatically -- Babylon.js 8.0 with Havok physics, WebGPU support across all major browsers (Chrome, Firefox, Safari, Edge as of November 2025), and production-quality physics via Rapier WASM mean you can now achieve near-desktop-quality visuals in a browser tab. For a hackathon demo to DeepMind researchers, the highest-impact path is **Babylon.js + Havok physics + Yuka.js game AI + crowd navigation**, which gives you terrain, 1000+ animated units, pathfinding, steering behaviors, and AAA-quality lighting in a single HTML file loaded from CDN. Setup time: under 2 hours.

The second-best option is **Three.js + Rapier WASM + Yuka.js**, which gives you more flexibility but requires more manual scene setup. For a polished 2D approach, **Phaser 3** or **PixiJS v8** with WebGPU can deliver impressive particle effects and unit control.

There are also existing open-source browser RTS games (Freeciv-web, Kiomet) and AI wargame frameworks (WarAgent, SIM-1, GenWar) that could be forked or used as references.

---

## 1. What Looks Visually Impressive in a Browser RIGHT NOW

### Babylon.js (RECOMMENDED - Best Overall)

**Visual Quality: AAA-tier for browser**

Babylon.js 8.0 (released March 2025) represents the current state of the art for browser 3D:

- **Area Lights**: 2D shapes that emit diffuse light, creating movie-set-quality lighting without complex setup
- **Node Render Graph**: Full visual control over the rendering pipeline -- customize every step of the render process
- **WebGPU native**: All core shaders available in both GLSL and WGSL, no conversion layer, 2x smaller bundle when targeting WebGPU
- **Snapshot Rendering**: Records draw calls during one frame and replays them, up to **10x performance increase** for mostly-static scenes
- **Havok Physics**: AAA game physics engine (the same Havok used in Halo, Half-Life 2, Skyrim) running as WASM in the browser

**Key Demos That Look Incredible:**
- **Ocean Demo** (Popov72): FFT-based ocean simulation with WebGPU compute shaders -- https://popov72.github.io/OceanDemo/dist/
- **Area Lights Demo**: Movie-quality diffuse lighting -- available at babylonjs.com/featureDemos/
- **1000+ Animated Soldiers**: Instanced meshes with bone animations running at 144fps
- **WebGPU Compute Shader Demo**: Real-time particle physics
- **Sponza Scene**: Deferred rendering, 400+ dynamic lights, real-time reflections, complex shadows at ~50fps on MacBook Pro M1

**CDN Setup (single HTML file):**
```html
<script src="https://cdn.babylonjs.com/babylon.js"></script>
<script src="https://cdn.babylonjs.com/havok/HavokPhysics_umd.js"></script>
<script src="https://cdn.babylonjs.com/babylon.loaders.min.js"></script>
```

**Sources:**
- https://blogs.windows.com/windowsdeveloper/2025/03/27/announcing-babylon-js-8-0/
- https://babylonjs.medium.com/introducing-babylon-js-8-0-77644b31e2f9
- https://github.com/Popov72/OceanDemo
- https://babylonjs.medium.com/creating-thousands-of-animated-entities-in-babylon-js-ce3c439bdacf

### Three.js (Strong Alternative)

**Visual Quality: Excellent, but requires more manual work**

Three.js remains the most popular WebGL library with the largest ecosystem. State-of-the-art demos include:

- **WebGPU Compute Particles**: 500,000 particles with physics -- https://threejs.org/examples/webgpu_compute_particles.html
- **GPGPU Flocking (Boids)**: GPU-accelerated bird flocking simulation -- https://threejs.org/examples/webgl_gpgpu_birds.html
- **WebGPU Attractor Particles**: Mesmerizing particle attractors -- https://threejs.org/examples/webgpu_tsl_compute_attractors_particles.html
- **Galaxy Simulation**: 1 million particles with compute shaders
- **Shattering Image Gallery**: Physics-based 3D particle explosions
- **Glass Refraction Effects**: Light refraction and chromatic aberration

**Key Advantage**: Largest community, most examples, most third-party libraries
**Key Disadvantage**: Not a game engine -- you assemble components yourself

**Sources:**
- https://threejs.org/examples/
- https://tympanus.net/codrops/hub/tag/three-js/
- https://threejsroadmap.com/blog/galaxy-simulation-webgpu-compute-shaders

### PlayCanvas (Best for Collaborative Development)

**Visual Quality: Console-quality, fastest load times**

PlayCanvas powers commercial browser games with impressive visuals:

- **Robostorm**: Multiplayer robot battle with amazing particle effects
- **Mini Royale: Nations**: Browser-based FPS that looks like a full game
- **Aritelia**: Procedurally generated MMO with day/night cycles, real-time lighting
- **After the Flood**: Mozilla's WebGL 2 graphical showcase

**Standalone CDN Usage:**
```html
<script type="importmap">
{
  "imports": {
    "playcanvas": "https://cdn.jsdelivr.net/npm/playcanvas/+esm"
  }
}
</script>
```

**Key Advantage**: Zero compile time, integrated physics, real-time collaboration editor
**Key Disadvantage**: Smaller community than Three.js/Babylon.js

**Sources:**
- https://playcanvas.com/explore
- https://developer.playcanvas.com/user-manual/engine/standalone/
- https://github.com/playcanvas/engine

### WebGPU Compute Shader Demos

WebGPU became supported across all major browsers in November 2025. Notable demos:

- **Party (Juan Cazala)**: Thousands of particles with real-time physics you can manipulate
- **Fluid Simulations (Matsuoka)**: MLS-MPM method, ~100,000 particles on integrated GPU
- **Particle Life Simulation**: Emergent behavior from simple rules
- **Galaxy Simulation**: 1 million stars with compute shaders
- **Volumetric Snow Globe**: Mesh-based particles with proper normals
- **Sponza with 400+ lights**: Deferred rendering at 50fps

**Sources:**
- https://www.webgpu.com/showcase/party-webgpu-particle-physics-playground/
- https://tympanus.net/codrops/2025/02/26/webgpu-fluid-simulations-high-performance-real-time-rendering/
- https://lisyarus.github.io/blog/posts/particle-life-simulation-in-browser-using-webgpu.html

### PixiJS v8 (Best 2D)

PixiJS v8 launched with WebGPU integration:

- Fastest 2D WebGL/WebGPU renderer
- Particle systems for explosions, fire, magic, environmental effects
- Multi-texture batching, custom shaders
- Consistent 60fps on modest hardware
- Render textures for dynamic content generation

**Sources:**
- https://pixijs.com/
- https://pixijs.com/showcase

---

## 2. Game Engines for Military/Adversarial Simulation

### RECOMMENDED: Babylon.js + Havok + Recast Navigation + Yuka.js

This is the most complete stack for your use case. Here is why:

**Babylon.js provides:**
- 3D rendering with WebGPU
- Heightmap terrain (single line of code)
- Dynamic terrain extension for infinite worlds
- Area lights for atmospheric lighting
- Instanced meshes for 1000+ units at 144fps

**Havok Physics (built into Babylon.js) provides:**
- AAA-quality rigid body physics
- Collision detection
- Vehicle physics (tank treads, wheeled vehicles)
- Available from CDN: `https://cdn.babylonjs.com/havok/HavokPhysics_umd.js`

**Setup code:**
```javascript
const havokInstance = await HavokPhysics();
const plugin = new BABYLON.HavokPlugin(true, havokInstance);
scene.enablePhysics(new BABYLON.Vector3(0, -9.81, 0), plugin);
```

**Recast Navigation (built into Babylon.js) provides:**
- Navigation mesh generation from terrain
- Crowd agent simulation with path finding and avoidance
- Autonomous agents that navigate around obstacles
- 1000+ agents pathfinding simultaneously

**Yuka.js provides (engine-agnostic AI layer):**
- Steering behaviors: seek, flee, pursuit, evade, arrive, wander
- Formation control for unit groups
- State-driven agent design (FSMs)
- Goal-driven agent design (behavior trees)
- Navigation mesh pathfinding
- Fuzzy logic for decision making
- Works with both Babylon.js AND Three.js

**Yuka.js Key Demos:**
- Soccer simulation with tiered team AI and hierarchical decision making
- Pursuit/evade behaviors
- First-person shooter AI (deathmatch)
- https://mugen87.github.io/yuka/examples/
- https://mugen87.github.io/yuka/showcases/

**Sources:**
- https://doc.babylonjs.com/features/featuresDeepDive/physics/havokPlugin
- https://doc.babylonjs.com/features/featuresDeepDive/crowdNavigation/crowdAgents/
- https://github.com/Mugen87/yuka
- https://mugen87.github.io/yuka/

### Alternative: Three.js + Rapier + Yuka.js

**Rapier Physics (Rust/WASM):**
- 2D and 3D physics engine written in Rust, compiled to WASM
- 2-5x speed improvements over 2024 version
- SIMD-accelerated collision detection
- Official NPM packages and CDN support
- Handles thousands of active physics bodies
- Built-in Three.js integration: `THREE.RapierPhysics`

**Three.js + Rapier Example Projects:**
- three-game-engine: Simple lightweight game engine using Three.js + three-mesh-ui + Rapier (https://github.com/WesUnwin/three-game-engine)
- Various CodeSandbox examples with physics
- Official Three.js Rapier integration docs

**Sources:**
- https://rapier.rs/
- https://github.com/dimforge/rapier
- https://threejs.org/docs/pages/RapierPhysics.html

### Phaser 3 (Polished 2D Alternative)

For a polished 2D approach:
- **Strike Tactics**: Full RTS with workers, resources, factories, unit selection, waypoints, AI opponents
- **Medieval War**: Turn-based strategy inspired by Fire Emblem
- **RPS**: Complete RTS with campaign, multiplayer, AI
- Phaser 3 now has AI integration examples

**Limitation**: 2D only, may not look "impressive enough" for DeepMind audience

**Sources:**
- https://phaser.discourse.group/t/is-possible-to-create-rts-game-with-phaser-3/3866
- https://phaser.io/news/2017/08/strike-tactics

---

## 3. Existing Browser-Based Strategy/Simulation Games (Forkable or Referenceable)

### Open-Source Browser RTS Games

| Project | Tech Stack | Stars | Visual Quality | AI Support | Link |
|---------|-----------|-------|---------------|------------|------|
| **Freeciv-web** | Three.js + WebGL + Java backend | 2k+ | Good (Civ-style 3D) | Built-in AI opponents | https://github.com/freeciv/freeciv-web |
| **Kiomet** | Rust + WASM + WebGL + GLSL | Active | Polished hex-grid | Multiplayer | https://github.com/SoftbearStudios/kiomet |
| **emnh/rts** | WebGL + ClojureScript | Small | Technical demo | WIP | https://emnh.github.io/rts-blog/ |
| **limeforadime/phaser-rts** | Phaser + Express | Small | Basic 2D | Multiplayer | https://github.com/limeforadime/phaser-rts |
| **VillagePrototype** | Three.js | Small | Basic 3D RTS camera | None | https://github.com/sasoh/VillagePrototype |

### Notable Existing Tank/Combat Games

| Project | Engine | Description | Link |
|---------|--------|-------------|------|
| **Tank Firefight 3D** | Babylon.js | Battle City-inspired tank warfare | Babylon.js Forum |
| **3D Tank Game** | Babylon.js | AI enemies that track and engage player, health bars | Medium tutorial |
| **Battle Tank** | Three.js | Real physics, functional targeting system | Three.js forum |
| **BattleTanks** | Three.js | 3D battle tank game | https://github.com/EGalahad/BattleTanks |
| **TankGame** | Three.js | Multiplayer tank battle in JavaScript | https://github.com/lazd/TankGame |

### Browser-Based .io Games Worth Studying

- **Kiomet.com**: Hex-grid multiplayer RTS, 27 tower types, Rust+WASM, open source AGPL-3.0
- **Robostorm** (PlayCanvas): Multiplayer robot battle with particle effects
- **Mini Royale: Nations** (PlayCanvas): Browser FPS with social strategy

### AI Wargame Simulation Platforms

| Platform | Description | Visualization | Link |
|----------|-------------|--------------|------|
| **WarAgent** | LLM-based multi-agent WWI/WWII simulation | Text-based + charts | https://github.com/agiresearch/WarAgent |
| **SIM-1 (Fable Studio)** | Multi-agent competition simulation | Unreal Engine 5 render | https://fablestudio.github.io/openai-wargames/ |
| **GenWar (JHU APL)** | AI wargaming with LLM agents | Physics-based models | JHU APL |
| **WarMatrix (USAF)** | AI-powered digital sandbox | Autonomous agent entities | Defense News |
| **Snow Globe** | LLM-powered qualitative wargames | Text-based | Academic |
| **Sean Goedecke's Wargame** | RTS with text orders to AI generals | Browser-based | https://www.seangoedecke.com/wargame-agents/ |

**Sources:**
- https://github.com/freeciv/freeciv-web
- https://github.com/SoftbearStudios/kiomet
- https://github.com/agiresearch/WarAgent
- https://fablestudio.github.io/openai-wargames/
- https://www.seangoedecke.com/wargame-agents/

---

## 4. World Simulation Platforms

### Oasis (Decart) - AI-Generated Minecraft

- Generates frames in real-time using next-frame prediction
- Runs in browser at oasis2.decart.ai
- 47ms inference per frame on NVIDIA H100
- 360p at 20fps
- **NOT suitable for your use case**: It is a neural network generating video frames, not a controllable simulation. You cannot programmatically control units.

### Browser Voxel Engines

| Engine | Tech | Description | Link |
|--------|------|-------------|------|
| **Wave** | WASM (rewrite of noa-engine) | LOD system, dynamic lighting via cellular automata | https://github.com/skishore/wave |
| **All is Cubes** | Rust + WASM | Blocks made of blocks, interactive editing | https://github.com/kpreid/all-is-cubes |
| **Voxel.js** | JavaScript + npm modules | ~200 addons on NPM, modular architecture | https://voxeljs.com/ |
| **Multiplayer Voxel Engine** | HTML5 | Open-sourced multiplayer 3D voxel browser engine | kevzettler.com |

### Agent-Based Modeling in Browser

**AgentScript** is particularly relevant:
- NetLogo-like semantics (Patches, Turtles, Links)
- MVC architecture separating model from view
- Three.js 2.5D and 3D visualization views
- Browser-based with ES6 modules
- https://agentscript.org/
- https://github.com/backspaces/agentscript

**Multi-Agent Web Simulation (AgentSimJs + ThreeJs):**
- https://github.com/damianoc90/Multi-Agent-web-simulation-based-on-AgentSimJs-ThreeJs

---

## 5. FASTEST PATH to an Impressive Hackathon Demo

### OPTION A: Babylon.js Full Stack (RECOMMENDED - Highest Impact, ~90 min setup)

**What you get**: 3D terrain with heightmap, 50+ animated soldier units per team (red/blue), pathfinding via navigation mesh, Havok physics for collisions and projectiles, area lighting for atmosphere, real-time HUD overlay.

**Single HTML file approach:**
```html
<!DOCTYPE html>
<html>
<head>
  <script src="https://cdn.babylonjs.com/babylon.js"></script>
  <script src="https://cdn.babylonjs.com/babylonjs.materials.min.js"></script>
  <script src="https://cdn.babylonjs.com/babylonjs.loaders.min.js"></script>
  <script src="https://cdn.babylonjs.com/havok/HavokPhysics_umd.js"></script>
  <script src="https://cdn.babylonjs.com/babylon.gui.min.js"></script>
  <!-- Recast for navigation mesh -->
  <script src="https://preview.babylonjs.com/babylonjs.proceduralTextures.min.js"></script>
</head>
<body>
  <canvas id="renderCanvas" style="width:100%;height:100vh;"></canvas>
  <script>
    // Full game scene setup here
  </script>
</body>
</html>
```

**Key capabilities available from CDN:**
1. `MeshBuilder.CreateGroundFromHeightMap()` -- instant terrain
2. `HavokPlugin` -- physics for all entities
3. Crowd navigation via Recast -- pathfinding for all units
4. `mesh.createInstance()` -- 1000+ units at 144fps
5. `AreaLight` -- cinematic lighting
6. `BABYLON.GUI` -- in-scene HUD elements

**Where to get 3D assets:**
- Clara.io: 100,000+ free models including military vehicles, tanks, soldiers (OBJ, glTF, Babylon formats)
- Sketchfab: Free Babylon.js models
- 3D Babylon Marketplace: Free game assets

### OPTION B: Three.js + Rapier + Yuka (~2 hr setup)

**What you get**: 3D scene with procedural terrain, physics-driven units, AI steering behaviors (pursue, evade, formation), programmatic control.

```html
<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.170/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.170/examples/jsm/",
    "yuka": "https://cdn.jsdelivr.net/npm/yuka/build/yuka.module.js"
  }
}
</script>
```

**Key components:**
1. Three.js for rendering
2. Rapier WASM for physics (via Three.js built-in `RapierPhysics`)
3. Yuka.js for AI steering behaviors and navigation
4. OrthographicCamera for RTS-style top-down view
5. Instanced meshes for unit rendering

### OPTION C: PlayCanvas Standalone (~1 hr setup)

**What you get**: Engine with built-in physics, zero compile time, entity-component architecture.

```html
<script type="importmap">
{
  "imports": {
    "playcanvas": "https://cdn.jsdelivr.net/npm/playcanvas/+esm"
  }
}
</script>
```

### OPTION D: WebGPU Compute Shader Particle Simulation (~2 hr setup)

For maximum visual "wow factor" without game-like structure:
- 500,000+ particles with GPU compute
- Boids/flocking for emergent behavior
- Use Three.js WebGPU examples as starting point
- https://threejs.org/examples/webgpu_compute_particles.html
- https://threejs.org/examples/webgl_gpgpu_birds.html

### OPTION E: Fork Existing Browser RTS

**Fastest to "something that looks like a real game":**
- Fork Kiomet (Rust/WASM, hex-grid, multiplayer RTS): https://github.com/SoftbearStudios/kiomet
- Fork Freeciv-web (Three.js, civilization strategy): https://github.com/freeciv/freeciv-web
- Use VillagePrototype as RTS camera base: https://github.com/sasoh/VillagePrototype

---

## 6. Comparative Analysis: What to Choose

### Decision Matrix

| Criterion | Babylon.js+Havok | Three.js+Rapier+Yuka | PlayCanvas | Phaser 3 | WebGPU Raw |
|-----------|-----------------|----------------------|-----------|---------|------------|
| Visual Quality | 10/10 | 8/10 | 9/10 | 6/10 | 10/10 |
| Setup Speed | 9/10 | 7/10 | 8/10 | 9/10 | 4/10 |
| Physics Quality | 10/10 (Havok) | 9/10 (Rapier) | 7/10 | 6/10 | N/A |
| AI Agent Support | 9/10 (Crowd Nav) | 9/10 (Yuka) | 6/10 | 5/10 | 1/10 |
| Unit Pathfinding | 10/10 (Recast built-in) | 8/10 (Yuka navmesh) | 5/10 | 4/10 | 0/10 |
| Programmatic Control | 10/10 | 10/10 | 9/10 | 8/10 | 10/10 |
| CDN / Single File | Yes | Yes | Yes | Yes | Partial |
| 3D Terrain | Built-in | Manual | Partial | No | Manual |
| Community Size | Large | Largest | Medium | Large | Small |
| DeepMind "Wow" Factor | High | Medium-High | Medium | Low | Very High |
| Hackathon Feasibility | High | Medium | High | High | Low |

### STRONG RECOMMENDATION

**For your specific use case (adversarial agent simulation for DeepMind):**

**Primary: Babylon.js + Havok + Crowd Navigation**

Reasons:
1. Built-in heightmap terrain generation (one line of code)
2. Havok is the same physics engine used in AAA games -- DeepMind will recognize it
3. Built-in crowd navigation with Recast -- agents pathfind and avoid each other automatically
4. 1000+ animated entities at 144fps via instanced meshes
5. Area lights for cinematic atmosphere
6. Everything available from CDN, no build step
7. The Babylon.js team specifically wrote about building RTS-style games with large unit counts
8. WebGPU support for additional compute if needed

**Supplementary: Add Yuka.js for Higher-Level AI Behaviors**

Yuka.js works with both Babylon.js and Three.js, providing:
- Pursuit, evade, flee, arrive, wander steering behaviors
- Formation control
- State machines and behavior trees for decision making
- This is where you plug in your adversarial AI logic

---

## 7. Research Gaps

1. **No single open-source browser RTS with AI agents that looks AAA-quality**: The closest is Kiomet (polished but 2D hex-grid) and Freeciv-web (functional but dated visuals).

2. **SIM-1/GenWar are not browser-renderable**: Fable Studio's SIM-1 uses Unreal Engine 5 for visualization, not browser-native rendering. GenWar uses AFSIM which is a separate modeling framework.

3. **0 A.D. web port does not exist**: 0 A.D. is a native C++ game with no browser version. OpenRA also has no web port.

4. **Oasis is not controllable**: It generates video frames via neural network -- you cannot programmatically control units or access game state.

5. **PlayCanvas physics**: While PlayCanvas has built-in physics, its standalone (no-editor) physics documentation is thinner than Babylon.js + Havok.

---

## 8. Confidence Assessment

| Finding | Confidence |
|---------|-----------|
| Babylon.js 8.0 is the most complete browser game engine | HIGH |
| Havok physics runs in browser via WASM from CDN | HIGH (verified in documentation) |
| 1000+ animated units at 144fps is achievable | HIGH (Babylon.js blog post with benchmarks) |
| Yuka.js provides steering/pathfinding for both engines | HIGH (verified examples exist) |
| Rapier WASM is the best standalone physics option | HIGH (benchmarked, actively developed) |
| Setup in under 2 hours is feasible with CDN approach | MEDIUM-HIGH (depends on asset complexity) |
| DeepMind researchers will be impressed by Babylon.js quality | MEDIUM (subjective, but the rendering quality is objectively superior to basic demos) |
| Kiomet source code can be forked and adapted | MEDIUM (AGPL license, Rust ecosystem complexity) |
| WebGPU compute is ready for production use | HIGH (supported in all major browsers since Nov 2025) |

---

## 9. Recommended Follow-ups

1. **Try the Babylon.js Playground immediately**: Visit https://playground.babylonjs.com/ and search for "heightmap", "crowd", "instanced" to see working examples you can copy
2. **Look at the Babylon.js "Creating thousands of animated entities" blog post**: https://babylonjs.medium.com/creating-thousands-of-animated-entities-in-babylon-js-ce3c439bdacf
3. **Browse Yuka.js showcases**: https://mugen87.github.io/yuka/showcases/ -- the soccer simulation shows exactly the kind of multi-agent behaviors you need
4. **Download free military 3D models from Clara.io**: Search "military" or "tank" in glTF format
5. **Study Sean Goedecke's wargame-agents**: https://www.seangoedecke.com/wargame-agents/ -- directly relevant to LLM-controlled RTS units
6. **Examine WarAgent codebase**: https://github.com/agiresearch/WarAgent -- LLM multi-agent simulation of conflicts

---

## 10. Quick-Reference: CDN URLs for Immediate Use

### Babylon.js Full Stack
```
https://cdn.babylonjs.com/babylon.js
https://cdn.babylonjs.com/babylon.max.js (debug)
https://cdn.babylonjs.com/babylonjs.materials.min.js
https://cdn.babylonjs.com/babylonjs.loaders.min.js
https://cdn.babylonjs.com/havok/HavokPhysics_umd.js
https://cdn.babylonjs.com/babylon.gui.min.js
```

### Three.js + Addons
```
https://cdn.jsdelivr.net/npm/three@0.170/build/three.module.js
https://cdn.jsdelivr.net/npm/three@0.170/examples/jsm/  (addons)
```

### Rapier Physics
```
https://cdn.jsdelivr.net/npm/@dimforge/rapier3d-compat/rapier.js
```

### Yuka Game AI
```
https://cdn.jsdelivr.net/npm/yuka/build/yuka.module.js
```

### PlayCanvas Engine
```
https://cdn.jsdelivr.net/npm/playcanvas/+esm
```

### PixiJS v8
```
https://cdn.jsdelivr.net/npm/pixi.js@8/dist/pixi.min.js
```

### Phaser 3
```
https://cdn.jsdelivr.net/npm/phaser@3/dist/phaser.min.js
```
