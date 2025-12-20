# Quick Reference

## Dice Notation

- `XdY`: Roll X dice with Y sides
- Operators: `+`, `-`, `*`, `/`
- Division by zero = 0
- Negative results = 0
- Fractional results floor-divided

## Action Structure

```
if: Condition check (boolean expression)
do: Effects executed when condition is TRUE
then: Effects that ALWAYS execute (costs typically go here)
else: Effects executed when condition is FALSE (optional)
```

**Execution order**: (if) → [true: (do), false: (else)] → (then)

**Example**:
```
Basic Attack (Action)
if: [ActionPoints] >= 1
do: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

## Resource Notation

- Self resources: `[Resource]` (e.g., `[Health]`, `[ActionPoints]`)
- Target resources: `[Target Resource]` (e.g., `[Target Health]`)
- Brackets `[]` are required for resource injection

## Resource Rules

- Positive integers only (≥ 0)
- Cannot go below zero
- Lazy initialization: defaults to 0 on first use

## Balance Guidelines

**Cost-to-Damage Ratios**:
- 1 AP ≈ 1d6 damage baseline
- 2 AP ≈ 2d6 or 1d6+attribute
- 3 AP ≈ 3d6 or 2d6+attribute

**Condition Difficulty**:
- Simple checks (adjacent, resource ≥ X): Easy success
- Opposed rolls (1d20+modifier vs 1d20+modifier): ~50% success
- High threshold checks: 25-30% success rate

## Movement Costs

- Cardinal: Standard cost (typically 1)
- Diagonal: 1.5× standard (rounded up)

## Common Expressions

- `1d20+modifier`: Modified roll
- `[Resource]`: Your resource value
- `[Target Resource]`: Target's resource value
- `(expression1)-(expression2)`: Complex calculation
