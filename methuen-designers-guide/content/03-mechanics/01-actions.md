# Actions - Design Guide

## Designing Actions

Actions are the core of actor capabilities. Well-designed actions create meaningful decisions and strategic depth.

## Action Structure (Designer Perspective)

### if: Condition Design

**Purpose**: Determine which effect branch executes (do or else)

**Execution**: Boolean expression that evaluates to true or false

**Good Conditions**:
- Resource checks: `[ActionPoints] >= 2`
- Range checks: `Adjacent to target`
- State checks: `[Target Health] > 0`
- Tile checks: `Target on "forest" tile`
- Opposed rolls: `1d20 + [Dexterity] > [Target Dexterity] + 10`

**Avoid**:
- Ambiguous conditions: `if reasonable`
- Undefined terms: `if target is weak`
- Multiple unrelated checks without logical operators

**Design Principle**: The condition should represent a meaningful game state or challenge. True/false determines which gameplay branch occurs.

### do: Primary Effect Design

**Purpose**: Effects that execute ONLY when condition is TRUE

**When to Use**:
- Main action effect (damage, buff, movement)
- Success-only outcomes
- Powerful effects that require meeting conditions

**Effect Patterns**:
- Direct damage: `[Target Health] -= (1d6 + [Strength])`
- Buff/debuff: `[Defense] += 2 for 3 turns`
- Position change: `Move target 2 spaces North`
- Resource gain: `[Gold] += 1d4`
- State changes: `Target becomes "poisoned"`

**Design Principle**: The (do) component should contain the action's primary payoff—what the actor wants to happen when the condition succeeds.

### then: Always-Executed Effect Design

**Purpose**: Effects that ALWAYS execute, regardless of condition outcome

**Common Uses**:
- **Costs**: `[ActionPoints] -= 1`, `[Mana] -= 3`
- **Consumables**: `[Arrows] -= 1`
- **Universal consequences**: `Make noise`, `Leave tracks`
- **Cleanup effects**: `Remove marker`, `End status`

**Design Principle**: Use (then) for costs and effects that should occur whether the action succeeds or fails. This is ideal for action economy costs.

**Balance Considerations**:
- Higher costs for powerful (do) effects
- Free actions (no then cost) for basic operations
- Scaling costs for variable effects

### else: Alternative Effect Design

**Purpose**: Effects that execute ONLY when condition is FALSE

**When to Use**:
- Partial/reduced effects on failure
- Alternative outcomes
- Negative consequences for failure
- Different gameplay branches

**Examples**:
- Reduced damage: `[Target Health] -= 1d4` (vs 2d6 in do)
- Self-damage: `[Health] -= 1d4` (risky actions)
- Escalation: `[Target Alert] += 1` (failed stealth)
- Alternative resource: `[XP] += 1` (learn from failure)

**When to Omit**:
- Simple pass/fail gates
- Actions where failure has no effect
- When costs in (then) are sufficient consequence

**Design Principle**: The (else) component creates interesting failure states. It can soften failure or create risk-reward dynamics.

## Execution Flow for Designers

Understanding the execution order helps design cohesive actions:

**Sequence**:
1. Evaluate (if) condition → true or false
2. **Branch**:
   - If TRUE: Execute (do)
   - If FALSE: Execute (else) if defined
3. **Always**: Execute (then)

**Example Design**:
```
Power Strike (Action)
if: [ActionPoints] >= 2
do: [Target Health] -= (2d6 + [Strength])
then: [ActionPoints] -= 2
```

**Flow**: Check if actor has 2+ AP → If yes: deal heavy damage → Always: spend 2 AP

**What this means**: The actor pays the cost regardless of having enough AP, but only deals damage if the condition is met. This creates risk—spending resources without guarantee of success.

## Component References

Actions can use **inline** definitions or **referenced** components:

### Inline Action (All components defined in action)
```
Basic Attack (Action)
if: Adjacent to target AND [ActionPoints] >= 1
do: [Target Health] -= (1d6 + [Strength])
then: [ActionPoints] -= 1
```

### Referenced Components (Reusable building blocks)

**Define components separately**:
```
Adjacent With AP (Check)
Adjacent to target AND [ActionPoints] >= 1

Deal Basic Damage (Effect)
[Target Health] -= (1d6 + [Strength])

Pay One AP (Effect)
[ActionPoints] -= 1
```

**Reference in actions**:
```
Basic Attack (Action)
if: #Adjacent With AP
do: #Deal Basic Damage
then: #Pay One AP

Power Attack (Action)
if: #Adjacent With AP
do: [Target Health] -= (2d6 + [Strength])
then: #Pay One AP

Quick Strike (Action)
if: #Adjacent With AP
do: #Deal Basic Damage
then: (none)
```

**Benefits**:
- **Consistency**: Same check/effect across multiple actions
- **Maintenance**: Update once, affects all actions
- **Clarity**: Shorter action definitions
- **Modularity**: Mix and match components

**Design Guidance**: Use references when:
- Multiple actions share conditions
- Effects are reused frequently
- Maintaining consistency is important
- Campaign has many similar actions

## Balanced Action Design

### Power vs Cost

Costs in (then) should scale with power of (do) effects:

```
Light Attack (Action)
if: #Adjacent With AP
do: [Target Health] -= 1d4
then: [ActionPoints] -= 1

Medium Attack (Action)
if: #Adjacent With AP
do: [Target Health] -= 1d6 + [Strength]
then: [ActionPoints] -= 1

Heavy Attack (Action)
if: #Adjacent With AP
do: [Target Health] -= 2d6 + [Strength]
then: [ActionPoints] -= 2
```

**Balance principle**: Higher costs, more powerful effects.

### Risk vs Reward

Use (if) conditions and (else) components to create risk-reward dynamics:

```
Risky Strike (Action)
if: 1d20 + [Dexterity] > [Target Dexterity] + 10
do: [Target Health] -= 3d6
else: [Health] -= 1d6
then: [ActionPoints] -= 2
```

**Design**: High reward (3d6 damage) if you win the roll, but self-damage if you fail. Cost always paid.

### Conditional vs Universal Costs

**Pattern 1: Cost in (then) - Always paid**
```
Spell Attack (Action)
if: [Target Distance] <= [SpellRange]
do: [Target Health] -= (1d8 + [Intellect])
then: [Mana] -= 3, [ActionPoints] -= 1
```
Mana and AP spent regardless of range. Encourages positioning.

**Pattern 2: Cost in (do) - Only on success**
```
Craft Item (Action)
if: [Materials] >= 5
do: [Materials] -= 5, create item
then: (none)
```
Materials only consumed if you have enough. No waste.

**Design Choice**: Decide whether failed attempts should consume resources.

### Success/Failure Asymmetry

```
Persuade (Action)
if: 1d20 + [Charisma] > [Target Will]
do: Target becomes friendly, [Reputation] += 1
else: Target becomes hostile, [Reputation] -= 1
then: [ActionPoints] -= 1
```

**Design**: Significant different outcomes based on success. Creates meaningful tension.

## Common Action Patterns

### Standard Attack
```
Attack (Action)
if: #Can Reach Target
do: #Deal Damage
then: #Pay Cost
```

### Buff/Self-Enhancement
```
Defend (Action)
if: [ActionPoints] >= 1
do: [Defense] += 3 until next turn
then: [ActionPoints] -= 1
```

### Resource Conversion
```
Rest (Action)
if: [Energy] >= 2
do: [Energy] -= 2, [Health] += 1d6
then: (none)
```

### Conditional Scaling
```
Execute (Action)
if: [Target Health] < 5
do: [Target Health] -= 10d6
else: [Target Health] -= 1d6
then: [ActionPoints] -= 3
```

### All-or-Nothing
```
Hack Terminal (Action)
if: 1d20 + [Tech] > [Terminal Security]
do: Gain admin access
else: Alarm triggered, security +5
then: [ActionPoints] -= 2
```

## Design Checklist

When creating an action, verify:

- [ ] Condition (if) is precise and measurable
- [ ] Primary effect (do) creates meaningful outcome
- [ ] Costs (then) are appropriate for power level
- [ ] Alternative (else) creates interesting failure state (if used)
- [ ] Resource notation uses [brackets]
- [ ] Action doesn't trivialize challenges
- [ ] Action fits campaign theme and genre
- [ ] Action has clear use case in gameplay
- [ ] Consider whether components should be referenced

## Balance Testing

Playtest actions by considering:

1. **Frequency**: How often will this action be used?
2. **Power**: How much does it change game state?
3. **Cost**: Is the resource expenditure appropriate?
4. **Counterplay**: Can opponents respond or prevent it?
5. **Fun**: Does it create interesting decisions?

**Red flags**:
- Action always optimal (dominant strategy)
- Action never used (too weak or costly)
- Action has no downside or risk
- Action circumvents core mechanics

---

## See Also

- **Player's Handbook: Chapter 4**: Taking Actions (player perspective)
- **Chapter 2**: Effects - Designing effect components
- **Chapter 4**: Reactions - Trigger-based actions
- **Chapter 9: Reference**: Action Template
