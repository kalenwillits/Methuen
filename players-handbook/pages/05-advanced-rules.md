# Advanced Rules

## Features

A **Feature** is a passive rule that describes how game elements behave or interact.

Features modify core mechanics, define special behaviors, or establish constraints.

### Feature Examples

**Initiative**:
```
Initiative Roll
Roll 1d20 + Dexterity at start of encounter
Highest result goes first
```

**Resource Maximum**:
```
Health Maximum
Health cannot exceed initial rolled value
If effect would increase Health above maximum, Health stays at maximum
```

**Movement**:
```
Standard Movement
All actors move up to 6 spaces per turn
```

**Victory Condition**:
```
Survival Victory
Game ends when all player actors reach 0 Health
Actors with Health > 0 at game end are victorious
```

**Turn Structure**:
```
Flexible Turns
Actors may move and act in any order during their turn
```

### How Features Work

Features are defined in your campaign book. They modify or clarify core rules.

When a Feature contradicts a core rule, the Feature takes precedence.

**Example**: Core rule says resources start at 0. A Feature says "ActionPoints start at 3". The Feature overrides the core rule.

## Reactions

A **Reaction** is an action performed outside your normal turn in response to a trigger.

Reactions are defined by your campaign. Common patterns:

### Trigger-Based Reactions

```
Counter Strike (Reaction)
Trigger: When adjacent enemy attacks you
if: [ActionPoints] >= 1
do: [Attacker Health] -= 1d4
then: [ActionPoints] -= 1
```

When the trigger occurs:
1. Announce: "I use Counter Strike"
2. Check condition
3. Execute the reaction
4. Continue with triggering action

### Interrupt Reactions

Some reactions interrupt the triggering action:

```
Dodge (Reaction)
Trigger: When targeted by attack
if: [Energy] >= 2
do: Attack misses
then: [Energy] -= 2
```

Check your campaign for reaction timing rules.

## Multiple Targets

Some actions affect multiple actors or areas.

### Area Effects

**Radius**:
```
Fireball
Range: 10 spaces
Area: 3-space radius
All actors in area: [Target Health] -= 2d6
```

**Line**:
```
Lightning Bolt
Range: Self
Area: 5-space line in chosen direction
All actors in line: [Target Health] -= 1d8
```

**Cone**:
```
Flame Breath
Range: Self
Area: 3-space cone in facing direction
All actors in cone: [Target Health] -= 1d6
```

### Effect Distribution

**Divided**: Total effect split among targets
**Full**: Each target receives full effect (more common)

Your campaign specifies distribution method.

## Resource Limits and Edge Cases

### Resource Floor

Resources cannot drop below 0.

**Example**: You have 2 Health. You take 5 damage. Health becomes 0, not -3.

### Resource Operations

**Addition**: `[Health] += 5` increases Health by 5
**Subtraction**: `[Health] -= 5` decreases Health by 5
**Set**: `[Health] = 10` sets Health to exactly 10
**Compare**: `[Health] >= 10` checks if Health is 10 or more

### Division Results

Division rounds down to nearest integer.

**Example**: `7/2 = 3`

### Zero Division

Dividing by zero equals zero.

**Example**: `10/0 = 0`

This prevents errors in complex expressions.

### Negative Expression Results

Final expression results cannot be negative. Intermediate values can be negative.

**Example**: `5 - 8 = 0` (final result)
**Example**: `(5 - 8) + 10 = 7` (intermediate -3 becomes 7 after adding 10)

## Component References

Actions can reuse components with `#` notation.

### Defining Components

**Checks**:
```
Has ActionPoint (Check)
[ActionPoints] >= 1
```

**Effects**:
```
Pay ActionPoint (Effect)
[ActionPoints] -= 1
```

### Referencing Components

```
Attack
if: #Has ActionPoint AND Adjacent to target
do: [Target Health] -= 1d6
then: #Pay ActionPoint

Defend
if: #Has ActionPoint
do: [Defense] += 2
then: #Pay ActionPoint
```

### Benefits

- Consistency across actions
- Easier campaign maintenance
- Clearer action definitions
- Reduced redundancy

## Special Action Patterns

### Free Actions

Actions that don't cost resources or count against action economy.

```
Look Around (Free Action)
if: true
do: Gain information about adjacent tiles
```

Campaign defines which actions are free.

### Chained Actions

Actions that trigger other actions.

```
Execute and Advance
if: [ActionPoints] >= 2
do: Perform Basic Attack, then Move 2 spaces
then: [ActionPoints] -= 2
```

### Conditional Costs

Costs that vary based on circumstances.

```
Variable Movement
if: [MovementPoints] >= [Terrain Cost]
do: Move 1 space
then: [MovementPoints] -= [Terrain Cost]
```

Terrain Cost might be 1 for plains, 2 for forest, etc.

## Non-Player Actors

Campaigns define behaviors for NPCs and enemies.

### Behaviors

**Behaviors** are decision rules that determine NPC actions.

```
Aggressive Behavior
Check: [Target Health] < [Health]
Action: Attack weakest adjacent target
```

```
Defensive Behavior
Check: [Health] <= 5
Action: Retreat to nearest cover
```

### Strategies

**Strategies** combine multiple behaviors with priority.

```
Goblin Strategy
1. If [Health] <= 3: Retreat
2. If adjacent to player: Attack
3. Otherwise: Move toward nearest player
```

NPCs execute the first behavior whose check passes.

## Advanced Movement

### Terrain Costs

Different terrain types cost different movement points.

**Example**:
- Plains: 1 point
- Forest: 2 points
- Mountains: 3 points

Campaign defines terrain costs.

### Diagonal Movement

Campaigns may make diagonal movement cost more.

**Common pattern**: Diagonals cost 1.5× cardinal movement (rounded up)

### Difficult Terrain

Some terrain prevents or restricts movement.

**Example**: Water tiles require swimming ability

Campaign defines terrain restrictions.

## Status Effects

Status effects are conditions that modify actor behavior.

**Common patterns**:

```
Poisoned
At start of turn: [Health] -= 1
Duration: 3 turns
```

```
Burning
At end of turn: [Health] -= 1d4
Duration: Until extinguished
```

```
Stunned
Cannot perform actions
Duration: 1 turn
```

Campaign defines available status effects and their mechanics.

## Facing and Direction

Heading determines:
- Which direction you face
- Front/back/side positioning for attacks
- Cone/line effect direction

**Changing heading**: Campaign defines if this costs resources or is free.

**Directional modifiers**:
```
Backstab
if: Behind target AND [ActionPoints] >= 1
do: [Target Health] -= 2d6
then: [ActionPoints] -= 1
```

Front attacks might deal normal damage, back attacks deal more.

## Casts and Groups

Some campaigns use **casts**—groups of actors sharing initiative and turn.

```
Party Cast
Members: All player actors
Initiative: Highest member's initiative
Turn: Members act in any order
```

Benefits:
- Coordinated actions
- Shared resources
- Tactical flexibility

Campaign defines cast mechanics.

## Campaign-Specific Rules

Always check your campaign for:

- Victory and defeat conditions
- Initiative system
- Movement rules
- Turn structure
- Available actions
- Resource initialization
- Special mechanics
- Status effects
- Terrain types

When campaign rules conflict with core rules, campaign rules take precedence.
