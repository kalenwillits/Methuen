# Effects

## What are Effects?

**Effects** are active changes to game state that occur when triggered by actions or features.

In actions, effects appear in the (do), (then), and (else) components. They can be written **inline** or defined as **reusable components** referenced with `#` notation.

## Effect Characteristics

- Occur at specific moments (not always active)
- Make explicit changes to game state
- Written as imperative commands
- Resolve immediately when triggered

## Effect Types

### Resource Modification
```
Deal 1d6 damage to target
[Target Health] -= 1d6

Gain 10 gold
[Gold] += 10
```

### Position Change
```
Move 3 spaces North
Move 3N

Push target 2 spaces away
Move target 2 spaces directly away
```

### State Change
```
Target becomes Frozen
Set [Target Frozen] = true (if campaign supports boolean states)

Tile becomes impassable
[Target Tile Type] = "wall"
```

### Resource Transfer
```
Transfer 5 gold to target
[Gold] -= 5, [Target Gold] += 5
```

## Writing Effects

**Inline Format**:
```
[Resource] operator value
```

**Component Format**:
```
Effect Name (Effect)
[Resource] operator value
```

**Be Explicit**:
- State exactly what changes
- Include calculations clearly
- Specify targets precisely
- Use [Resource] notation for resources

## Effect Components

Effects can be defined as reusable components:

```
Deal Standard Damage (Effect)
[Target Health] -= (1d6 + [Strength])

Reduce ActionPoints (Effect)
[ActionPoints] -= 1

Heal Self (Effect)
[Health] += 1d6

Gain Loot (Effect)
[Gold] += 1d4

Apply Burning (Effect)
[Target Burning] += 1

Increment Counter (Effect)
[Attacks Made] += 1
```

Then reference in actions:

```
Attack (Action)
if: Adjacent to target
do: #Deal Standard Damage
then: #Reduce ActionPoints

Harvest Crop (Action)
if: On farmland tile
do: #Gain Loot
then: #Increment Counter
```

**Benefits**:
- Consistency across similar actions
- Easier to balance and adjust
- Clearer action definitions
- Can be used in any action component (do, then, or else)

---

## See Also
- Chapter 14: Features
- Chapter 16: Actions
- Reference: Effect Template
