# Designing Resources

Resources track everything important in Methuen. Well-designed resources create meaningful game state and interesting decisions.

## Resource Types

### Capability Resources

Define what actors can do:
- Strength, Dexterity, Intelligence
- Skills and proficiencies
- Ranges and reach

Use when: The value modifies expressions or gates actions.

### State Resources

Track current condition:
- Health, Energy, Stamina
- Temporary buffs/debuffs
- Status durations

Use when: The value changes frequently during play.

### Currency Resources

Tradeable or spendable:
- Gold, Materials, Food
- ActionPoints, MovementPoints
- Ammunition, Charges

Use when: Actors make spending decisions.

### Counter Resources

Track uses or quantities:
- Attacks made
- Damage taken
- Turns survived

Use when: You need to track totals for triggers or victory conditions.

## Resource Design Principles

**Meaningful**
Resources should impact gameplay decisions.

Good: ActionPoints (gates which actions are available)
Bad: FavoriteColor (no mechanical impact)

**Measurable**
Resources are positive integers only.

Good: Health 27
Bad: Health "somewhat injured"

**Clear**
Purpose should be unambiguous.

Good: Arrows (ammunition for ranged attacks)
Bad: Stuff (unclear purpose)

## Initialization Patterns

### Fixed Value

```
ActionPoints: 3
```

Resource always starts at 3.

### Dice Roll

```
Health: 1d20
```

Roll d20 for starting value.

### Calculated Value

```
Health: 1d20 + [Constitution]
```

Roll d20, add another resource.

### Complex Formula

```
Health: (1d10 + [Endurance]) * 2
```

Calculate using dice and resources.

### Default (Zero)

If no initialization rule specified, resource starts at 0.

## Resource Maximums

Use Features to define resource caps:

```
Health Maximum (Feature)
Health cannot exceed initial rolled value
If effect would increase Health above maximum, Health stays at maximum
```

Common resources with maximums:
- Health (prevents infinite healing)
- Energy (limits regeneration)
- ActionPoints (caps per turn)

Resources without maximums:
- Gold (accumulates indefinitely)
- Counters (no upper bound)

## Resource Interactions

Resources can:

**Modify expressions**:
```
[Target Health] -= (1d6 + [Strength])
```

**Trigger features**:
```
When [Health] < 5: Apply Bloodied status
```

**Gate actions**:
```
if: [ActionPoints] >= 2
```

**Change through effects**:
```
[Health] -= [Damage Taken]
```

## Designing Resource Economies

### Resource Sources

How do actors gain resources?

- Starting initialization
- Per-turn regeneration
- Action rewards
- Loot and pickups
- Environmental effects

### Resource Sinks

How do actors spend resources?

- Action costs
- Damage and attrition
- Trading and transfers
- Crafting and upgrades

### Balance Check

For each resource, verify:

☐ Clear sources (how gained)
☐ Clear sinks (how spent)
☐ Regeneration rate matches expenditure
☐ Scarcity creates meaningful decisions
☐ Abundance doesn't trivialize challenges

## Common Resource Patterns

### Action Economy

```
ActionPoints (Resource)
Initialize: 3
Regeneration: 3 at start of turn
Maximum: 3
```

Gates number of actions per turn.

### Health Pool

```
Health (Resource)
Initialize: 1d20 + [Constitution]
Maximum: Initial value
Victory/Defeat: Game ends when Health reaches 0
```

Core survival resource.

### Attribute Scores

```
Strength (Resource)
Initialize: 3d6
Usage: Modifies damage calculations
```

Static modifier for expressions.

### Consumables

```
Arrows (Resource)
Initialize: 20
Usage: Required for ranged attacks
Replenish: Loot or purchase
```

Limited-use resource creating scarcity.

## NPC Resource Design

NPCs only need resources that:
1. Drive behavioral decisions
2. Affect action availability
3. Create observable game state

**NPCs typically NEED**:
- Health (defeat condition)
- ActionPoints (if using action economy)

**NPCs typically DON'T NEED**:
- Individual attributes (bake into actions)
- Detailed inventory (unless behavior varies)
- Experience/leveling (no progression)

### Bake Constants into Actions

Instead of:
```
Bandit
Resources: Health 25, ActionPoints 2, Strength 4

Sword Slash
if: Adjacent to target
do: [Target Health] -= (1d6 + [Strength])
then: [ActionPoints] -= 1
```

Use:
```
Bandit
Resources: Health 25, ActionPoints 2

Sword Slash
if: Adjacent to target
do: [Target Health] -= (1d6 + 4)
then: [ActionPoints] -= 1
```

Fewer resources to track, clearer that all Bandits are identical.

## Resource Design Antipatterns

### Antipattern: Redundant Resources

```
Health: 50
HitPoints: 50
LifeForce: 50
```

Problem: Three resources tracking the same thing.

Fix: Use one resource with clear name.

### Antipattern: Static Resources

```
EyeColor: 2
```

Problem: Never changes, no mechanical impact.

Fix: Remove or make it a feature, not a resource.

### Antipattern: Unbounded Growth

```
Strength starts at 3
Every turn: Strength += 1
```

Problem: Exponential power growth breaks balance.

Fix: Add maximum or diminishing returns.

## Resource Design Checklist

When creating a resource, verify:

☐ Clear purpose and usage
☐ Initialization rule defined (or defaults to 0)
☐ Changes during gameplay
☐ Creates meaningful decisions
☐ Doesn't duplicate existing resources
☐ Name is unambiguous
☐ Maximum defined if needed

## Testing Resource Economies

Playtest by tracking:

**Source/Sink Ratio**
Do actors gain resources faster than they spend? Too fast = trivialized challenges. Too slow = frustrating grind.

**Decision Points**
Do resource values create meaningful choices? If always abundant or always scarce, no decisions exist.

**Victory Timing**
Does resource flow support intended campaign length? Adjust regeneration rates if games end too quickly or slowly.
