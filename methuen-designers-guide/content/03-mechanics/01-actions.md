# Actions - Design Guide

## Designing Actions

Actions are the core of actor capabilities. Well-designed actions create meaningful decisions.

## Action Structure (Designer Perspective)

### if: Condition Design

**Purpose**: Gate the action to appropriate situations

**Good Conditions**:
- Resource checks: `self.actionPoints >= 2`
- Range checks: `target within 5 spaces`
- State checks: `target.health > 0`
- Tile checks: `target on "forest" tile`

**Avoid**:
- Ambiguous conditions: `if reasonable`
- Undefined terms: `if target is weak`

### do: Cost Design

**Purpose**: Resource expenditure to perform action

**Cost Types**:
- Action economy: `self.actionPoints -= 1`
- Consumables: `self.arrows -= 1`
- Stat requirements: `self.mana -= 3`

**Balance Considerations**:
- Higher costs for powerful effects
- Free actions for basic operations
- Scaling costs for variable effects

### then: Effect Design

**Purpose**: What happens on success

**Effect Patterns**:
- Direct damage: `target.health -= (1d6+self.strength)`
- Buff/debuff: `self.defense += 2 for 3 turns`
- Position: `target moves 2 spaces`
- Resource gain: `self.gold += 1d4`

### else: Failure Design

**Purpose**: What happens if conditions fail (optional)

**When to Use**:
- Partial cost refund
- Alternative minor effect
- Negative consequence

**When to Omit**:
- Simple conditional gates
- No-cost failed attempts

## Balanced Action Design

### Power vs Cost

More powerful effects require higher costs:
- Low: `1 AP, deal 1d4 damage`
- Medium: `2 AP, deal 1d6+modifier damage`
- High: `3 AP, deal 2d6+modifier damage to area`

### Risk vs Reward

Some actions gamble for better outcomes:
```
Risky Strike
if: self.actionPoints >= 2
do: self.actionPoints -= 2
then: if 1d20 > 15, deal 3d6 damage, else deal 1d4 damage
```

---

## See Also
- Chapter 7: Taking Actions (player perspective)
- Chapter 17: Reactions Design
- Reference: Action Template
