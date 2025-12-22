# Reference

## Action Template

```
[Action Name] (Action)
Range: [Adjacent / X spaces / Unlimited]
Target: [Single actor / Multiple / Area]

if: [Condition that must be true]
do: [Effects when condition is TRUE]
else: [Effects when condition is FALSE] (optional)
then: [Effects that ALWAYS execute]
```

**Example**:
```
Power Strike (Action)
Range: Adjacent
Target: Single actor

if: [ActionPoints] >= 2 AND Adjacent to target
do: [Target Health] -= (2d6 + [Strength])
else: (none)
then: [ActionPoints] -= 2
```

## Check Template

```
[Check Name] (Check)
[Boolean condition that evaluates to true or false]
```

**Example**:
```
Has ActionPoint (Check)
[ActionPoints] >= 1
```

## Effect Template

```
[Effect Name] (Effect)
[Plain English command describing state change]
```

**Example**:
```
Deal Basic Damage (Effect)
[Target Health] -= (1d6 + [Strength])
```

## Feature Template

```
[Feature Name] (Feature)
[Description of passive rule or modification]
[When it applies and what it does]
```

**Examples**:
```
Initiative Roll (Feature)
Roll 1d20 + Dexterity at start of encounter
Highest result goes first each round
```

```
Health Maximum (Feature)
Health cannot exceed initial rolled value
If effect would increase Health above maximum, Health stays at maximum
```

## Behavior Template

```
Behavior: [Behavior Name]
Checks:
  - [Condition 1]
  - [Condition 2]
Action: [What NPC does if all checks pass]
```

**Example**:
```
Behavior: Attack Nearest
Checks:
  - Enemy within 5 spaces
  - [ActionPoints] >= 1
Action: Move toward nearest enemy, attack if adjacent
```

## Strategy Template

```
[Strategy Name] (Strategy)
Priority 1: [Highest priority behavior]
Priority 2: [Second priority behavior]
Priority 3: [Third priority behavior]
...
```

**Example**:
```
Aggressive Melee (Strategy)
Priority 1: Flee if [Health] < 3
Priority 2: Attack if adjacent to enemy
Priority 3: Move toward nearest enemy
```

## NPC Template

```
[NPC Name] (Actor)
Resources:
  [Resource]: [Value or initialization]
  [Resource]: [Value or initialization]

Features:
  - [Feature description]

Strategy: [Strategy Name]
```

**Example**:
```
Goblin (Actor)
Resources:
  Health: 25
  ActionPoints: 2

Features:
  - Cowardly: Flees when Health < 5

Strategy: Aggressive Melee
```

## Resource Template

```
[Resource Name] (Resource)
Initialize: [Starting value, dice roll, or calculation]
Maximum: [Value or "None"]
Usage: [How this resource is used]
```

**Examples**:
```
Health (Resource)
Initialize: 1d20 + [Constitution]
Maximum: Initial value
Usage: Defeat condition when reaches 0
```

```
ActionPoints (Resource)
Initialize: 3
Maximum: 3
Usage: Gates number of actions per turn
Regeneration: 3 at start of turn
```

## Encounter Template

```
# Encounter [Number]: [Name]

## Objective
[What players must accomplish]

## Map
[Grid layout, terrain features, dimensions]

## Starting Positions
Players: [Coordinates]
Enemies: [Names, quantities, coordinates]

## New Mechanics
- [Mechanic 1]: [Description]
- [Mechanic 2]: [Description]

## Victory Condition
[How players win]

## Defeat Condition
[How players lose]

## Loot
- [Items and quantities]
```

**Example**:
```
# Encounter 1: Roadside Ambush

## Objective
Defeat all bandits

## Map
20x15 grid, plains with scattered rocks for half cover
Rocks at: 5N 3E, 8N 10E, 12N 5E

## Starting Positions
Players: 0N 0E (South edge)
Enemies: 3× Bandit at 15N 5E, 15N 10E, 18N 7E

## New Mechanics
- Half Cover: +2 Defense when behind rocks

## Victory Condition
All bandits defeated

## Defeat Condition
All players reach 0 Health

## Loot
- 37 Gold (total)
- Health Potion (restores 2d6 Health)
```

## Quick Reference

### Action Structure

```
if → [do OR else] → then
```

Always executes: (then)
Conditional: (do) if true, (else) if false

### Dice Notation

- `XdY`: Roll X dice with Y sides
- `1d6+3`: Roll d6, add 3
- `2d10*[Strength]`: Roll 2d10, multiply by Strength

### Resource Notation

- `[Resource]`: Your resource value
- `[Target Resource]`: Target's resource value
- `[Resource] >= 5`: Comparison
- `[Resource] -= 3`: Modification

### Operators

- `+` Addition
- `-` Subtraction
- `*` Multiplication
- `/` Division (rounds down)

### Special Math Rules

- Division by zero = 0
- Negative results = 0
- Fractions round down

### Component References

- `#Name`: Reference check or effect
- Defined once, used many times

## Design Checklist

### Action Design

☐ Condition is precise and measurable
☐ Primary effect creates meaningful outcome
☐ Always-effects serve clear purpose
☐ Alternative effect creates interesting failure (if used)
☐ Resource costs are balanced
☐ Action has clear use case

### Resource Design

☐ Clear purpose and usage
☐ Initialization rule defined
☐ Changes during gameplay
☐ Creates meaningful decisions
☐ Name is unambiguous
☐ Maximum defined if needed

### NPC Design

☐ Minimal resources (only what's needed)
☐ Clear behaviors with 1-3 checks each
☐ Fallback behavior exists
☐ Strategy priority makes sense
☐ Behavior is predictable but not trivial

### Encounter Design

☐ Clear objective
☐ Appropriate difficulty
☐ Interesting tactical decisions
☐ New mechanics explained
☐ Victory and defeat conditions defined
☐ Resolves in target time

### Campaign Book

☐ Introduction (theme, players, materials, time)
☐ Setup guide (character creation)
☐ Resource glossary
☐ Action reference
☐ Features
☐ Encounters
☐ Entity definitions (if multi-encounter)
☐ Quick reference

## Common Patterns

### Basic Combat Action

```
Attack
if: Adjacent to target AND [ActionPoints] >= 1
do: [Target Health] -= (1d6 + [Strength])
then: [ActionPoints] -= 1
```

### Risky Action

```
Risky Strike
if: 1d20 + [Dexterity] > [Target Defense] + 10
do: [Target Health] -= 3d6
else: [Health] -= 1d6
then: [ActionPoints] -= 2
```

### Resource Conversion

```
Rest
if: [Energy] >= 2
do: [Energy] -= 2, [Health] += 1d6
```

### Conditional Scaling

```
Execute
if: [Target Health] < 5
do: [Target Health] -= 10d6
else: [Target Health] -= 1d6
then: [ActionPoints] -= 3
```

### NPC Melee Behavior

```
Strategy: Aggressive Melee
Priority 1: Flee if [Health] < 5
Priority 2: Attack if adjacent to enemy
Priority 3: Move toward nearest enemy
```

### NPC Ranged Behavior

```
Strategy: Defensive Ranged
Priority 1: Retreat if enemy adjacent
Priority 2: Ranged attack if enemy within 10 spaces
Priority 3: Melee if cornered
```

## Glossary

**Action**: Structured operation (if/do/then/else) that actor can perform

**Actor**: Named entity with location, heading, resources, and actions

**Behavior**: Single conditional action rule for NPCs

**Campaign**: Collection of content definitions using Methuen framework

**Check**: Boolean condition (true/false)

**Effect**: Active change to game state

**Expression**: Mathematical formula (dice + resources + operators)

**Feature**: Passive rule modifying core mechanics

**Initiative**: Turn order value

**Resource**: Named value (positive integer ≥ 0)

**Strategy**: Collection of behaviors in priority order

**Tile**: Single grid coordinate with properties

## Balance Guidelines

### Resource Flow

**Sources > Sinks**: Resources accumulate (game becomes easier)
**Sources < Sinks**: Resources deplete (game becomes harder)
**Sources ≈ Sinks**: Balanced (ideal for most campaigns)

### Action Power

**Light actions**: 1 AP, moderate effect
**Medium actions**: 1-2 AP, strong effect
**Heavy actions**: 2-3 AP, powerful effect

Scale cost with power.

### Enemy Strength

**Swarm**: Many weak enemies (Health 10-20)
**Standard**: Moderate enemies (Health 25-40)
**Elite**: Strong enemies (Health 50-80)
**Boss**: Single powerful enemy (Health 100+, multi-phase)

### Encounter Length

**Quick**: 15-30 minutes, simple objectives
**Standard**: 30-60 minutes, tactical depth
**Long**: 60-90 minutes, complex scenarios
**Epic**: 90+ minutes, multi-phase bosses

Match length to player count and complexity.

## Playtesting Questions

**Clarity**
- Are rules unambiguous?
- Do players understand what to do?
- Are edge cases covered?

**Balance**
- Do players win about 50-70% of the time?
- Are all actions viable?
- Do NPCs provide appropriate challenge?

**Engagement**
- Do players face interesting decisions?
- Is there tactical depth?
- Does gameplay stay fresh?

**Pacing**
- Does the encounter resolve in target time?
- Are turns quick to execute?
- Is downtime minimal?

## Where to Look

**Core mechanics**: Chapters 2-3 (actions and resources)
**NPCs**: Chapter 4 (behaviors and strategies)
**World building**: Chapter 5 (maps, encounters, features)
**Templates**: This chapter
**Player rules**: Methuen Player's Handbook
