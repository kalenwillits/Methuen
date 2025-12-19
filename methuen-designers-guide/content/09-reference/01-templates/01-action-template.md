# Action Template

```
Action Name: _______________
Range: _______________
Target: _______________

if: Check expression `1dx > 1dy`
do: Action/inline Effect
then: Action/inline Effect
else: Action/inline Effect
```

## Example

```
Action Name: Harvest Crop
Range: Adjacent tile
Target: Single tile

if: Target is "Farmland" type AND target.cropGrowth > 5
do: self.actionPoints -= 1
then: self.food += target.cropGrowth, target.cropGrowth = 0
else: (no effect)
```
