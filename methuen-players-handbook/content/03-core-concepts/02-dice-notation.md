# Dice Notation and Expressions

## Dice Notation

Methuen uses standard polyhedral dice notation with specific rules for calculation.

### Basic Notation

**Format**: `XdY`
- **X**: Number of dice to roll
- **d**: Separates quantity from die type
- **Y**: Number of sides on each die

**Examples**:
- `1d6`: Roll one six-sided die
- `2d10`: Roll two ten-sided dice, sum the results
- `3d4`: Roll three four-sided dice, sum the results

### Single Die Notation

When rolling one die, you may omit the "1":
- `d20` is equivalent to `1d20`
- `d6` is equivalent to `1d6`

## Expressions

**Definition**: An **expression** is a mathematical formula that combines dice rolls, resource values, and operators to calculate a result.

### Supported Operators

Methuen expressions support four operators:

1. **Addition** (`+`): Add values together
2. **Subtraction** (`-`): Subtract values
3. **Multiplication** (`*`): Multiply values
4. **Division** (`/`): Divide values (see special rules below)

### Operator Precedence

Standard mathematical order of operations applies:

1. Multiplication and division (left to right)
2. Addition and subtraction (left to right)
3. Use parentheses `()` to override precedence

**Example**: `2+3*4` equals `14`, not `20`

**Example**: `(2+3)*4` equals `20`
### Complex Expression Example

### Resource Injection
Actor resources can be injected into expressions using brackets. `[health]`
If no modifier is present, the injected resource is from the actor performing the action.
But there is no issue with being explicit for more complex cases. `[self health]`
There is not a finite set of ways to write modifiers, the only rule is that they are clear to players in any condition to what actor they are referencing.
It is best practice to include expanded definitions on "Resource Injection Access Modifiers" in the campaign

```
((1d6)+[accuracy])-((1d4/2)*([target dodge]))
```

**Step-by-step** (with example values):
1. Roll 1d6, get 4
2. Add self.accuracy (assume 3): `4+3 = 7`
3. Roll 1d4, get 3
4. Divide by 2: `3/2 = 1` (floor division)
5. Multiply by target.dodge (assume 2): `1*2 = 2`
6. Subtract: `7-2 = 5`
7. **Final result**: 5

## Special Rules

### Zero Division

Dividing by zero results in zero (not an error).

**Example**: `10/0 = 0`

### Negative Results

Final expressions values cannot produce negative values. Any calculation resulting in less than zero becomes zero.

**Example**: `5-8 = 0` (not -3)

**Example**: `[health] - 50` when health is 20 results in `0`

However, inner values may be negative. 

**Example**: `(5-8) + 4 = 1`


### Floor Division

Fractional results are floor-divided, keeping only the integer component.

**Example**: `7/2 = 3` (not 3.5)

**Example**: `1d4/2` rolled as 3 becomes `1`

### Multiple Dice in Expressions

Dice rolls within expressions are summed before applying operators.

**Example**: `2d6+3`
- Roll 2d6, get 4 and 5
- Sum: `4+5 = 9`
- Add 3: `9+3 = 12`

## Common Patterns

### Modified Roll
`1d20+[dex]`: Roll with resource bonus

### Contested Value
`[attack]-[target defense]`: Compare two resources

### Scaled Damage
`(1d6)*[power-level]`: Multiply random value by resource


Note that expressions are read-only. Anything that performs a persisting operation on a actor's resource is called an "Effect" and should be written with a `=` assignment operator.
---

## See Also

- **Chapter 1**: Actors and Resources - Understanding resource references
- **Chapter 5**: Taking Actions - Using expressions in action resolution
- **Appendix B**: Quick Reference - Expression syntax summary


Why don't we allow negative integers on final expression results? 
- To reduce complexity and the burden on campaign writers to test their expressions. For example, if a `damage` effect used an expression `[target health] -= 1d6+[strength]-(1d4+[target armor])`, This is a perfectly logical way to address armor and damage. However, if negative values were allowed there could be a chance for error that the damage effect actually increases a target's health with very high armor. This case would require a feature to not allow negative integers. Instead, we remove the ability to drop below zero in any calculation empowering campaign writers to know they're effects always adjust resources in the intended direction.

Why floor divide? 
- To simplify calculations. Resources may not be decimal numbers, there for fractional parts have no meaning to results.

Typically dividing by zero is undefined. Why do we equal zero?
- To avoid accidental zero division errors. It would be easy to write `1d20/1d10*[armor]`, but if armor is 0 we now need extra logic to handle that case. Instead, we cancel the division operation and place a 0.
