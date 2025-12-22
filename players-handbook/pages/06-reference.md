# Reference

## Quick Reference Card

### Turn Structure

**CHECK** → **ACT** → **MOVE** → **END**

1. Resolve start-of-turn effects
2. Perform actions
3. Move (if allowed)
4. Resolve end-of-turn effects

### Action Structure

```
if: Condition (true/false)
do: Execute when TRUE
then: ALWAYS execute
else: Execute when FALSE
```

**Execution order**: (if) → [do or else] → (then)

### Dice Notation

- `XdY` = Roll X dice with Y sides
- `1d6` = Roll one six-sided die
- `2d10` = Roll two ten-sided dice, add them
- `d20` = Same as `1d20`

### Operators

- `+` Addition
- `-` Subtraction
- `*` Multiplication
- `/` Division (rounds down)

### Resource Notation

- `[Resource]` = Your resource value
- `[Target Resource]` = Target's resource value
- `[Health] >= 10` = Comparison
- `[Health] -= 5` = Modification

### Directions

**Cardinals**: N, E, S, W
**Diagonals**: NE, SE, SW, NW

### Resource Rules

- Always ≥ 0 (never negative)
- Whole numbers only (no fractions)
- Default start value: 0
- All actors have all resources

### Special Math Rules

- Division by zero = 0
- Negative results = 0
- Fractions round down

### Common Terms

**Adjacent**: 1 space away (any direction)
**Range**: Distance in spaces
**Component Reference**: `#Name` (reusable check/effect)

## Turn Checklist

Use this checklist during play:

### Pre-Game

☐ Read victory condition
☐ Set up map
☐ Create actors
☐ Determine initiative
☐ Prepare materials (dice, sheets, campaign book)

### Each Turn

☐ **CHECK**: Resolve start-of-turn effects
☐ **ACT**: Perform actions
  - Declare action and target
  - Check (if) condition
  - Execute (do) or (else)
  - Execute (then)
  - Update character sheet
☐ **MOVE**: Move actor (if allowed)
☐ **END**: Resolve end-of-turn effects

### Each Action

☐ Declare action name and target
☐ Check (if) condition (true/false?)
☐ If TRUE: Execute (do)
☐ If FALSE: Execute (else) if it exists
☐ Always: Execute (then)
☐ Update character sheet immediately

### End of Round

☐ All actors have acted
☐ Start new round with highest initiative

## Glossary

**Action**
Structured operation with if/do/then/else components. Execution order: (if) → [do or else] → (then)

**Actor**
Named entity with location, heading, resources, and actions. Can be player-controlled or NPC.

**Adjacent**
One space away in any direction (cardinal or diagonal).

**Behavior**
Decision rule for non-player actors. Defines conditions and resulting actions.

**Campaign**
Collection of content (resources, actions, maps, features) adhering to Methuen framework.

**Cardinal Directions**
N, E, S, W (four main compass directions).

**Cast**
Group of actors sharing initiative and turn.

**Check**
Boolean condition that evaluates to true or false. Can be inline or referenced with #.

**Component Reference**
Reusable check or effect referenced with `#Name` notation.

**Diagonal Directions**
NE, SE, SW, NW (four corner directions).

**Effect**
Active change to game state (resource modification, position change, etc.). Can be inline or referenced with #.

**Expression**
Mathematical formula combining dice, resources, and operators to calculate a result.

**Feature**
Passive rule describing how game elements behave or interact. Can override core rules.

**Heading**
Direction an actor faces (N, NE, E, SE, S, SW, W, NW).

**Initiative**
Value determining turn order. Higher initiative acts first.

**Location**
Actor's position on map using coordinate notation (e.g., 3N 2E).

**Map**
Grid of tiles containing spatial information and terrain.

**Range**
Distance between actors or from actor to target, measured in spaces.

**Reaction**
Action performed outside normal turn in response to trigger.

**Resource**
Named value (positive integer ≥ 0) tracking actor capabilities, states, currencies, or counters.

**Round**
One full cycle where all actors take their turns in initiative order.

**Strategy**
Collection of behaviors with priority order for non-player actors.

**Target**
Actor or location affected by an action.

**Terrain**
Tile type that may affect movement costs or provide special properties.

**Tile**
Single grid coordinate on map with properties (terrain type, contents, etc.).

## Common Action Patterns

### Basic Attack

```
Basic Attack
Range: Adjacent
if: [ActionPoints] >= 1
do: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

Simple damage with resource cost.

### Defend

```
Defend
if: [ActionPoints] >= 1
do: [Defense] += 2
then: [ActionPoints] -= 1
```

Trade action for defense boost.

### Move

```
Move
if: [MovementPoints] >= 1
do: Move 1 space in chosen direction
then: [MovementPoints] -= 1
```

Standard movement pattern.

### Conditional Attack

```
Precise Shot
if: [Target Distance] <= [Accuracy]
do: [Target Health] -= 2d6
else: [Target Health] -= 1d6
then: [Arrows] -= 1, [ActionPoints] -= 1
```

Damage varies by condition. Resources always spent.

### Resource Transfer

```
Give Gold
if: [Gold] >= 5
do: [Gold] -= 5, [Target Gold] += 5
```

Transfer only if you have enough. No cost if condition fails (no then component).

### Risky Action

```
Risky Strike
if: 1d20 + [Dexterity] > [Target Defense]
do: [Target Health] -= 2d6
else: [Health] -= 1d4
then: [ActionPoints] -= 1
```

Success deals damage to target, failure damages self. Always costs ActionPoint.

## Expression Examples

### Simple Roll

```
1d20
```

Roll one twenty-sided die.

### Modified Roll

```
1d20 + [Dexterity]
```

Roll d20, add your Dexterity value.

### Damage Calculation

```
1d6 + [Strength]
```

Roll d6, add Strength for damage amount.

### Complex Calculation

```
(1d6 + [Strength]) - ([Target Armor] / 2)
```

Roll d6, add Strength, subtract half of target's Armor (rounded down).

### Contested Check

```
1d20 + [Attack] > [Target Defense]
```

Roll d20, add Attack, compare to target's Defense. Result is true or false.

## Initialization Examples

### Fixed Value

```
ActionPoints: 3
```

ActionPoints always start at 3.

### Dice Roll

```
Health: 1d20
```

Roll d20 for starting Health.

### Calculated Value

```
Health: 1d20 + [Constitution]
```

Roll d20, add Constitution resource for starting Health.

### Complex Formula

```
Health: (1d10 + [Endurance]) * 2
```

Roll d10, add Endurance, multiply by 2.

## Movement Reference

### Standard Costs

**Cardinal** (N, E, S, W): 1 point per space
**Diagonal** (NE, SE, SW, NW): 1.5 points per space (rounded up)

### Position Notation

**Origin**: 0N 0E
**North**: 3N 0E (3 spaces north of origin)
**East**: 0N 3E (3 spaces east of origin)
**Northeast**: 2N 2E (2 north, 2 east)

### Distance Calculation

Count spaces between actors using shortest path.

**Adjacent**: 1 space
**Nearby**: 2-3 spaces
**Distant**: 4+ spaces

Campaign defines range categories.

## Status Effect Reference

Common status effects (campaign-defined):

**Poisoned**
Periodic damage over time.

**Burning**
Damage at end of turn until extinguished.

**Stunned**
Cannot perform actions for duration.

**Slowed**
Reduced movement.

**Boosted**
Increased resource or capability.

Check your campaign book for specific effects and mechanics.

## Component Reference Examples

### Defining Components

```
Has ActionPoint (Check)
[ActionPoints] >= 1

Pay ActionPoint (Effect)
[ActionPoints] -= 1

Adjacent to Target (Check)
Adjacent to target
```

### Using Components

```
Attack
if: #Has ActionPoint AND #Adjacent to Target
do: [Target Health] -= 1d6
then: #Pay ActionPoint

Defend
if: #Has ActionPoint
do: [Defense] += 2
then: #Pay ActionPoint
```

Benefits: Consistency, clarity, maintainability.

## Campaign Checklist

When starting a new campaign, verify you understand:

☐ Victory condition
☐ Defeat condition
☐ Initiative system
☐ Turn structure
☐ Movement rules
☐ Available actions
☐ Resource list and initialization
☐ Special features
☐ Status effects
☐ Terrain types
☐ Map layout

## Tips and Reminders

### Always Remember

- The (then) component ALWAYS executes
- Resources cannot go below 0
- Resources are whole numbers only
- Update your sheet immediately after changes
- Campaign rules override core rules

### Easy to Forget

- Diagonal movement often costs more
- (then) executes even when (if) fails
- Resources initialize on first use if not pre-initialized
- Division results round down
- Zero division equals zero (not an error)

### Common Mistakes

- Forgetting to execute (then) component
- Not initializing resources when first referenced
- Allowing resources to go negative
- Not checking campaign-specific features
- Executing actions without valid targets

## Where to Look

**Core mechanics**: Chapters 2-3
**Turn structure**: Chapter 3
**Setup and character creation**: Chapter 4
**Advanced rules**: Chapter 5
**Quick reference**: This chapter
**Campaign-specific rules**: Your campaign book
