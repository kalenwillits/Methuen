# Chapter 4: Resources

## 4.1 Overview

Resources are the fundamental unit of state tracking in Methuen. All measurable quantities in the game, including actor capabilities, currencies, counters, and conditions, are represented as resources.

## 4.2 Resource Definition

### 4.2.1 Formal Definition

A **Resource** is a named integer value that:
- Must always be zero or greater
- Is available to all actors in a campaign
- Persists across turns and encounters unless explicitly modified

### 4.2.2 Resource Properties

| Property | Description |
|----------|-------------|
| Name | Unique identifier for the resource |
| Value | Current integer value (minimum 0) |
| Maximum | Optional upper limit (defined by Features; see Chapter 14) |
| Initialization | Optional rule for determining starting value |

## 4.3 Resource Categories

Resources typically fall into the following categories, though campaigns may define resources for any purpose:

### 4.3.1 Capabilities

Capabilities represent inherent qualities or attributes of an actor.

**Examples**:
- Strength
- Dexterity
- Intelligence
- Constitution
- Wisdom
- Charisma

### 4.3.2 States

States represent current conditions that change during play.

**Examples**:
- Health
- Energy
- Focus
- Morale
- Fatigue

### 4.3.3 Currencies

Currencies represent expendable quantities used for transactions or costs.

**Examples**:
- Gold
- Materials
- Ammunition
- Supplies
- Experience Points

### 4.3.4 Counters

Counters track occurrences, limits, or progression.

**Examples**:
- Action Points
- Turns Survived
- Enemies Defeated
- Distance Traveled

## 4.4 Resource Rules

### 4.4.1 Non-Negative Constraint

Resources cannot have negative values. If any operation would reduce a resource below zero, the resource is set to zero instead.

**Example**:
```
Current Health: 5
Damage taken: 8
Calculation: 5 - 8 = -3
Result: Health = 0 (clamped to minimum)
```

### 4.4.2 Integer Constraint

Resources are always whole numbers. When a calculation produces a fractional result, round down before applying the change.

**Example**:
```
Current Energy: 10
Effect: Restore Energy equal to [Wisdom] / 2
Wisdom: 7
Calculation: 7 / 2 = 3.5 -> 3 (rounded down)
Result: Energy = 10 + 3 = 13
```

### 4.4.3 Universal Access

All actors have implicit access to all resources defined in the campaign. An actor need not explicitly declare which resources they use. Resources are tracked only when their values become relevant.

### 4.4.4 Default Value

Unless otherwise specified by the campaign, all resources default to a value of 0.

## 4.5 Resource Initialization

### 4.5.1 Lazy Initialization

Resources use lazy initialization. A resource value is not determined until it is first referenced or modified. This approach:

- Reduces bookkeeping for unused resources
- Allows dynamic initialization based on game state
- Enables flexible actor design

### 4.5.2 Initialization Procedure

When an actor's resource is first accessed:

1. **Check for initialization rule**: Consult the campaign for a resource initialization rule.
2. **Apply initialization**: If a rule exists, execute it to determine the starting value.
3. **Use default**: If no rule exists, set the resource to 0.
4. **Record the value**: Track the resource value for the actor going forward.

### 4.5.3 Initialization Examples

**Example 1**: Campaign-defined initialization
```
Campaign Rule:
  Health initialization: 1d20 + [Constitution]

First access to actor's Health:
  Roll 1d20: 15
  Constitution: 12
  Calculation: 15 + 12 = 27
  Result: Health = 27 (recorded)
```

**Example 2**: No initialization rule
```
Campaign has no initialization rule for Gold.

First access to actor's Gold:
  Result: Gold = 0 (default)
```

**Example 3**: Derived initialization
```
Campaign Rule:
  Action Points initialization: 3

First access to actor's Action Points:
  Result: Action Points = 3 (as specified)
```

### 4.5.4 Unknown Resources

A resource that has never been accessed is considered "unknown" for that actor. Unknown resources have no recorded value until initialization occurs. Once initialized, the resource value is tracked normally.

## 4.6 Resource Maximums

### 4.6.1 Optional Constraints

Campaigns may define maximum values for resources using Features (see Chapter 14). When a maximum is defined, the resource cannot exceed that value.

### 4.6.2 Maximum Enforcement

If an operation would increase a resource above its maximum, the resource is set to its maximum instead.

**Example**:
```
Current Health: 25
Maximum Health: 27
Healing received: 10
Calculation: 25 + 10 = 35
Result: Health = 27 (clamped to maximum)
```

### 4.6.3 Common Maximum Features

**Static Maximum**:
```
Health Maximum
Health cannot exceed 100.
```

**Dynamic Maximum**:
```
Health Maximum
Health cannot exceed its initial rolled value.
```

**Derived Maximum**:
```
Energy Maximum
Energy cannot exceed [Constitution] * 2.
```

### 4.6.4 Maximum Modification

Maximums may change during play if the Feature defining them references dynamic values. When a maximum decreases below the current resource value, the resource is immediately reduced to the new maximum.

**Example**:
```
Feature: Energy Maximum equals [Constitution] * 2

Current state:
  Constitution: 10
  Energy Maximum: 20
  Current Energy: 18

Constitution reduced by 3:
  New Constitution: 7
  New Energy Maximum: 14
  Current Energy: 18 (exceeds new maximum)
  Result: Energy reduced to 14
```

## 4.7 Resource Modification

### 4.7.1 Modification Operations

Resources are modified through the following operations:

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Set | `[Resource] = X` | Set resource to value X |
| Add | `[Resource] += X` | Increase resource by X |
| Subtract | `[Resource] -= X` | Decrease resource by X |
| Multiply | `[Resource] *= X` | Multiply resource by X |
| Divide | `[Resource] /= X` | Divide resource by X |

### 4.7.2 Modification Procedure

1. **Evaluate the expression**: Calculate the value to be applied.
2. **Apply the operation**: Perform the mathematical operation.
3. **Round if necessary**: Round down any fractional result.
4. **Enforce minimum**: If result is negative, set to 0.
5. **Enforce maximum**: If maximum exists and result exceeds it, set to maximum.
6. **Record new value**: Update the tracked resource value.

### 4.7.3 Modification Examples

**Example 1**: Addition with maximum
```
Operation: [Health] += 10
Current Health: 22
Maximum Health: 25
Calculation: 22 + 10 = 32
After maximum enforcement: 25
Result: Health = 25
```

**Example 2**: Subtraction to zero
```
Operation: [Energy] -= 15
Current Energy: 8
Calculation: 8 - 15 = -7
After minimum enforcement: 0
Result: Energy = 0
```

**Example 3**: Division with rounding
```
Operation: [Gold] /= 3
Current Gold: 50
Calculation: 50 / 3 = 16.666...
After rounding: 16
Result: Gold = 16
```

## 4.8 Resource Scope

### 4.8.1 Actor Resources

Most resources are scoped to individual actors. Each actor maintains their own values for each resource.

### 4.8.2 Shared Resources

Campaigns may define shared resources that are tracked at the campaign or encounter level rather than per-actor. Shared resources are accessed using special syntax defined by the campaign.

**Example**:
```
Campaign Resource: Party Gold
All actors in the player cast share a single Gold value.
```

### 4.8.3 Temporary Resources

Some resources may be scoped to a single encounter or turn. These temporary resources are discarded when their scope ends.

**Example**:
```
Encounter Resource: Alarm Level
Tracked at the encounter level.
Reset to 0 when the encounter ends.
```

## 4.9 Resource Visibility

### 4.9.1 Known Values

By default, all actor resource values are known to all players. Players may inspect resource values to inform decisions.

### 4.9.2 Hidden Resources

Campaigns may specify that certain resources are hidden from some or all players. Hidden resource values are tracked but not revealed until specific conditions are met.

**Example**:
```
Feature: Hidden Morale
Non-player actor Morale values are hidden from players
until a Check reveals them.
```

## 4.10 Default Mechanics

This section defines default behaviors that apply when campaigns do not specify alternatives. These defaults ensure the game is playable without extensive campaign-specific rules.

### 4.10.1 Action Points Default

Unless a campaign specifies otherwise:

```
Default Feature: Action Points
All actors have an Action Points resource.
At the start of each actor's turn, Action Points resets to 3.
Most actions cost 1 Action Point.
```

This provides the standard action economy: three actions per turn.

### 4.10.2 Defeat Default

Unless a campaign specifies otherwise:

```
Default Feature: Defeat at Zero Health
When an actor's Health resource reaches 0, that actor is defeated.
A defeated actor:
- Is removed from the map
- No longer takes turns
- Cannot be targeted by actions
- Does not block movement or line of sight
```

This is the standard defeat condition. Campaigns may override with Features that provide alternative outcomes (unconsciousness, death saves, etc.).

### 4.10.3 Common Resource Defaults

| Resource | Default Initialization | Common Maximum |
|----------|----------------------|----------------|
| Health | Campaign-defined | Initial value |
| Action Points | 3 | 5 |
| Mana | 0 | Campaign-defined |
| Gold | 0 | None |

### 4.10.4 Resource Refresh Timing

By default, resources that refresh do so at the start of the actor's turn, before any start-of-turn effects. This ordering is:

1. Resource refresh (Action Points reset)
2. Start-of-turn features trigger
3. Duration effects that expire "at start of turn" end
4. Actor may take actions

Campaigns may specify different refresh timing through Features.

## 4.11 Example: Character Resource Tracking

This example shows how resources might be tracked for a player actor.

```
Actor: Kira the Fighter
----------------------------------
CAPABILITIES
  Strength:     6
  Dexterity:    4
  Constitution: 5
  Intelligence: 2
  Wisdom:       3

STATES
  Health:       18 / 20 (Maximum)

COUNTERS
  Action Points: 3 / 3 (resets each turn)

CURRENCIES
  Gold:         45
  Experience:   250
----------------------------------
```

During play, update these values as actions are taken and effects resolve. Many players find it helpful to use a character sheet layout like this.

## 4.12 Rule Book Precedence

When there is a discrepancy between a campaign's Feature and the rules in this chapter, this Rule Book is the superseding document. Campaigns may extend but not contradict the core resource rules.
