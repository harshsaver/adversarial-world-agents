# Example Scenarios

The Adversarial World Agents platform supports configurable scenarios. The user describes a scenario, and the system generates an appropriate environment, spawns agents with scenario-specific capabilities, and runs the simulation.

---

## 1. Urban Defense

**Description:** A city is under attack. The attacker deploys units to infiltrate and destroy key infrastructure. The defender must protect critical buildings and eliminate the attacker's forces.

**Environment:**
- City blocks as obstacles
- Streets as corridors
- Key buildings marked as objectives
- Elevated positions for tactical advantage

**Attacker Objective:** Destroy 3+ key buildings or eliminate all defenders

**Defender Objective:** Protect all key buildings for the duration or eliminate all attackers

**Special Mechanics:**
- Buildings have HP and can be damaged
- Narrow streets create chokepoints
- Line of sight blocked by buildings

---

## 2. Naval Battle

**Description:** Two fleets engage on open water. The attacker tries to reach and destroy a port/harbor. The defender patrols the waters and intercepts.

**Environment:**
- Open water with islands as obstacles
- Harbor/port as the base objective
- Shallow areas that restrict movement
- Current/wind affecting unit movement

**Attacker Objective:** Reach and damage the harbor

**Defender Objective:** Sink all attacking ships or prevent harbor damage until time expires

**Special Mechanics:**
- Different unit types (fast scouts, heavy battleships)
- Torpedo/ranged attacks
- Island cover

---

## 3. Cyber Attack/Defense

**Description:** A digital network is under attack. The attacker tries to breach firewalls and access protected data nodes. The defender deploys countermeasures and patches vulnerabilities.

**Environment:**
- Network topology as a graph
- Nodes as servers/databases
- Edges as network connections
- Firewalls as barriers

**Attacker Objective:** Access 3+ protected data nodes

**Defender Objective:** Prevent data breaches, isolate compromised nodes

**Special Mechanics:**
- "Hacking" takes time (must stay at node for multiple turns)
- Defender can cut network connections to isolate threats
- Attacker can deploy decoys/distractions

---

## 4. Resource Competition

**Description:** Two factions compete to gather resources from a shared environment. Resources spawn at random locations and must be collected and returned to base.

**Environment:**
- Resource nodes scattered across the map
- Both teams have a home base
- Obstacles and terrain features

**Attacker Objective:** Collect more total resources than the defender

**Defender Objective:** Collect more total resources than the attacker

**Special Mechanics:**
- Units can carry limited resources
- Must return to base to "bank" resources
- Stealing resources from opponent units on kill
- Resource spawn locations change over time

---

## 5. Territory Control

**Description:** Two teams compete to control territory on a map. Standing in an area claims it. The team with the most territory when time expires wins.

**Environment:**
- Map divided into control zones
- Neutral zones start unclaimed
- Obstacles and chokepoints between zones

**Attacker Objective:** Control 60%+ of zones by end of timer

**Defender Objective:** Prevent attacker from reaching 60% control

**Special Mechanics:**
- Zones flip when occupied by one team's units
- Contested zones (both teams present) don't change
- Some zones worth more than others (strategic points)
- Flanking and multi-front strategies emerge naturally

---

## 6. Infrastructure Attack (IsoCity Canvas)

**Description:** One agent builds a city (placing buildings, infrastructure, defenses). The other agent tries to destroy it. Uses the IsoCity isometric canvas as the visual environment.

**Environment:**
- Isometric city grid (from [isometric-city-swart.vercel.app](https://isometric-city-swart.vercel.app))
- Builder places structures on the grid
- Attacker deploys destructive units

**Builder Objective:** Build and maintain a city with population above a threshold

**Attacker Objective:** Reduce city population below threshold by destroying infrastructure

**Special Mechanics:**
- Builder places buildings that generate population/resources
- Attacker destroys buildings, reducing population
- Builder can place defensive structures (walls, turrets)
- Attacker must choose targets strategically (power plants vs houses vs defenses)
- Real-time tug-of-war between construction and destruction

---

## Scenario Configuration

Users configure scenarios via a simple JSON format:

```json
{
  "scenario": "urban_defense",
  "duration_seconds": 120,
  "attacker_units": 8,
  "defender_units": 8,
  "environment": {
    "size": [960, 580],
    "obstacle_density": "medium",
    "theme": "modern_city"
  },
  "objectives": {
    "attacker": "destroy_buildings",
    "defender": "protect_buildings"
  },
  "difficulty": "balanced"
}
```

NanoBanana 2 uses the scenario configuration to generate appropriate terrain and visuals. Lyria generates ambient audio matching the scenario theme.
