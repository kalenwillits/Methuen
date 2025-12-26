# Chapter 6: Actions

## 6.1 Overview

Actions are the primary mechanism by which actors interact with the game world. During encounters, actors perform actions to affect other actors, modify resources, change positions, and alter the game state.

## 6.2 Action Definition

### 6.2.1 Formal Definition

An **Action** is a structured operation that:
- Is performed by an actor during their turn
- May target one or more actors, tiles, or areas
- Follows a conditional execution pattern
- Produces effects on the game state

### 6.2.2 Action Properties

| Property | Description | Required |
|----------|-------------|----------|
| Name | Unique identifier for the action | Yes |
| if | Condition to evaluate (the Test) | No (defaults to true) |
| do | Effects when condition is true (On Success) | Yes |
| then | Effects that always execute (Always) | No |
| else | Effects when condition is false (On Failure) | No |

## 6.3 Action Structure

### 6.3.1 The Four Components

Every action has up to four components. The framework uses `if/do/then/else` notation, but you may find it helpful to think of these as:

| Component | Notation | Alternative Name | Purpose |
|-----------|----------|------------------|---------|
| **if** | `if:` | Test / Condition | A Check that determines success or failure |
| **do** | `do:` | On Success | Effects that happen when the test passes |
| **else** | `else:` | On Failure | Effects that happen when the test fails |
| **then** | `then:` | Always | Effects that happen regardless of test result |

**if** (Test)
- A boolean expression (Check) evaluated before the action resolves
- Determines whether `do` or `else` effects apply
- If omitted, the condition is treated as automatically true

**do** (On Success)
- Effects that execute when the `if` condition evaluates to true
- Contains the primary intended outcome of the action

**else** (On Failure)
- Effects that execute when the `if` condition evaluates to false
- Optional component for handling failed attempts

**then** (Always)
- Effects that always execute regardless of condition outcome
- Executes after either `do` or `else`
- Used for costs, cleanup, or universal consequences

### 6.3.2 Execution Order

Actions execute in this precise sequence:

```
1. EVALUATE: Resolve the 'if' condition (the Test)
       |
       +--[TRUE]--> 2a. EXECUTE: Apply 'do' effects (On Success)
       |
       +--[FALSE]-> 2b. EXECUTE: Apply 'else' effects (On Failure)
       |
       v
3. EXECUTE: Apply 'then' effects (Always)
       |
       v
4. COMPLETE: Action resolution finished
```

### 6.3.3 Component Relationships

| Condition Result | do (Success) | else (Failure) | then (Always) |
|------------------|--------------|----------------|---------------|
| TRUE | Executes | Skipped | Executes |
| FALSE | Skipped | Executes | Executes |
| (no condition) | Executes | Skipped | Executes |

### 6.3.4 Important Note on Costs

The `then` component executes regardless of whether the action succeeds or fails. This is intentional: it means you pay the cost of attempting an action even if you miss. This creates meaningful risk when resources are limited.

If a campaign wants an action that only costs resources on success, it should place the cost in the `do` component instead of `then`.

## 6.4 Action Notation

### 6.4.1 Standard Format

Actions are written in the following format:

```
[Action Name]
if: [Condition / Test]
do: [Success Effects]
else: [Failure Effects]
then: [Guaranteed Effects / Always]
```

### 6.4.2 Minimal Format

Actions with no condition and no else:

```
[Action Name]
do: [Effects]
```

## 6.5 Common Action Examples

These examples demonstrate actions as they might appear in play.

### 6.5.1 Strike (Basic Attack)

```
Strike
Range: Melee (adjacent target)
if: 1d20 + [Attack] >= [Target Defense]
do: [Target Health] -= 1d8 + [Strength]
then: [Action Points] -= 1
```

> Sera attacks the Goblin Warrior.
>
> She rolls 1d20 and gets 14. Adding her Attack of 5, the total is 19.
> The Goblin's Defense is 12.
> 19 >= 12? Yes! Hit!
>
> Sera rolls 1d8 for damage and gets 6. Adding her Strength of 4, she deals 10 damage.
> The Goblin's Health drops from 10 to 0. Defeated!
>
> Sera's Action Points decrease from 3 to 2.

### 6.5.2 Defend (Buff Self)

```
Defend
do: [Defense] += 2 until end of turn
then: [Action Points] -= 1
```

> Marcus raises his shield, bracing for attacks.
>
> His Defense increases from 14 to 16 until the end of his turn.
> His Action Points decrease from 2 to 1.

### 6.5.3 Heal (Resource Restoration)

```
Heal
Range: 3 tiles
if: [Target Health] < [Target Health Maximum]
do: [Target Health] += 2d6
then: [Action Points] -= 1
     [Mana] -= 5
```

> Elena casts Heal on the wounded Sera, who is 2 tiles away.
>
> Sera's Health is 8 out of 20 maximum. 8 < 20? Yes, healing can proceed.
>
> Elena rolls 2d6 and gets 9. Sera's Health increases from 8 to 17.
> Elena's Action Points decrease by 1, and her Mana decreases by 5.

### 6.5.4 Shield Bash (Attack with Forced Movement)

```
Shield Bash
Range: Melee
if: 1d20 + [Strength] >= [Target Defense]
do: [Target Health] -= 1d6
    Push target 1 tile away from actor
then: [Action Points] -= 1
else: Actor loses balance; -2 Defense until start of next turn
```

> Sera attempts to Shield Bash the Orc.
>
> She rolls 1d20 and gets 8. Adding Strength 6, total is 14.
> The Orc's Defense is 15. 14 >= 15? No. Miss!
>
> The Shield Bash misses. Sera loses her balance and takes -2 Defense until her next turn starts.
> Her Action Points still decrease from 3 to 2 (the `then` always executes).

### 6.5.5 Dash (Enhanced Movement)

```
Dash
do: This turn, the actor may Move twice without spending additional Action Points
then: [Action Points] -= 1
```

> Finn needs to cross the battlefield quickly.
>
> He uses Dash. For the rest of this turn, his Move actions are free.
> His Action Points decrease from 3 to 2.
> He then uses Move twice (normally 1 AP each, but free due to Dash).

### 6.5.6 Power Shot (High Risk, High Reward)

```
Power Shot
Range: 8 tiles
if: 1d20 + [Attack] - 3 >= [Target Defense]
do: [Target Health] -= 3d8
then: [Action Points] -= 2
else: Ammunition is wasted; [Ammunition] -= 1
```

> Renna takes aim at the distant enemy captain.
>
> She rolls 1d20 and gets 17. Adding Attack 6, subtracting 3 for the difficult shot: 17 + 6 - 3 = 20.
> Target Defense is 14. 20 >= 14? Yes! Hit!
>
> She rolls 3d8 for damage: 5 + 7 + 4 = 16 damage!
> Her Action Points decrease by 2 (from 3 to 1).

## 6.6 Targeting

### 6.6.1 Target Declaration

Most actions require a target to be declared before execution. The target must be:
- A valid actor (active, within range, etc.)
- A valid tile or area
- Allowed by the action's targeting rules

### 6.6.2 Target Keywords

| Keyword | Meaning |
|---------|---------|
| Self | The acting actor |
| Target | The declared target of the action |
| Ally | Any actor in the same cast or allied cast |
| Enemy | Any actor in an opposing cast |
| Adjacent | Any actor on an adjacent tile |
| All | All actors matching criteria |

### 6.6.3 Range Requirements

Actions may specify range requirements:

| Range Type | Description |
|------------|-------------|
| Self | Only the acting actor |
| Melee | Adjacent tiles only (range 1) |
| Ranged X | Up to X tiles distance |
| Unlimited | Any distance |

**Example**:
```
Longbow Shot
Range: 12
if: 1d20 + [Accuracy] >= [Target Defense]
do: [Target Health] -= 1d8
then: [Action Points] -= 1
```

### 6.6.4 Line of Sight

Some actions require line of sight to the target. Line of sight rules:
- Draw a line from the center of the actor's tile to the center of the target's tile
- If the line passes through blocking terrain, line of sight is blocked
- If line of sight is blocked, the action cannot target that actor

Line of sight requirements are specified per action or by campaign Features.

## 6.7 Action Costs

### 6.7.1 Cost in "then" (Standard)

Most action costs belong in the `then` component. This means the cost is paid regardless of success or failure:

```
Strike
if: 1d20 + [Attack] >= [Target Defense]
do: [Target Health] -= 1d8
then: [Action Points] -= 1    <-- Always paid
```

### 6.7.2 Cost in "if" (Prerequisites)

Some actions require resources to even attempt. These belong in the `if` condition:

```
Desperate Strike
if: [Health] <= [Health Maximum] / 2
do: [Target Health] -= 3d10
then: [Action Points] -= 1
```

Here, you must be at half health or below to use this action.

### 6.7.3 Cost in "do" (Success Only)

Some actions only consume resources on success:

```
Steal
if: 1d20 + [Stealth] >= [Target Perception]
do: [Gold] += [Target Gold] / 2
    [Target Gold] -= [Target Gold] / 2
then: [Action Points] -= 1
```

The gold transfer only happens on success.

### 6.7.4 Multiple Cost Types

Actions may have multiple costs:

```
Fireball
Range: 10 tiles, 2-tile radius
if: Targets within radius
do: All targets take 3d6 fire damage
then: [Action Points] -= 2
      [Mana] -= 8
```

## 6.8 Reactions

### 6.8.1 Definition

A **Reaction** is an action that triggers during another actor's turn, interrupting the normal flow of play.

### 6.8.2 Reaction Format

Reactions have an additional trigger condition:

```
Parry (Reaction)
Trigger: An adjacent enemy attacks this actor with a melee attack
if: 1d20 + [Defense] >= [Attacker Attack]
do: Negate the attack's damage
then: [Reaction Points] -= 1
```

### 6.8.3 Reaction Timing

When a reaction triggers, it interrupts the current action:

1. Trigger condition is met during another actor's action
2. Reaction holder chooses whether to use the reaction
3. If used, the reaction resolves completely
4. The original action continues (if still possible)

**Important**: The triggering action has already paid its costs (the `then` component of the original action). The reaction does not prevent cost payment.

### 6.8.4 Example: Attack and Parry

> The Orc attacks Sera with Strike.
>
> **Orc's Strike resolves:**
> - Roll: 1d20 + 5 = 18 vs Sera's Defense 16. Hit!
> - Damage would be: 1d10 + 4 = 11 damage
>
> **Before damage is applied, Sera's Parry triggers:**
> - Trigger: Adjacent enemy attacked with melee. Condition met!
> - Sera chooses to use Parry.
> - Roll: 1d20 + 6 = 19 vs Orc's Attack 5. 19 >= 5? Yes!
> - Effect: The attack's damage is negated.
> - Cost: Sera's Reaction Points decrease by 1.
>
> **Result:** The Orc's Strike hit but dealt no damage. The Orc still paid 1 Action Point. Sera paid 1 Reaction Point.

### 6.8.5 Reaction Limits

Campaigns typically limit reactions:
- Per turn (e.g., 1 reaction per round)
- Per trigger (e.g., only one reaction per attack)
- By resource (e.g., requires Reaction Points)

## 6.9 Action Resolution Procedure

To resolve an action, follow this procedure:

1. **Declare Action**: The actor announces which action they are performing.
2. **Declare Target**: If required, the actor declares the target(s).
3. **Verify Validity**: Confirm the action is valid (actor has the action, target is valid, prerequisite conditions met).
4. **Evaluate Condition**: Resolve the `if` expression if present.
5. **Apply Primary Effects**: Execute `do` (if condition true) or `else` (if condition false).
6. **Resolve Triggered Reactions**: Process any reactions that were triggered.
7. **Apply Guaranteed Effects**: Execute `then` if present.
8. **Complete**: Action resolution is finished.

### 6.9.1 Resolution Example

> **Situation:**
> - Sera (Knight): Attack 5, Strength 4, Action Points 2
> - Goblin Warrior: Defense 12, Health 8
>
> **Action: Strike**
> ```
> if: 1d20 + [Attack] >= [Target Defense]
> do: [Target Health] -= 1d8 + [Strength]
> then: [Action Points] -= 1
> ```
>
> **Resolution:**
> 1. Sera declares Strike action
> 2. Sera declares Goblin as target
> 3. Validity check: Sera has Strike, Goblin is adjacent (valid target)
> 4. Roll 1d20: result 9, plus Attack 5 = 14, compared to Defense 12
>    Condition: 14 >= 12 is TRUE
> 5. Execute do: Roll 1d8: result 5, plus Strength 4 = 9
>    Goblin Health: 8 - 9 = -1, clamped to 0
> 6. No reactions triggered
> 7. Execute then: Sera Action Points: 2 - 1 = 1
> 8. Action complete
>
> **Result:** Goblin reduced to 0 Health (defeated). Sera has 1 Action Point remaining.

## 6.10 Failed Actions

### 6.10.1 Invalid Actions

An action fails to execute if:
- The actor does not have the action
- The target is invalid (out of range, no line of sight, etc.)
- Prerequisites are not met (conditions in `if` that prevent the attempt)
- Required costs cannot be paid

Invalid actions are not performed and no components execute.

### 6.10.2 Failed Conditions

When an action's `if` condition evaluates to false:
- The action is still performed (it was attempted)
- The `else` effects execute (if present)
- The `then` effects execute (costs are paid)
- This is a "failed check" not an invalid action

## 6.11 Simultaneous Actions

### 6.11.1 Resolution Order

When multiple effects would occur simultaneously:
1. Active player resolves their effects first
2. Other effects resolve in initiative order
3. Effects from the same source resolve in listed order

### 6.11.2 State Dependencies

Effects that depend on game state use the state at the moment of resolution, not declaration.

**Example**:
```
If an action reduces Target Health to 0 and another effect
references [Target Health], that reference sees 0.
```
