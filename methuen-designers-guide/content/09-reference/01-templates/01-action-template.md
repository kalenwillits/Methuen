# Action Template

## Action Template (Inline)

Use this template when defining actions with all components inline:

```
Action Name: _______________
Range: _______________
Target: _______________

if: Boolean condition expression
do: Effect(s) executed when condition is TRUE
then: Effect(s) that ALWAYS execute
else: Effect(s) executed when condition is FALSE (optional)
```

**Execution Order**: (if) → [true: (do), false: (else)] → (then)

## Action Template (Referenced)

Use this template when using component references:

```
Action Name: _______________
Range: _______________
Target: _______________

if: #Check Component Name
do: #Effect Component Name
then: #Effect Component Name
else: #Effect Component Name (optional)
```

## Check Component Template

```
Check Name: _______________
Boolean expression that evaluates to true or false
```

**Example**:
```
Has Action Point (Check)
[ActionPoints] >= 1
```

## Effect Component Template

```
Effect Name: _______________
Resource modifications, state changes, or other game effects
```

**Example**:
```
Deal Basic Damage (Effect)
[Target Health] -= (1d6 + [Strength])
```

## Complete Examples

### Example 1: Inline Action

```
Action Name: Power Strike
Range: Adjacent
Target: Single actor

if: Adjacent to target AND [ActionPoints] >= 2
do: [Target Health] -= (2d6 + [Strength])
then: [ActionPoints] -= 2
else: (none)
```

**Explanation**:
- Check if adjacent and have 2+ AP
- If true: Deal heavy damage
- Always: Spend 2 AP (cost paid regardless)

### Example 2: Referenced Action

**Components**:
```
Can Harvest (Check)
Target is "Farmland" tile AND [CropGrowth] > 5

Collect Crop (Effect)
[Food] += [CropGrowth], [CropGrowth] = 0

Pay Action Cost (Effect)
[ActionPoints] -= 1
```

**Action**:
```
Action Name: Harvest Crop
Range: Adjacent tile
Target: Single tile

if: #Can Harvest
do: #Collect Crop
then: #Pay Action Cost
else: (none)
```

**Explanation**:
- Reuses components for consistency
- Multiple actions can reference #Pay Action Cost
- Easier to maintain and update

### Example 3: Action with Failure Consequence

```
Action Name: Risky Strike
Range: Adjacent
Target: Single actor

if: 1d20 + [Dexterity] > [Target Dexterity] + 10
do: [Target Health] -= 3d6
then: [ActionPoints] -= 2
else: [Health] -= 1d4
```

**Explanation**:
- Opposed roll determines success
- Success: Deal heavy damage to target
- Failure: Take damage yourself
- Always: Pay 2 AP

### Example 4: Conditional Scaling

```
Action Name: Execute
Range: Adjacent
Target: Single actor

if: [Target Health] < 5
do: [Target Health] -= 10d6
then: [ActionPoints] -= 3
else: [Target Health] -= 1d6
```

**Explanation**:
- Condition checks target's health
- Low health: Massive damage
- Normal health: Standard damage
- Always: High cost (3 AP)

### Example 5: Resource Conversion

```
Action Name: Rest
Range: Self
Target: Self

if: [Energy] >= 2
do: [Energy] -= 2, [Health] += 1d6
then: (none)
else: (none)
```

**Explanation**:
- Check if you have energy
- If yes: Convert energy to health
- No universal cost (cost is in do)

## Design Guidelines

### Condition (if)

- Must be measurable and precise
- Should create meaningful decision point
- Can use comparisons, dice rolls, state checks
- Avoid ambiguous terms

### Primary Effect (do)

- Main payoff of the action
- Only executes on condition success
- Should be balanced with cost in (then)
- Can include multiple effects

### Always Effect (then)

- Ideal for action economy costs
- Universal consequences
- Cleanup effects
- Executed regardless of success/failure

### Alternative Effect (else)

- Creates interesting failure states
- Optional component
- Can soften failure or add risk
- Use when failure should have consequences

## Design Decision Guide

### Should I use inline or referenced components?

**Use Inline When:**
- Action is unique or rarely reused
- Campaign is small (< 20 actions)
- Prototyping and iterating quickly

**Use References When:**
- Multiple actions share conditions/effects
- Maintaining consistency is important
- Campaign is large or will grow over time

### Should conditions be resource checks or dice rolls?

**Resource Checks** (`[ActionPoints] >= 2`):
- Deterministic, predictable outcomes
- Players can plan with certainty
- Good for resource management focus

**Dice Rolls** (`1d20 + [Dexterity] > 15`):
- Adds uncertainty and tension
- Creates memorable moments (crits/fails)
- Good for action/adventure focus

**Opposed Rolls** (`1d20+[Stat] > [Target Stat]+10`):
- Interactive competition
- Scales with character growth
- Good for PvP or dramatic contests

### Where should I put costs?

**Cost in (then) - Always Paid:**
- Use when: Attempting the action itself has consequences
- Creates: Strategic positioning, resource tension
- Example: Spell costs mana even if target is out of range

**Cost in (do) - Only on Success:**
- Use when: Failure shouldn't waste resources
- Creates: Player-friendly experimentation
- Example: Crafting only consumes materials if you have enough

## Component Reusability

Define common components once:

```
# Commonly used checks
Has AP (Check)
[ActionPoints] >= 1

Adjacent (Check)
Adjacent to target

# Commonly used effects
Pay One AP (Effect)
[ActionPoints] -= 1

Deal Standard Damage (Effect)
[Target Health] -= 1d6
```

Reference in multiple actions:

```
Attack (Action)
if: #Has AP AND #Adjacent
do: #Deal Standard Damage
then: #Pay One AP

Defend (Action)
if: #Has AP
do: [Defense] += 2 until next turn
then: #Pay One AP
```

## Testing Your Actions

After creating an action, verify:

- [ ] Condition is clear and measurable
- [ ] Effects are balanced for their cost
- [ ] Resource notation uses [brackets]
- [ ] Execution flow makes sense
- [ ] Action fits campaign balance
- [ ] No ambiguous or undefined terms
- [ ] Considers both success and failure paths
