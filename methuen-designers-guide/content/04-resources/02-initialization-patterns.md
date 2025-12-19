# Resource Initialization Patterns

## Initialization Rules

Define how resources start when an actor is created or when a resource is first referenced.

## Pattern Types

### Fixed Value
```
Gold: Starts at 100
```

### Simple Dice Roll
```
Strength: Roll 1d20
Health: Roll 3d6
```

### Modified Dice Roll
```
Health: Roll 1d20+10
StartingGold: Roll 2d6×10
```

### Derived from Other Resources
```
MaxHealth: Strength + Constitution
CarryCapacity: Strength × 5
```

### Conditional Initialization
```
Gold: Roll 3d6 if Noble background, else roll 1d6
```

### Table-Based
```
StartingLocation: Roll 1d10, consult Starting Position table
```

## Lazy Initialization

Resources don't need to be initialized until first used. When a resource appears:
1. Check campaign for initialization rule
2. If rule exists, apply it
3. If no rule, resource starts at 0
4. Record value on character sheet

---

## See Also
- Chapter 12: Creating Resources
- Chapter 5: Setup Phase
