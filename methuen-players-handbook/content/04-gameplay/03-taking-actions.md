# Taking Actions

## What is an Action?

**Definition**: An **action** is a structured operation an actor can perform, defined by four components: **if**, **do**, **then**, and **else**.

## Action Structure

Every action follows this template:

### if: Condition Check

A boolean expression that determines whether the action's primary effect (do) or alternative effect (else) executes.

- Resource comparisons (`[ActionPoints] >= 2`)
- Range requirements (`Adjacent to target`)
- State checks (`Target is on "forest" tile`)
- Compound conditions (`Adjacent to target AND [ActionPoints] >= 1`)

### do: Primary Effects

Effects that execute **only when the condition is TRUE**.

- Resource modifications (`[Target Health] -= (1d6 + [Strength])`)
- Position changes (`Move 3 spaces North`)
- State changes (`Target becomes "poisoned"`)
- Multiple effects (execute in order listed)

### then: Always-Executed Effects

Effects that **always execute**, regardless of whether the condition was true or false.

- Costs (`[ActionPoints] -= 1`)
- Resource modifications (`[Energy] -= 2`)
- Cleanup effects (`Remove marker from tile`)
- Universal consequences (execute after do or else)

### else: Alternative Effects (Optional)

Effects that execute **only when the condition is FALSE**.

- Partial effects (`[Target Health] -= 1` instead of full damage)
- Alternative outcomes (`Create noise instead of moving`)
- Failure consequences (`Weapon durability decreases`)
- Often omitted if no failure state exists

## Execution Order

Actions execute in this sequence:

1. **Evaluate (if)**: Check if the condition is true or false
2. **Conditional Branch**:
   - If TRUE: Execute (do)
   - If FALSE: Execute (else) if defined
3. **Always Execute**: Execute (then)

**Example Flow**:
```
if: [ActionPoints] >= 2
do: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

If you have 3 ActionPoints:
1. Check: 3 >= 2? TRUE
2. Execute (do): Deal 1d6 damage to target
3. Execute (then): Lose 1 ActionPoint (now have 2)

If you have 1 ActionPoint:
1. Check: 1 >= 2? FALSE
2. Skip (do): No damage dealt
3. Execute (then): Lose 1 ActionPoint (now have 0)

**Note**: The (then) component always executes, making it ideal for costs that must be paid regardless of success.

## Component References

Actions can be written **inline** (all components defined directly) or using **component references** (reusable named components).

### Inline Action

```
Basic Attack (Action)
if: Adjacent to target AND [ActionPoints] >= 1
do: [Target Health] -= (1d6 + [Strength])
then: [ActionPoints] -= 1
```

### Referenced Components

Components can be defined separately and referenced with `#` notation:

```
Adjacent With ActionPoints (Check)
Adjacent to target AND [ActionPoints] >= 1

Deal Basic Damage (Effect)
[Target Health] -= (1d6 + [Strength])

Pay Action Cost (Effect)
[ActionPoints] -= 1

Basic Attack (Action)
if: #Adjacent With ActionPoints
do: #Deal Basic Damage
then: #Pay Action Cost
```

**Benefits of References**:
- Reuse components across multiple actions
- Clearer action definitions
- Easier to maintain and update
- Consistent effects throughout campaign

## Performing an Action

### Step 1: Declare Action and Target

Announce which action you're performing and what/who the target is.

**Example**: "I'm using Basic Attack on the adjacent enemy"

### Step 2: Check Condition (if)

Evaluate the condition in the **if** component:

- Do you meet resource requirements?
- Is the target in range?
- Are state requirements satisfied?

The result (true or false) determines whether (do) or (else) executes next.

### Step 3: Execute Conditional Effect

**If condition is TRUE**: Execute the **do** component
**If condition is FALSE**: Execute the **else** component (if defined)

- Calculate expressions (roll dice, reference resources)
- Modify resources
- Change positions or states

### Step 4: Execute Always-Effect (then)

Apply all effects in the **then** component:

- Pay costs (action points, resources, etc.)
- Apply universal effects
- Execute cleanup operations

The (then) component **always executes** regardless of the condition outcome.

### Step 5: Update Character Sheet

Record all resource changes on your character sheet.

## Example Action Walkthrough

**Action: Power Strike**

```
Power Strike (Action)
if: Adjacent to target AND [ActionPoints] >= 2
do: [Target Health] -= (1d6 + [Strength])
then: [ActionPoints] -= 2
```

**Scenario**: You have 4 ActionPoints and 3 Strength. The target has 15 Health.

**Walkthrough**:

1. **Declare**: "I use Power Strike on the adjacent enemy"

2. **Check Condition**:
   - Adjacent to target? Yes (1 space away)
   - [ActionPoints] >= 2? Yes (I have 4)
   - Condition evaluates to TRUE ✓

3. **Execute (do)** (condition was true):
   - Roll 1d6: result is 4
   - Add [Strength]: 4 + 3 = 7
   - [Target Health] -= 7
   - Target had 15 Health, now has 8

4. **Execute (then)** (always executes):
   - [ActionPoints] -= 2
   - 4 - 2 = 2 ActionPoints remaining

5. **Update Sheet**:
   - ActionPoints: 4 → 2
   - Target Health: 15 → 8

**Alternative Scenario**: You have only 1 ActionPoint.

1. **Check Condition**: [ActionPoints] >= 2? (1 >= 2?) FALSE ✗
2. **Skip (do)**: No damage dealt (condition was false)
3. **Execute (then)**: [ActionPoints] -= 2
   - Attempts to subtract 2 from 1
   - Resources cannot go below 0, so ActionPoints becomes 0
4. **Result**: You paid what you could (lost your remaining AP) but dealt no damage

**Important**: The (then) component always executes, even when the condition fails. This means you can waste resources attempting actions you're not prepared for.

## Example with (else) Component

**Action: Risky Strike**

```
Risky Strike (Action)
if: 1d20 + [Dexterity] > [Target Dexterity] + 10
do: [Target Health] -= 2d6
else: [Health] -= 1d4
then: [ActionPoints] -= 1
```

**Execution**:
1. Roll condition check
2. If you succeed: Deal 2d6 damage to target
3. If you fail: Take 1d4 damage to yourself
4. Always: Pay 1 ActionPoint

## Multiple Targets

Some actions affect multiple actors or tiles. The action definition specifies:

- **Area of Effect**: Shape and size (3-space radius, 5-space line, etc.)
- **Target Selection**: How targets within area are chosen
- **Effect Application**: Whether effects apply to all targets or are divided

**Example**: "All actors within 2 spaces take 1d4 damage"

## Action Timing

### Standard Actions

Performed during your turn's action phase (or whenever, if flexible turn structure).

### Reactions

Special actions performed outside your turn in response to triggers. See **Chapter 5: Reactions**.

### Free Actions

Actions that don't count against action economy, as defined by campaign.

## Common Action Patterns

The following examples are organized by complexity to help you learn the system.

### Beginner Examples

Simple actions with straightforward effects and no else clause.

#### Basic Resource Check

```
Defend (Action)
if: [ActionPoints] >= 1
do: [Defense] += 2
then: [ActionPoints] -= 1
```

Execution: If you have an ActionPoint, gain defense. Always spend the ActionPoint.

#### Simple Movement

```
Move (Action)
if: [MovementPoints] >= 1
do: Move 1 space in chosen direction
then: [MovementPoints] -= 1
```

Execution: If you have movement remaining, move. Always consume a movement point.

### Intermediate Examples

Actions with else clauses, multiple effects, or alternative patterns.

#### Resource Transfer (Cost in Do Pattern)

```
Give Gold (Action)
if: [Gold] >= 5
do: [Gold] -= 5, [Target Gold] += 5
then: (none)
```

Execution: If you have enough gold, transfer it. No cost in (then) because the cost is in (do). This means you only spend gold if you have enough.

> **Note**: The amount transferred (5 in this example) is defined by your campaign. Some campaigns may make this a variable amount chosen by the player.

#### Movement with Cost

```
Sprint (Action)
if: [MovementPoints] >= 3
do: Move 3 spaces in chosen direction
then: [Energy] -= 1
```

Execution: If you have movement, move. Always pay 1 Energy regardless.

#### Conditional Damage with Else Clause

```
Precise Shot (Action)
if: [Target Distance] <= [Accuracy]
do: [Target Health] -= 2d6
else: [Target Health] -= 1d6
then: [Arrows] -= 1, [ActionPoints] -= 1
```

Execution: Hit or miss, you always consume an arrow and action point. Damage varies by accuracy.

#### Action with Failure Consequences

```
Hack Computer (Action)
if: 1d20 + [Intelligence] > [Target Security]
do: Gain access to system
else: Alarm triggers, [Target Security] += 2
then: [ActionPoints] -= 1
```

Execution: Success grants access. Failure increases security. Cost always paid.

### Advanced Examples

Actions using component references and complex patterns.

#### Component Reusability

Define commonly used checks and effects once, reference many times:

```
Has Action Point (Check)
[ActionPoints] >= 1

Pay One Action (Effect)
[ActionPoints] -= 1

Attack (Action)
if: #Has Action Point AND Adjacent to target
do: [Target Health] -= 1d6
then: #Pay One Action

Defend (Action)
if: #Has Action Point
do: [Defense] += 2 until next turn
then: #Pay One Action

Move (Action)
if: #Has Action Point
do: Move 1 space
then: #Pay One Action
```

Three different actions all reuse the same check and cost components.

## Invalid Actions

You cannot perform an action if:

- The action is not available to your actor
- No valid target exists
- Campaign rules prohibit it at this time

**Note**: Even if the (if) condition is false, you can still attempt the action (the else and then components may execute). The condition only determines whether (do) or (else) executes.

---

## See Also

- **Chapter 1**: Quick Start - Introduction to actions
- **Chapter 3**: Core Concepts - Resources and dice notation
- **Chapter 4**: Turn Structure - When actions can be performed
- **Chapter 5**: Reactions - Special trigger-based actions
