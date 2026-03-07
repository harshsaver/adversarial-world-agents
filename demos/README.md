# Adversarial Simulation Demos

Four interactive physics engine prototypes exploring different visual approaches for the adversarial agent environment.

**Open each HTML file in your browser to compare. No build step needed.**

---

## Demos

### `matter_demo.html` -- 2D Physics with Matter.js

A 2D physics arena built on [Matter.js](https://brm.io/matter-js/). Features:
- Walled arena with rectangular and circular obstacles
- 5v5 red (attacker) vs blue (defender) units
- Glowing units with radial gradients and HP rings
- Collision-based damage with cooldowns
- Particle explosion effects on unit death
- Team connection lines between nearby allies
- Scanline and vignette post-processing effects
- HUD with team HP bars and countdown timer
- Base objective (hexagonal with pulsing glow)
- 60fps with custom Canvas 2D rendering (not Matter.js renderer)

### `threejs_demo.html` -- 3D with Three.js + cannon-es

A cinematic 3D arena built on [Three.js](https://threejs.org/) with [cannon-es](https://pmndrs.github.io/cannon-es/) physics. Features:
- Full 3D arena with ground plane, transparent walls, and grid overlay
- 5v5 spherical units with emissive materials and point lights per unit
- Octahedron crystal base with pedestal and torus ring marker
- ACES filmic tone mapping and PCF soft shadow maps
- Exponential fog for depth
- Orbiting camera that slowly circles the arena
- Physics-based knockback on attacks
- Units shrink as they take damage
- Flash and particle effects on hits
- Death animation (units float upward and fade)
- Dramatic red and blue accent lighting

### `p5_demo.html` -- Bioluminescent Swarm with p5.js

An artistic deep-sea style simulation built on [p5.js](https://p5js.org/). Features:
- 18v18 bioluminescent swarm agents
- Full flocking behaviors (separation, cohesion, alignment)
- Animated tentacles/tendrils per agent with wave physics
- Additive blending for all light effects
- Deep-ocean gradient background with caustic patterns
- Ambient floating particles (multiple colors)
- Hive structure with orbiting particles and breathing animation
- Connection lines between nearby allies
- Combat flash effects at engagement points
- Death burst with directional particles
- HP bars only shown when damaged
- Kill counters per team
- Most visually beautiful of all demos

### `canvas_demo.html` -- Pure Canvas 2D

A zero-dependency simulation using only the HTML5 Canvas API. Features:
- 8v8 units with ranged projectile combat
- Line-of-sight checks (projectiles blocked by obstacles)
- Predictive aim (units lead their targets)
- Randomly generated obstacles per match
- Gradient backgrounds and grid overlay
- Glowing unit rendering with radial gradients
- Trail effects behind moving units
- HP bars with color coding (green/yellow/red)
- Impact spark particles and death explosions
- Minimap in bottom-right corner
- FPS counter
- 60fps with no external dependencies whatsoever
- Obstacle avoidance AI with steering behaviors
- Base defense objective with hexagonal indicator

---

## Comparison

| Feature | Matter.js | Three.js | p5.js | Canvas |
|---------|-----------|----------|-------|--------|
| Dimensions | 2D | 3D | 2D | 2D |
| Dependencies | matter.js | three.js + cannon-es | p5.js | None |
| Unit Count | 5v5 | 5v5 | 18v18 | 8v8 |
| Combat Type | Collision | Melee | Proximity | Ranged (projectiles) |
| Visual Style | Sci-fi HUD | Cinematic | Bioluminescent | Military tactical |
| Best For | Physics accuracy | Visual impressiveness | Artistic beauty | Reliability + speed |
