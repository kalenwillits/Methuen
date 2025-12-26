## Dice and Expressions

### Dice Notation

**Format**: `XdY`
- X = number of dice
- d = separator
- Y = number of sides

**Examples**:
- `1d6` = roll one six-sided die
- `2d10` = roll two ten-sided dice and add them
- `3d4` = roll three four-sided dice and add them

You can omit the "1": `d20` means `1d20`

### Expressions

An **expression** combines dice, resources, and math operators to calculate a result.

**Operators**:
- Addition: `+`
- Subtraction: `-`
- Multiplication: `*`
- Division: `/`

**Order of operations**: Multiplication and division before addition and subtraction. Use parentheses to override.

**Resource injection**: Use brackets `[]` to insert resource values.
- `[Health]` = your Health value
- `[Target Health]` = target's Health value

**Example**: `1d6 + [Strength]`
- Roll 1d6, get 4
- Add your Strength of 3
- Result: 7

### Special Rules When Resolving Dice Notation

**Division by zero = 0**
`10/0` equals `0`

**Fractions round down**
`7/2` equals `3` (not 3.5)

**Negative results on final evaluation= 0**
`(5 - 8)` equals `0`, *not -3*.
`(5 - 8) + 4` equals `1`, *5 - 8 is -3, plus 4 leads the final evaluation of 1* 


## Grid and Movement

### Directions

**Cardinals**: N, E, S, W
**Diagonals**: NE, SE, SW, NW

### Position Notation

`3N 2E` means 3 spaces North, 2 spaces East from origin

