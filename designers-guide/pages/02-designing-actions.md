# Designing Actions

Actions are the core of actor capabilities. Well-designed actions create meaningful decisions and strategic depth.

## Action Structure

Every action has four components:

**if**: Condition check (true/false)
**do**: Effects when condition is TRUE
**then**: Effects that ALWAYS execute
**else**: Effects when condition is FALSE (optional)

**Execution order**: Evaluate (if) → Execute (do or else) → Execute (then)

## Component Design

### if: Condition Design

Purpose: Determine which effect branch executes.

**Good conditions**:
- Resource checks: `[ActionPoints] >= 2`
- Range checks: `Adjacent to target`
- Opposed rolls: `1d20 + [Dexterity] > [Target Dexterity] + 10`
- State checks: `[Target Health] > 0`

**Avoid**:
- Ambiguous conditions: `if reasonable`
- Undefined terms: `if target is weak`

### do: Primary Effect Design

Purpose: Effects that execute ONLY when condition is TRUE.

**Common patterns**:
- Direct damage: `[Target Health] -= (1d6 + [Strength])`
- Buffs: `[Defense] += 2 for 3 turns`
- Position changes: `Move target 2 spaces North`
- Resource gain: `[Gold] += 1d4`

### then: Always-Executed Effect Design

Purpose: Effects that ALWAYS execute regardless of condition.

**Common uses**:
- Resource costs: `[ActionPoints] -= 1`
- Consumables: `[Arrows] -= 1`
- Counters: `[AttacksMade] += 1`
- Universal consequences: `Make noise`, `Trigger alarm`

### else: Alternative Effect Design

Purpose: Effects that execute ONLY when condition is FALSE.

**When to use**:
- Partial effects on failure: `[Target Health] -= 1d4` (vs 2d6 in do)
- Self-damage: `[Health] -= 1d4` (risky actions)
- Escalation: `[Target Alert] += 1` (failed stealth)

**When to omit**:
- Simple pass/fail gates
- Actions where failure has no effect

## Simple Action Examples

### Basic Attack

```
Basic Attack
Range: Adjacent
if: [ActionPoints] >= 1
do: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

### Defend

```
Defend
if: [ActionPoints] >= 1
do: [Defense] += 2 until next turn
then: [ActionPoints] -= 1
```

### Resource Transfer

```
Give Gold
if: [Gold] >= 5
do: [Gold] -= 5, [Target Gold] += 5
```

Transfer only if you have enough. No (then) means no cost if condition fails.

## Balanced Action Design

### Power vs Cost

Scale resource costs with effect power:

```
Light Attack
if: Adjacent to target
do: [Target Health] -= 1d4
then: [ActionPoints] -= 1

Heavy Attack
if: Adjacent to target
do: [Target Health] -= 2d6 + [Strength]
then: [ActionPoints] -= 2
```

Heavy Attack trades efficiency for power.

### Risk vs Reward

Use (else) to create risk-reward dynamics:

```
Risky Strike
if: 1d20 + [Dexterity] > [Target Dexterity] + 10
do: [Target Health] -= 3d6
else: [Health] -= 1d6
then: [ActionPoints] -= 2
```

High damage on success, self-damage on failure.

## Resource Expenditure Patterns

**Pattern 1: Expenditure in (then) - Always occurs**
```
Spell Attack
if: [Target Distance] <= [SpellRange]
do: [Target Health] -= (1d8 + [Intellect])
then: [Mana] -= 3, [ActionPoints] -= 1
```

**Pattern 2: Expenditure in (do) - Only on success**
```
Craft Item
if: [Materials] >= 5
do: [Materials] -= 5, create item
```

**Pattern 3: Counters in (then)**
```
Inspire Allies
if: [Charisma] > 5
do: All allies gain +2 attack
then: [Inspired Counter] += 1
```

Choose pattern based on desired behavior.

## Component References

Reuse common checks and effects:

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

Benefits: Consistency, clarity, easier maintenance.

## Design Antipatterns

### Antipattern: No Meaningful Choice

```
Super Power
if: [ActionPoints] >= 1
do: Deal 10d20 damage, gain +5 Defense, heal 2d10
then: [ActionPoints] -= 1
```

Problem: No trade-offs, strictly dominates other actions.

Fix: Add risk, increase cost, or reduce power.

### Antipattern: Invisible Failure

```
Lockpick
if: 1d20 + [Dexterity] > [Lock Difficulty]
do: Door unlocks
then: [ActionPoints] -= 1
```

Problem: Failure has no consequence beyond wasted AP.

Fix: Add (else) with meaningful consequence:
```
else: [Lockpick] -= 1, [Noise] += 1
```

### Antipattern: Kitchen Sink

```
Ultimate Combo
if: [ActionPoints] >= 3
do: Deal damage, heal, move, gain defense, apply status, gain gold, summon ally
then: [ActionPoints] -= 3
```

Problem: Too many unrelated effects.

Fix: Split into focused actions.

## Action Design Checklist

When creating an action, verify:

☐ Condition (if) is precise and measurable
☐ Primary effect (do) creates meaningful outcome
☐ Always-effects (then) serve clear purpose
☐ Alternative (else) creates interesting failure state (if used)
☐ Resource notation uses [brackets]
☐ Action doesn't trivialize challenges
☐ Action has clear use case in gameplay

## Balance Testing

Playtest actions by considering:

**Frequency**: How often will this be used?
**Impact**: How much does it change game state?
**Resource Flow**: Are costs appropriate?
**Counterplay**: Can opponents respond?
**Engagement**: Does it create interesting decisions?

Red flags:
- Action always optimal (dominant strategy)
- Action never used (too weak)
- Action has no trade-offs
- Action circumvents core mechanics
