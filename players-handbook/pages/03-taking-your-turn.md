# Taking Your Turn

## Turn Structure

Use this sequence each turn:

**START** → Resolve start-of-turn features.
**ACT** → Select and perform as few or as many actions as desired. 
**END** → Resolve end-of-turn features.

## Initiative
Turn order is be defined by a *global feature* in the campaign book.
This is called the *initiative feature*. Without it, a campaign defaults to
this initiative feature:
```
Default Initiative
When an actor or cast is first deployed to a map, roll 1d100. Turn order is in
decending order. Ties are resolved by the two tied actors or casts rolling
1d100 placing the higher rolling actor or cast in the turn before the lower
rolling actor or cast.
```

## Performing Actions

### Action Structure

Every action has four components:

**if**: Condition check (true or false)
**do**: Effects when condition is TRUE
**then**: Effects that ALWAYS execute
**else**: Effects when condition is FALSE (optional)

**Execution order**: Evaluate (if) → Execute (do or else) → Execute (then)

### Simple Example

```
Basic Attack
Range: Adjacent
Target: Single actor

if: [Action Points] >= 1
do: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

**How it works**:
1. Check: Do you have 1 or more ActionPoints?
2. If yes: Deal 1d6 damage to target (do)
3. Always: Subtract 1 ActionPoint (then)

**Important**: The (then) component always executes, even if the condition fails.

### Performing an Action: Step by Step

**1. Declare**
Announce the action and target.
*"I use Basic Attack on the adjacent Goblin"*

**2. Check Condition**
Evaluate the (if) component.
*ActionPoints >= 1? Yes, I have 3*

**3. Execute Effect**
- If condition is TRUE: Execute (do)
- If condition is FALSE: Execute (else) if it exists

*Condition is true, so roll 1d6 for damage. Result: 5*

**4. Always Execute**
Execute (then) component.
*Subtract 1 ActionPoint. 3 - 1 = 2*

**5. Update Sheet**
Record all changes.
*ActionPoints: 3 → 2*

### Complete Turn Example

**Setup**:
- Your actor: Raven at 0N 0E
- Enemy: Goblin at 1N 0E
- Your ActionPoints: 3
- Your Strength: 4
- Goblin Health: 12

**Your Turn**:

1. **CHECK**: Initiative determined—you go first
2. **ACT**: Use Basic Attack on Goblin
   - Declare: "Basic Attack on Goblin"
   - Check: Adjacent? Yes. ActionPoints >= 1? Yes
   - Execute (do): Roll 1d6, get 5. Deal 5 damage. Goblin Health: 12 → 7
   - Execute (then): ActionPoints: 3 → 2
3. **MOVE**: (If your campaign allows movement)
4. **END**: No end-of-turn effects. Pass turn.

## Action Components Explained

### if: Condition Checks

Conditions evaluate to true or false.

**Resource comparisons**:
- `[ActionPoints] >= 2`
- `[Health] > 0`

**Range requirements**:
- `Adjacent to target`
- `Within 5 spaces of target`

**Compound conditions**:
- `Adjacent to target AND [ActionPoints] >= 1`
- `[Health] <= 10 OR [Energy] > 5`

### do: Primary Effects

Execute only when condition is TRUE.

**Resource modifications**:
- `[Target Health] -= 1d6`
- `[Defense] += 2`

**Position changes**:
- `Move 3 spaces North`
- `Swap positions with target`

**State changes**:
- `Target becomes poisoned`
- `Remove burning status`

### then: Always-Executed Effects

Execute regardless of condition outcome.

**Resource costs**:
- `[ActionPoints] -= 1`
- `[Arrows] -= 1`

**Counters**:
- `[AttacksMade] += 1`

**Universal consequences**:
- `[Energy] -= 1`

### else: Alternative Effects

Execute only when condition is FALSE. Optional component.

**Partial effects**:
```
if: 1d20 + [Accuracy] > [Target Defense]
do: [Target Health] -= 2d6
else: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

Hit or miss, you always spend the ActionPoint. Damage varies.

## Action Patterns

### Pattern: Resource Check

```
Defend
if: [ActionPoints] >= 1
do: [Defense] += 2
then: [ActionPoints] -= 1
```

Spend ActionPoint to gain Defense.

### Pattern: Resource Transfer

```
Give Gold
if: [Gold] >= 5
do: [Gold] -= 5, [Target Gold] += 5
```

Transfer only if you have enough. No (then) component means no cost if you lack gold.

### Pattern: Movement

```
Move
if: [MovementPoints] >= 1
do: Move 1 space in chosen direction
then: [MovementPoints] -= 1
```

Move if you have movement remaining.

### Pattern: Conditional Damage

```
Precise Shot
if: [Target Distance] <= [Accuracy]
do: [Target Health] -= 2d6
else: [Target Health] -= 1d6
then: [Arrows] -= 1, [ActionPoints] -= 1
```

Hit for more damage if within accuracy range. Always consume arrow and ActionPoint.

## Component References

Actions can reference reusable components with `#` notation.

**Define once**:
```
Has ActionPoint (Check)
[ActionPoints] >= 1

Pay ActionPoint (Effect)
[ActionPoints] -= 1
```

**Reference many times**:
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

## Movement

Movement rules are defined by your campaign through Features.

**Common movement patterns**:

```
Standard Movement
Move up to 6 spaces per turn
```

```
Resource-Based Movement
Move up to [Speed] spaces per turn
```

```
ActionPoint Movement
Spend 1 ActionPoint per space moved
```
