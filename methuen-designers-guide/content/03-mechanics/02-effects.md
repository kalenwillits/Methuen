# Effects

## What are Effects?

**Effects** are active changes that occur when triggered by actions or features.

## Effect Characteristics

- Occur at specific moments (not always active)
- Make explicit changes to game state
- Written as imperative commands
- Resolve immediately when triggered

## Effect Types

### Resource Modification
```
Deal 1d6 damage to target
target.health -= 1d6

Gain 10 gold
self.gold += 10
```

### Position Change
```
Move 3 spaces North
self.location changes 3N

Push target 2 spaces away
target.location changes 2 spaces directly away from self
```

### State Change
```
Target becomes Frozen
Set target.frozen = true (if campaign supports boolean states)

Tile becomes impassable
target.tile.type = "wall"
```

### Resource Transfer
```
Transfer 5 gold to target
self.gold -= 5, target.gold += 5
```

## Writing Effects

**Template**:
```
Plain English description of change
Technical notation: resource.property operator value
```

**Be Explicit**:
- State exactly what changes
- Include calculations clearly
- Specify targets precisely

---

## See Also
- Chapter 14: Features
- Chapter 16: Actions
- Reference: Effect Template
