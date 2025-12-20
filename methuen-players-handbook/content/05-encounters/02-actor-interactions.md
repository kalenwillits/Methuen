# Actor Interactions

## Interaction Resolution

When actors interact through actions, the framework provides structure, but campaigns define the specific resolution method.

## Resolution Methods

Campaigns typically use one of these approaches:

### Direct Resolution

The expression calculates a result that is directly applied:

```
Action: Harvest Crop
then: [Food] += (1d6+[Target CropGrowth])
```

The above is an example of an in-line effect. However, it's perfectly acceptable as a campaign grows to reference another action or effect that has its own definition:
```
Effect: Increase Food
[Food] += (1d6+[Target CropGrowth])
```
```
Action: Harvest Crop
then: #Increase Food
```



- Roll dice and calculate
- Apply result immediately
- No success/failure check

### Success Check Resolution

The expression is compared against a threshold:

```
Action: Persuade
if: (1d20+[charisma]) > [target will]
then: `target follows command`
else: `target refuses`
```

- Calculate result
- Compare to target value
- Apply appropriate outcome

### Contested Resolution

Both actors calculate expressions, highest wins:

```
Action: Arm Wrestle
Self rolls: 1d20+[Strength]
Target rolls: 1d20+[Target Strength]
Higher result wins
```

- Both sides calculate
- Compare results
- Resolve based on winner

**Note**: Your campaign defines which method is used for which actions.

## Damage and Resource Reduction

### Applying Resource Changes

When an action reduces a target's resource:

1. Calculate the expression result
2. Subtract from target's current resource value
3. Resource cannot go below zero (floor at 0)

**Example**:
```
Action deals 8 damage
Target has 5 health
5 - 8 = 0 (not -3)
Target now has 0 health
```

### Resistance and Mitigation

Some campaigns include damage reduction:

**Armor-Style Reduction**:
```
Damage dealt: 10
Target armor: 4
Final damage: 10 - 4 = 6
```

**Percentage Reduction**:
```
Damage dealt: 10
Target has "50% reduction" feature
Final damage: 10 / 2 = 5
```
### Individual Resolution

Calculate separately for each target:

```
Area Spell: Deal 1d6 damage to all actors in 3-space radius
Actor A: Rolled 4, takes 4 damage
Actor B: Rolled 2, takes 2 damage
Actor C: Rolled 6, takes 6 damage
```

### Shared Resolution

Calculate once, apply to all:

```
Explosion: All actors in radius take 8 damage
All affected actors lose 8 health
```

### Divided Resolution

Total is split among targets:

```
Distribute 12 food among targets
3 targets: Each gets 4 food
```

## Forced Movement

Actions that move other actors:

### Push/Pull

```
Effect: Move target 3 spaces directly away (push) or toward (pull) self
```

- Calculate direction based on relative positions
- Move target the specified distance
- If path is blocked, move as far as possible

### Teleport

```
Effect: Move target to specific coordinates or tile type
```

- Instant relocation
- No path required
- May have conditions (e.g., must be empty tile)

### Reposition

```
Effect: Swap positions with target
```

- Both actors exchange locations
- Simultaneous movement

## Status Effects and Conditions

Some campaigns include lasting effects:

### Temporary Modifiers

"Target has -2 to all rolls for 3 turns"

- Track duration using a resource!
- Apply modifier to relevant calculations
- Remove when expired

### State Changes

"Target is Frozen: cannot move"

- Binary on/off state
- Prevents certain actions
- Removed by condition or duration

### Ongoing Damage

"Target takes 2 damage at start of each turn for 4 turns"

- Automatic damage trigger
- Track remaining duration
- Resolve at specified time

**Note**: Your campaign defines which effects exist and how they're tracked.

## Chain Reactions

When one effect triggers another:

**Example**:
```
Action reduces [Target Health] to 0
→ Triggers "on death" effect
→ Explodes, dealing damage to adjacent actors
→ May trigger their "on damage" effects
```

Resolve chains in the order they occur, completing each before moving to the next.

## Interaction with Environment

Actions can target tiles or environmental features:

### Tile Modification

```
Action: Build Wall
then: Target tile type becomes "wall", blocks movement
```

### Resource Extraction

```
Action: Mine Ore
then: [Ore] += [Target OreDeposit], [Target OreDeposit] becomes 0
```

### Environmental Triggers

```
Action: Light Fire
then: Target tile and all adjacent tiles become "burning",
      actors on burning tiles take 1d4 damage each turn
```
