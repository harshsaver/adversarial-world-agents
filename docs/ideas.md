# Visual Environment Options Explored

During ideation, we explored many different visual environment approaches for the adversarial simulation. Here is a summary of every option considered, with pros/cons and status.

---

## 1. HTML Canvas 2D Grid

**Status: Viable (simplest)**

A basic 2D grid rendered on HTML Canvas. Units occupy cells, move between cells, and combat happens when units are adjacent.

- **Pros:** Simplest to build, guaranteed to work, easy to snapshot state, very fast
- **Cons:** Least visually impressive, no physics, grid-based movement feels artificial
- **Best for:** Rapid prototyping, guaranteed demo

## 2. Matter.js 2D Physics

**Status: Viable (good balance)**

Full 2D physics simulation using [Matter.js](https://brm.io/matter-js/). Continuous movement, real collisions, obstacles, and walls.

- **Pros:** Good visual quality, real physics, relatively simple API, well-documented
- **Cons:** 2D only, physics can get chaotic with many units
- **Best for:** Balance of visual quality and buildability
- **Demo:** See `demos/matter_demo.html`

## 3. Three.js + cannon-es 3D

**Status: Viable (most impressive)**

Full 3D arena using [Three.js](https://threejs.org/) for rendering and [cannon-es](https://pmndrs.github.io/cannon-es/) for physics.

- **Pros:** Most visually impressive, cinematic camera, shadows, lighting, fog
- **Cons:** More complex to build, 3D state harder to snapshot for agents, performance considerations
- **Best for:** Maximum visual impact for judges/demos
- **Demo:** See `demos/threejs_demo.html`

## 4. p5.js Swarm

**Status: Viable (most artistic)**

Bioluminescent deep-sea swarm simulation using [p5.js](https://p5js.org/) with flocking behaviors.

- **Pros:** Most visually beautiful, additive blending creates stunning effects, unique aesthetic
- **Cons:** Swarm behavior harder to map to strategic AI decisions, more organic than tactical
- **Best for:** Artistic impression, unique visual identity
- **Demo:** See `demos/p5_demo.html`

## 5. Pure Canvas (No Dependencies)

**Status: Viable (fastest)**

Zero-dependency simulation using only the native HTML5 Canvas API.

- **Pros:** No dependencies, maximum performance, full control, works everywhere, ranged combat with projectiles
- **Cons:** Must implement everything from scratch, no physics engine
- **Best for:** Reliability, performance, no dependency risk
- **Demo:** See `demos/canvas_demo.html`

## 6. Harsh's Polytopia Clone

**Status: Considered**

A 3D hexagonal terrain strategy game clone already built by team member Harsh.

- **Repo:** [github.com/harshsaver/polytopia](https://github.com/harshsaver/polytopia)
- **Deployed:** [polytopia-seven.vercel.app](https://polytopia-seven.vercel.app)
- **Features:** 3D hex terrain, existing canvas rendering, unit placement, terrain types
- **Pros:** Already built, visually impressive, hex grid is great for strategy AI
- **Cons:** Would need to adapt for adversarial agents, existing codebase to learn

## 7. Harsh's IsoCity

**Status: Considered (great for infrastructure scenarios)**

An isometric city builder already built by team member Harsh.

- **Deployed:** [isometric-city-swart.vercel.app](https://isometric-city-swart.vercel.app)
- **Features:** Isometric rendering, building placement, city infrastructure
- **Pros:** Perfect for "one builds, one destroys" scenarios, already built
- **Cons:** Not designed for combat, would need significant adaptation

## 8. Minecraft via Mineflayer

**Status: Approved but rejected (too complex)**

Using [Mineflayer](https://github.com/PrismarineJS/mineflayer) to control Minecraft bots in a Minecraft server.

- **Pros:** Rich 3D environment, judges explicitly approved this approach, huge existing ecosystem
- **Cons:** Requires running a Minecraft server, complex setup, latency issues, hard to snapshot state cleanly
- **Judge feedback:** Judges said this would be fine but acknowledged the setup complexity

## 9. Polytopia-style Turn-based

**Status: Rejected**

A turn-based strategy game where agents take turns (like the board game Polytopia).

- **Rejection reason:** Real life is simultaneous, not turn-based. The whole point of the project is that both agents act at the same time, creating emergent adversarial dynamics. Turn-based removes the simultaneity that makes the data interesting.

---

## Decision Matrix

| Option | Visual Quality | Build Speed | Agent Integration | State Snapshotting |
|--------|---------------|-------------|-------------------|-------------------|
| Canvas 2D Grid | Low | Fast | Easy | Easy |
| Matter.js | Medium-High | Medium | Medium | Easy |
| Three.js 3D | Very High | Slow | Hard | Medium |
| p5.js Swarm | Very High | Medium | Medium | Easy |
| Pure Canvas | Medium | Medium | Medium | Easy |
| Polytopia | High | Fast (existing) | Medium | Medium |
| IsoCity | Medium | Fast (existing) | Hard | Medium |
| Minecraft | Very High | Very Slow | Hard | Hard |

## Final Approach

We built demos for the top four options (Matter.js, Three.js, p5.js, Pure Canvas) to let the team compare them side by side and decide based on the actual visual output. All four are included in the `demos/` folder.
