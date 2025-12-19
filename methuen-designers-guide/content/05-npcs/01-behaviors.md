# NPC Behaviors

## What are Behaviors?

**Behaviors** define how non-player actors make decisions.

## Behavior Structure

```
Behavior: [Name]
Checks: [Conditions to evaluate]
Action: [What to do if checks pass]
```

**Example**:
```
Behavior: Attack Nearest
Checks: 
  - Is there an actor within 5 spaces?
  - Do I have actionPoints >= 1?
Action: Move toward nearest actor, then attack if adjacent
```

## Check Types

- **Resource checks**: Does actor have enough resources?
- **Position checks**: Is target in range?
- **State checks**: Is target valid?
- **Priority checks**: Is this the best option?

## Writing Behaviors

1. Define the condition(s)
2. Specify the action to take
3. Include fallback if checks fail

---

## See Also
- Chapter 22: Strategies
- Chapter 16: Actions Design
