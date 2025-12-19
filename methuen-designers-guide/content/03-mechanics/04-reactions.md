# Reactions - Design Guide

## Designing Reactions

Reactions add tactical depth by allowing responses outside normal turns.

## Reaction Components

### Trigger Definition

**Be Specific**:
- `When an adjacent actor moves away`
- `When you take damage from a ranged action`
- `At the start of any actor's turn`

**Avoid Ambiguity**:
- Not: `When something bad happens`
- Not: `When you're in danger`

### Reaction Structure

Same as actions, plus trigger:
```
Reaction: Counter-Attack
Trigger: You are targeted by a melee action
if: self.actionPoints >= 1
do: self.actionPoints -= 1
then: Deal 1d4 damage to attacker
```

## Reaction Timing

Define when reaction resolves:
- **Before** triggering event
- **After** triggering event
- **Instead of** triggering event

## Balancing Reactions

### Limit Frequency

Prevent reaction spam:
- "Once per turn"
- "Once per round"
- "Costs resources" (natural limiter)

### Match Power to Cost

Reactions should cost appropriately:
- Defensive reactions: Moderate cost
- Offensive reactions: Higher cost
- Utility reactions: Lower cost

---

## See Also
- Chapter 10: Reactions (player perspective)
- Chapter 16: Actions Design
- Reference: Reaction Template
