# Taking Actions

## What is an Action?

**Definition**: An **action** is a structured operation an actor can perform, defined by four components: **if**, **do**, **then**, and **else**.

## Action Structure

Every action follows this template:

### if: Conditions
Requirements that must be met to attempt the action
- Resource checks (self.actionPoints >= 2)
- Range requirements (target within 5 spaces)
- State requirements (target is on "forest" tile)

### do: Costs
Resources spent to perform the action
- Resource deductions (self.actionPoints -= 1)
- Material consumption (self.arrows -= 1)
- State changes required to attempt

### then: Success Outcome
What happens when the action succeeds
- Effects on target (target.health -= damage)
- Effects on self (self.position moves 3N)
- Changes to environment (tile becomes "burned")

### else: Failure Outcome (Optional)
What happens if conditions aren't met or action fails
- Partial effects
- Alternative consequences
- Often omitted if no failure state exists

## Performing an Action

### Step 1: Declare Action and Target

Announce which action you're performing and what/who the target is.

**Example**: "I'm using Harvest Crop on the tile at 3N 2W"

### Step 2: Check Conditions (if)

Verify all conditions in the **if** component are met:

- Do you meet resource requirements?
- Is the target in range?
- Are state requirements satisfied?

If any condition fails, proceed to **else** (if defined) or the action cannot be performed.

### Step 3: Pay Costs (do)

Deduct resources or make changes specified in the **do** component:

- Subtract action points
- Consume materials
- Change states

**Important**: Costs are paid even if later steps fail.

### Step 4: Resolve Outcome (then)

Apply all effects listed in the **then** component:

- Calculate expressions (roll dice, reference resources)
- Modify resources
- Change positions
- Update states

If the **then** component includes multiple effects, resolve them in the order listed.

### Step 5: Update Character Sheet

Record all resource changes on your character sheet.

## Example Action Walkthrough

**Action: Precise Strike**

```
if: Adjacent to target AND self.actionPoints >= 2
do: self.actionPoints -= 2
then: target.health -= (1d6+self.accuracy)
else: self.actionPoints -= 1 (partial cost for failed attempt)
```

**Walkthrough**:

1. **Declare**: "I use Precise Strike on the adjacent actor"

2. **Check Conditions**:
   - Adjacent to target? Yes (1 space away)
   - self.actionPoints >= 2? Yes (I have 4)
   - Conditions met ✓

3. **Pay Costs**:
   - self.actionPoints -= 2
   - 4 - 2 = 2 actionPoints remaining

4. **Resolve Outcome**:
   - Roll 1d6: result is 4
   - Add self.accuracy: 4 + 3 = 7
   - target.health -= 7
   - Target had 15 health, now has 8

5. **Update Sheet**:
   - ActionPoints: 4 → 2

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

Special actions performed outside your turn in response to triggers. See **Chapter 8: Reactions**.

### Free Actions

Actions that don't count against action economy, as defined by campaign.

## Common Action Patterns

### Resource Transfer
```
if: self.gold >= amount
do: self.gold -= amount
then: target.gold += amount
```

### Position Change
```
if: self.movementPoints >= 3
do: self.movementPoints -= 3
then: self.position changes 3 spaces in chosen direction
```

### Conditional Effect
```
if: target.health < 10
do: self.actionPoints -= 1
then: target.health -= 2d6
else: target.health -= 1d6
```

## Action Costs vs. Effects

**Important Distinction**:

- **Costs** (do): Paid by the actor performing the action
- **Effects** (then/else): Applied to targets or environment

Costs are always paid, even if the outcome doesn't occur as intended.

## Invalid Actions

You cannot perform an action if:

- Conditions are not met (if fails)
- You cannot pay the cost (insufficient resources)
- No valid target exists
- Campaign rules prohibit it

---

## See Also

- **Chapter 2**: Dice Notation - Understanding expressions
- **Chapter 6**: Turn Structure - When actions can be performed
- **Chapter 11**: Actions Design - For campaign designers creating actions
