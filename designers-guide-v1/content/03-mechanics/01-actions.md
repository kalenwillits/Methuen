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
- Resource changes: `[ActionPoints] -= 1`, `[Mana] -= 3`, `[Gold] += 5`
- Consumables: `[Arrows] -= 1`, `[Potions] += 1`
- Universal consequences: `Make noise`, `Leave tracks`, `Trigger alarm`
- Cleanup effects: `Remove marker`, `End status`, `Reset counter`
- Chained actions: `then: #FollowUpAction`
- Status applications: `[Burning] += 1`, `Mark target`

**Design Principle**: Use (then) for effects that should occur whether the condition succeeds or fails. This creates certainty in outcomes.

**Common Patterns**:
- **Pattern A**: Resource expenditure (action costs resources to attempt)
- **Pattern B**: Guaranteed effects (something always happens)
- **Pattern C**: Action chains (trigger follow-up actions)
- **Pattern D**: State tracking (counters, markers, flags)

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

**Flow**: Check if actor has 2+ AP → If yes: deal heavy damage → Always: reduce 2 AP

**What this means**: The AP reduction happens whether or not the actor had enough. The (do) effect only happens when condition is true. This demonstrates (then) as "always executes."

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

## Action Chaining

Actions can trigger other actions through (then) and (else) clauses, creating multi-step sequences.

### How Action Chaining Works

**Syntax**: Reference an action by name within then/else components:
```
Attack and Retreat (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + [Strength])
then: Move 2 spaces away from target; #Stealth Check
```

**Execution Flow**:
1. Evaluate (if) condition
2. Execute (do) or (else) based on result
3. Execute (then) which triggers:
   - Resource changes
   - Status effects
   - **Chained actions** (execute immediately in sequence)

### Chaining vs Component References

**Component References** (reusable building blocks):
- Share common checks or effects
- Reduce duplication
- Single execution context

**Action Chaining** (sequential actions):
- Multi-step sequences
- Complex combinations
- Each action has own execution flow

### Examples of Action Chains

**Example 1: Attack and Reposition**
```
Strike and Withdraw (Action)
if: Adjacent to target AND [ActionPoints] >= 2
do: [Target Health] -= (1d8 + [Strength]); then: #Tactical Retreat
else: (none)
then: [ActionPoints] -= 2
```

The #Tactical Retreat action executes after damage, allowing immediate repositioning.

**Example 2: Conditional Follow-Up**
```
Test Defenses (Action)
if: 1d20 + [Strength] > [Target Defense] + 12
do: [Target Health] -= 1d4; then: #Power Strike
else: [Confidence] -= 1
then: [ActionPoints] -= 1
```

If the initial strike succeeds, immediately follow with a power strike (spending its cost separately).

**Example 3: Escalating Sequence**
```
Combo Attack (Action)
if: [Combo Counter] >= 2
do: [Target Health] -= 2d6; [Combo Counter] = 0; then: #Victory Cry
else: [Combo Counter] += 1
then: [ActionPoints] -= 1
```

Building to a powerful attack that triggers a buff action on success.

### Design Considerations for Chaining

**When to Use Chaining**:
- Multi-step tactics (attack then reposition)
- Combo systems (build up to powerful finisher)
- Conditional sequences (if hit, then follow-up)
- Escalating effects (each success enables stronger action)

**When NOT to Use Chaining**:
- Simple resource changes (use direct effects instead)
- Effects that should happen simultaneously (use component composition)
- Actions already complex (avoid over-complication)

**Balance Considerations**:
- Each chained action executes its own (then) effects
- Can create unexpectedly complex effect combinations
- May require extensive playtesting for simulation balance
- Consider total effect accumulation across chain

### Chaining Execution Order

```
Primary Action
if: [condition]
do: [effects]; then: #ChainedAction1
then: #ChainedAction2

ChainedAction1
if: [condition]
do: [effects]
then: [cost]

ChainedAction2
if: [condition]
do: [effects]
then: [cost]
```

**Order**:
1. Primary action (if) evaluated
2. Primary action (do) or (else) executes
3. Primary action chained actions execute in order
4. Primary action (then) effects applied
5. ChainedAction1 fully resolves (if/do/then)
6. ChainedAction2 fully resolves (if/do/then)

**Important**: Chained actions execute completely before returning to parent action's (then) effects.

### Advanced Pattern: Branching Chains

```
Adaptive Strike (Action)
if: [Target Health] > 20
do: [Target Health] -= 1d6; then: #Heavy Follow-Up
else: [Target Health] -= 2d6; then: #Execute Strike
then: [ActionPoints] -= 2
```

Different branches can chain to different actions based on conditions.

## Balanced Action Design

### Power vs Resource Expenditure

When using (then) for resource expenditure, scale it with power of (do) effects:

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

**Design Commentary:**
- **Design Goal**: Create meaningful tactical choices between efficiency and power. Players decide whether to use AP efficiently or burst damage.
- **Balance Rationale**: Light Attack (1 AP, avg 2.5 damage) is most efficient. Heavy Attack (2 AP, avg 7+STR damage) trades efficiency for power. Medium Attack balances both with attribute scaling.
- **Player Decision**: "Should I attack twice with Light, once with Heavy, or balance with Medium?" Creates resource management tension.
- **Power Curve**: Resource expenditure scales sub-linearly (1, 1, 2) while damage scales super-linearly (1d4, 1d6+STR, 2d6+STR), rewarding investment in powerful attacks.

**Note**: This is ONE pattern (resource expenditure in then). Equally valid: resource gain in then, status effects in then, or chained actions in then.

### Risk vs Reward

Use (if) conditions and (else) components to create risk-reward dynamics:

```
Risky Strike (Action)
if: 1d20 + [Dexterity] > [Target Dexterity] + 10
do: [Target Health] -= 3d6
else: [Health] -= 1d6
then: [ActionPoints] -= 2
```

**Design Commentary:**
- **Design Goal**: Create high-stakes decisions where players gamble for powerful effects. Introduces risk-reward tension.
- **Balance Rationale**: Opposed roll (1d20+DEX vs DEX+10) gives roughly 30-40% success rate depending on attributes. High damage (3d6 avg 10.5) balances resource expenditure (2 AP) and self-damage risk.
- **Player Decision**: "Is the reward worth risking my own Health?" Situational - valuable when ahead, dangerous when low on Health.
- **Failure Consequence**: Taking damage on failure creates meaningful stakes and prevents spamming risky actions.

### Resource Expenditure Patterns

**Pattern 1: Expenditure in (then) - Always occurs**
```
Spell Attack (Action)
if: [Target Distance] <= [SpellRange]
do: [Target Health] -= (1d8 + [Intellect])
then: [Mana] -= 3, [ActionPoints] -= 1
```
Mana and AP spent regardless of range. Action attempt has cost.

**Pattern 2: Expenditure in (do) - Only on success**
```
Craft Item (Action)
if: [Materials] >= 5
do: [Materials] -= 5, create item
then: (none)
```
Materials only consumed if condition met. No waste on failure.

**Pattern 3: Guaranteed effect in (then)**
```
Inspire Allies (Action)
if: [Charisma] > 5
do: All allies gain +2 attack
then: [Inspired Counter] += 1
```
Counter increments whether or not Charisma check succeeds. Tracks attempts.

**Pattern 4: Chained actions in (then)**
```
Strike and Fade (Action)
if: Adjacent to target
do: [Target Health] -= 1d8
then: #Tactical Retreat
```
Retreat action executes regardless of hit/miss. Movement always happens.

**Design Principle**: Choose pattern based on desired simulation behavior, not prescribed "best practices." Methuen is a framework—these are tools, not rules.

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
then: #Reduce Resources
```
(Using then for resource expenditure is one common pattern)

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

## Action Design Antipatterns

Understanding common mistakes helps you design cleaner, more maintainable actions.

### Antipattern: Cluttered Condition Checks

A common mistake is putting resource requirements and bookkeeping checks in the IF clause instead of using Features:

**❌ AVOID:**
```
Melee Strike (Action)
if: [ActionPoints] >= 1 AND [Stamina] >= 5 AND Adjacent to target AND [Weapon Equipped] = 1
do: [Target Health] -= (1d8 + [Strength])
then: [Stamina] -= 5; [ActionPoints] -= 1
```

**Why this is problematic:**
- The IF condition is cluttered with bookkeeping (AP check, Stamina check, equipment check)
- The actual interesting decision (hitting the target) is buried or absent
- Resource requirements are repeated across similar actions, creating maintenance burden
- New players can't quickly identify what the meaningful choice is

**✓ PREFER:**
```
Melee Strike (Action)
Requirements (as Features on this action):
- Requires: 1 Action Point
- Requires: 5 Stamina
- Requires: Adjacent to target
- Requires: Weapon equipped

if: 1d20 + [Strength] > [Target Defense] + 10
do: [Target Health] -= (1d8 + [Strength])
then: [Stamina] -= 5; [ActionPoints] -= 1
```

**Why this is better:**
- IF contains the actual skill check (the interesting probabilistic decision)
- Requirements are listed clearly and separately as constraints
- Action is more readable and easier to maintain
- Players can quickly see what the meaningful choice is (roll vs Defense)
- Consistent presentation across all actions

**Design Principle**: Use Features to list static requirements (resource minimums, range, equipment). Use IF for the meaningful gameplay decision (skill checks, opposed rolls, tactical choices, probabilistic outcomes).

### Antipattern: No Meaningful Choice

Actions where the IF condition is trivial or the outcome is always optimal:

**❌ AVOID:**
```
Super Power (Action)
if: [ActionPoints] >= 1
do: Deal 10d20 damage, gain +5 Defense, heal 2d10 Health
then: [ActionPoints] -= 1
```

**Why this is problematic:**
- No trade-offs or opportunity cost beyond 1 AP
- Strictly dominates all other actions
- Creates degenerate strategy (spam this action every turn)
- Removes meaningful tactical decisions

**✓ PREFER - Add Risk:**
```
Risky Power (Action)
if: 1d20 > 12
do: Deal 3d10 damage, gain +5 Defense
else: Take 2d6 damage
then: [ActionPoints] -= 2
```

**✓ PREFER - Add Resource Cost:**
```
Limited Power (Action)
if: [ActionPoints] >= 2 AND [Energy] >= 10
do: Deal 3d10 damage, gain +3 Defense
then: [ActionPoints] -= 2; [Energy] -= 10
```

**Design Principle**: Every action should have trade-offs. Balance power with risk, resource expenditure, or opportunity cost.

### Antipattern: Invisible Failure States

Actions where failure has no feedback or consequence:

**❌ AVOID:**
```
Lockpick (Action)
if: 1d20 + [Dexterity] > [Lock Difficulty]
do: Door unlocks
then: [ActionPoints] -= 1
```

**Why this is problematic:**
- Failure just wastes AP with no interesting consequence
- Encourages tedious repeated attempts
- No tension or meaningful risk

**✓ PREFER - Add Failure Consequence:**
```
Lockpick (Action)
if: 1d20 + [Dexterity] > [Lock Difficulty]
do: Door unlocks
else: [Lockpick] -= 1; [Noise] += 1 (might alert guards)
then: [ActionPoints] -= 1
```

**Design Principle**: Use ELSE to create interesting failure states. Consequences can be resource loss, escalation (alarms, reinforcements), or partial effects.

### Antipattern: Kitchen Sink Actions

Actions that try to do everything:

**❌ AVOID:**
```
Ultimate Combo (Action)
if: [ActionPoints] >= 3 AND [Mana] >= 10 AND [Stamina] >= 5
do: Deal 2d6 damage, heal 1d6, move 3 spaces, gain +2 Defense, apply Burning to target, gain 5 Gold, summon ally
then: [ActionPoints] -= 3; [Mana] -= 10; [Stamina] -= 5
```

**Why this is problematic:**
- Too many unrelated effects create confusion
- Difficult to balance and playtest
- Players can't build clear mental model
- Trivializes multiple game systems

**✓ PREFER - Focused Actions:**
```
Strike (Action)
if: Adjacent to target
do: Deal 2d6 damage, apply Burning
then: [ActionPoints] -= 1

Tactical Retreat (Action)
if: [Stamina] >= 5
do: Move 3 spaces, gain +2 Defense until next turn
then: [Stamina] -= 5; [ActionPoints] -= 1
```

**Design Principle**: Each action should have a clear purpose and focused effect. Use action chaining for multi-step combinations rather than bundling everything into one action.

### Antipattern: Ambiguous or Unmeasurable Conditions

Conditions that require subjective interpretation:

**❌ AVOID:**
```
Intimidate (Action)
if: You appear threatening
do: Target becomes afraid
then: [ActionPoints] -= 1
```

**Why this is problematic:**
- "Appear threatening" is subjective and unmeasurable
- No clear resolution mechanism
- Creates arguments and inconsistency

**✓ PREFER - Measurable Conditions:**
```
Intimidate (Action)
if: 1d20 + [Strength] + [Charisma] > [Target Willpower] + 10
do: [Target Morale] -= 1d6
then: [ActionPoints] -= 1
```

**Design Principle**: Conditions must be objectively resolvable using resources, dice rolls, or measurable game state. Avoid vague requirements.

## Design Checklist

When creating an action, verify:

- [ ] Condition (if) is precise and measurable
- [ ] Primary effect (do) creates meaningful outcome
- [ ] Always-executed effects (then) serve clear purpose
- [ ] Alternative (else) creates interesting failure state (if used)
- [ ] Resource notation uses [brackets]
- [ ] Action doesn't trivialize challenges
- [ ] Action fits campaign theme and genre
- [ ] Action has clear use case in gameplay
- [ ] Consider whether components should be referenced

## Balance Testing

Playtest actions by considering:

1. **Frequency**: How often will this action be used?
2. **Impact**: How much does it change game state?
3. **Resource Flow**: Are resource changes appropriate?
4. **Counterplay**: Can opponents respond or prevent it?
5. **Engagement**: Does it create interesting decisions?

**Red flags**:
- Action always optimal (dominant strategy)
- Action never used (too weak or resource-intensive)
- Action has no trade-offs or consequences
- Action circumvents core mechanics

---

## See Also

- **Player's Handbook: Chapter 4**: Taking Actions (player perspective)
- **Chapter 2**: Effects - Designing effect components
- **Chapter 4**: Reactions - Trigger-based actions
- **Chapter 9: Reference**: Action Template
