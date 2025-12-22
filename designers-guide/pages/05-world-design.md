# World Design

World design includes maps, terrain, encounters, and victory conditions.

## Maps and Grids

### Map Structure

Maps are grids of tiles with coordinates.

**Coordinate notation**: `3N 2E` = 3 spaces North, 2 spaces East from origin

**Directions**:
- Cardinals: N, E, S, W
- Diagonals: NE, SE, SW, NW

### Map Size Guidelines

**Small** (10x10 to 15x15)
- Quick encounters (15-30 min)
- Limited positioning
- Direct combat

**Medium** (20x20 to 30x30)
- Standard encounters (30-60 min)
- Tactical positioning
- Multiple objectives

**Large** (40x40+)
- Long encounters (60+ min)
- Strategic movement
- Multi-phase battles

### Map Representation

Use ASCII art or grid notation:

```
. . . . . .  (plains)
. . # # . .  (# = wall)
. . . . . .
. . W W . .  (W = water)
```

Or coordinate lists:
```
Walls: 3N 2E, 3N 3E
Water: 2N 2E, 2N 3E
```

## Terrain and Tiles

### Tile Properties

**Movement Cost**
How many movement points to enter.

Examples:
- Plains: 1 point
- Forest: 2 points
- Mountains: 3 points
- Water: Impassable (or requires swimming)

**Cover**
Defensive bonuses when occupying tile.

Examples:
- Half Cover: +2 Defense
- Full Cover: +5 Defense
- No Cover: +0 Defense

**Special Effects**
Triggered when entering or occupying.

Examples:
- Fire: 1d4 damage per turn
- Ice: Movement cost +1
- Healing Spring: +1d6 Health per turn

### Terrain Features

**Obstacles**
Block movement or line of sight.

**Elevation**
High ground provides bonuses.

**Difficult Terrain**
Increased movement costs.

**Hazards**
Damage or status effects.

## Encounter Design

### Core Elements

**Objective**
What must players accomplish?

Examples:
- Defeat all enemies
- Reach location X
- Survive X turns
- Protect NPC
- Collect X items

**Enemy Placement**
Where do NPCs start?

Consider:
- Distance from players
- Cover availability
- Tactical advantages

**Victory Condition**
How do players win?

**Defeat Condition**
How do players lose?

### Encounter Difficulty

Balance based on:

**Player Count**
More players = more or stronger enemies

**Resource Availability**
Limited healing = harder
Abundant actions = easier

**Tactical Complexity**
Simple map = focus on combat
Complex terrain = positioning matters

**Enemy Strength**
- Swarm: Many weak enemies
- Elite: Few strong enemies
- Mixed: Variety of threats

## Progressive Complexity

Introduce mechanics gradually:

**Encounter 1: Foundation**
- Core mechanics only (movement, basic actions)
- Simple map
- Straightforward objective

**Encounter 2: First Expansion**
- Add 1-2 new mechanics (cover, consumables)
- More complex map
- Build on Encounter 1

**Encounter 3: Combination**
- Add more mechanics (status effects, special tiles)
- Combine previous mechanics
- Multi-phase or multi-objective

**Encounter 4+: Full Complexity**
- All mechanics available
- Complex interactions
- Boss fights or strategic challenges

## Features

Features are passive rules that modify core mechanics.

### Common Feature Types

**Initiative**
```
Initiative Roll (Feature)
Roll 1d20 + Dexterity at start of encounter
Highest result goes first
```

**Movement**
```
Standard Movement (Feature)
All actors move up to 6 spaces per turn
```

**Victory Conditions**
```
Survival Victory (Feature)
Game ends when all enemies defeated
Players with Health > 0 are victorious
```

**Resource Maximums**
```
Health Maximum (Feature)
Health cannot exceed initial rolled value
```

**Turn Structure**
```
Flexible Turns (Feature)
Actors may move and act in any order during their turn
```

## Campaign Structure

### Single Encounter Campaigns

Structure:
1. Introduction
2. Setup guide
3. Resource glossary
4. Action reference
5. Map and encounter
6. Quick reference

Keep everything in one document.

### Multi-Encounter Campaigns

Structure:
1. Introduction
2. Setup guide (character creation)
3. Encounters (separate chapter per encounter)
4. Entity definitions (all NPCs, actions, strategies)
5. Quick reference

**Separate entities from encounters** for reusability and clarity.

#### Encounter Chapters Include

- Map layout
- Enemy names, quantities, positions
- New mechanics introduced
- Victory/defeat conditions
- Loot and rewards
- Reference to entity definitions (e.g., "see Ch 5")

#### Entity Definition Chapter Includes

- Player actions
- NPC actors and stats
- NPC strategies and behaviors
- Shared features
- Reusable components

### Example Encounter Chapter

```
# Encounter 2: Dark Crypt

## Map
[Grid layout showing walls, traps, darkness zones]

## Enemies
- 3× Draugr (see Entity Definitions)
  - Draugr 1: 5N 3E, facing South
  - Draugr 2: 8N 8E, facing West
  - Draugr 3: 2N 10E, facing South

## New Mechanics
- Darkness: Ranged attacks have -5 penalty
- Traps: Pressure plates deal 1d6 damage

## Victory
Defeat all Draugr and reach exit (12N 6E)

## Loot
- 65 Gold
- Ancient Blade (+3 melee damage)
```

### Example Entity Definition

```
# Entity Definitions

## Draugr (Actor)
Resources:
  Health: 45
  ActionPoints: 2
  Defense: 3

Features:
  - Frost Resistance 50%
  - Undead (immune to poison)

Strategy: Relentless Assault

## Draugr Actions

### Frost Touch
if: Adjacent to target
do: [Target Health] -= (1d6 + 3), apply Frost 1
then: [ActionPoints] -= 1

## Draugr Strategy: Relentless Assault

Behavior 1: Use Frost Touch if adjacent to enemy
Behavior 2: Move toward nearest enemy
```

## Balancing Encounters

### Playtest Checklist

☐ Clear victory condition
☐ Appropriate difficulty for player count
☐ Interesting tactical decisions
☐ No dominant strategies
☐ Encounter resolves in target time
☐ New mechanics explained clearly

### Common Balance Issues

**Too Easy**
- Reduce enemy Health
- Increase enemy damage
- Add more enemies
- Limit player resources

**Too Hard**
- Increase enemy Health
- Decrease enemy damage
- Remove enemies
- Add player resources or healing

**Too Long**
- Reduce enemy count
- Simplify map
- Increase damage on both sides

**Too Short**
- Add enemies
- Increase Health pools
- Expand map

## Loot and Rewards

### Loot Design

**Gold/Currency**
Quantifiable rewards.

**Equipment**
Items that modify stats or grant new actions.

**Consumables**
One-use items (potions, scrolls).

**Progression**
Unlocks for future encounters.

### Loot as Features

```
Ancient Blade (Feature)
Equipped by: Player
Effect: Melee attacks deal +3 damage and +1d4 frost
```

Equipment modifies actions or resources through features.

## Campaign Book Organization

### Essential Sections

1. **Introduction**: Theme, player count, materials, play time
2. **Setup**: Character creation, starting resources
3. **Resource Glossary**: All resources and initialization
4. **Actions**: All player actions
5. **Features**: Passive rules (initiative, movement, etc.)
6. **Encounters**: Maps, enemies, objectives
7. **Entity Definitions**: NPCs and strategies (if multi-encounter)
8. **Quick Reference**: Turn structure, common calculations

### Writing Style

**Mechanical rules**: Clear, unambiguous
**Flavor text**: Optional, enhances theme

Example:
```
Victory Condition: Defeat all enemies

"As the last Draugr crumbles, the crypt falls silent. Skyrim is safe."
```

Mechanics first, flavor second.

## Testing Your Campaign

**Solo Playtest**
Play both sides to check rules clarity and balance.

**Group Playtest**
Have others play to find confusing rules and unintended strategies.

**Iterate**
Revise based on feedback: clarify rules, rebalance, add missing content.

Focus testing on:
- Rules clarity
- Balance
- Pacing
- Engagement
