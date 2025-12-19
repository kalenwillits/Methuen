# NPC Strategies

## What are Strategies?

**Strategies** are collections of behaviors that define how non-player actors behave.

## Strategy Structure

```
Strategy: [Name]
Behaviors (in priority order):
  1. Behavior: [Highest priority]
  2. Behavior: [Medium priority]
  3. Behavior: [Fallback]
```

**Example**:
```
Strategy: Goblin Tactics
Behaviors:
  1. Flee if health < 3
  2. Attack if adjacent to enemy
  3. Move toward nearest enemy
  4. Move randomly
```

## Evaluation Order

Behaviors are evaluated in order until one succeeds:
1. Check first behavior conditions
2. If all checks pass, perform action
3. If checks fail, move to next behavior
4. Repeat until a behavior executes

## Balancing NPC Intelligence

**Simple Strategies**: 1-3 behaviors, straightforward logic
**Complex Strategies**: 5+ behaviors, tactical depth

---

## See Also
- Chapter 21: Behaviors
- Chapter 16: Actions Design
