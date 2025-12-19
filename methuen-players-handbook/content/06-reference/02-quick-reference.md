# Quick Reference

## Dice Notation

- `XdY`: Roll X dice with Y sides
- Operators: `+`, `-`, `*`, `/`
- Division by zero = 0
- Negative results = 0
- Fractional results floor-divided

## Action Structure

```
if: Condition check (boolean)
do: Effects when condition is TRUE
then: Effects that ALWAYS execute
else: Effects when condition is FALSE (optional)
```

**Execution Order**: (if) → [true: (do), false: (else)] → (then)

## Component References

- `#Name`: Reference a Check or Effect component
- Allows reusing components across multiple actions
- Example: `if: #Has ActionPoints`

## Resource Notation

- `[Resource]`: Your resource value
- `[Target Resource]`: Target's resource value
- `[Resource] >= value`: Comparison
- `[Resource] -= amount`: Modification

## Resource Rules

- Positive integers only (≥ 0)
- Cannot go below zero
- Initialize on first use if lazy init
- Default initialization value: 0

## Movement Costs

- Cardinal: Standard cost (typically 1)
- Diagonal: 1.5× standard (rounded up)

## Common Expressions

- `1d20+modifier`: Modified roll
- `[Resource]`: Your resource value
- `[Target Resource]`: Target's resource value
- `(expression1)-(expression2)`: Complex calculation

## Directions

- **Cardinals**: N, E, S, W
- **Diagonals**: NE, SE, SW, NW

## Turn Checklist

1. Resolve start-of-turn triggers
2. Check action economy (how many actions allowed)
3. Perform actions:
   - Evaluate (if) condition
   - Execute (do) if true, (else) if false
   - Execute (then) always
4. Perform movement
5. Resolve end-of-turn triggers
6. Announce turn complete
