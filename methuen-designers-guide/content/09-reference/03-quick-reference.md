# Quick Reference

## Dice Notation

- `XdY`: Roll X dice with Y sides
- Operators: `+`, `-`, `*`, `/`
- Division by zero = 0
- Negative results = 0
- Fractional results floor-divided

## Action Structure

```
if: Conditions
do: Costs
then: Success effects
else: Failure effects (optional)
```

## Resource Rules

- Positive integers only (≥ 0)
- Cannot go below zero
- Initialize on first use if lazy init

## Movement Costs

- Cardinal: Standard cost (typically 1)
- Diagonal: 1.5× standard (rounded up)

## Common Expressions

- `1d20+modifier`: Modified roll
- `self.resource`: Your resource value
- `target.resource`: Target's resource value
- `(expression1)-(expression2)`: Complex calculation
