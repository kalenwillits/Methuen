# Chapter 3: Dice and Expressions

## 3.1 Overview

Dice and Expressions form the randomization and calculation system for Methuen. All variable outcomes in the framework derive from dice rolls, and all calculations use the Expression system.

## 3.2 Dice Notation

### 3.2.1 Basic Format

Dice notation follows the format `XdY`:

| Component | Description |
|-----------|-------------|
| X | Number of dice to roll (positive integer) |
| d | Literal separator character |
| Y | Number of sides per die (positive integer) |

### 3.2.2 Notation Rules

1. **Standard notation**: `XdY` rolls X dice, each with Y sides, and sums the results.
2. **Implied single die**: When X is omitted, it defaults to 1. Thus `d20` is equivalent to `1d20`.
3. **Minimum values**: Both X and Y must be at least 1. A roll of `0d6` produces 0. A roll of `1d0` is invalid.

### 3.2.3 Common Dice Types

| Notation | Description | Range |
|----------|-------------|-------|
| d4 | Four-sided die | 1-4 |
| d6 | Six-sided die | 1-6 |
| d8 | Eight-sided die | 1-8 |
| d10 | Ten-sided die | 1-10 |
| d12 | Twelve-sided die | 1-12 |
| d20 | Twenty-sided die | 1-20 |
| d100 | Percentile die | 1-100 |

### 3.2.4 Multiple Dice

When rolling multiple dice, each die is rolled independently and the results are summed.

**Example**:

> Renna the Archer uses Power Shot, which deals `3d6` damage.
>
> She picks up three six-sided dice and rolls them.
> - First die: 4
> - Second die: 2
> - Third die: 5
> - Total: 4 + 2 + 5 = 11 damage

### 3.2.5 Statistical Properties

| Notation | Minimum | Maximum | Average |
|----------|---------|---------|---------|
| 1d6 | 1 | 6 | 3.5 |
| 2d6 | 2 | 12 | 7 |
| 3d6 | 3 | 18 | 10.5 |
| 1d20 | 1 | 20 | 10.5 |
| 1d100 | 1 | 100 | 50.5 |

General formula for XdY:
- Minimum: X
- Maximum: X * Y
- Average: X * (Y + 1) / 2

## 3.3 Expressions

### 3.3.1 Definition

An **Expression** is a mathematical formula that combines dice rolls, resource values, literal numbers, and arithmetic operators to calculate a result. All Expressions evaluate to a non-negative integer.

**Note**: Some materials use the term "dice-expression" interchangeably with Expression. This Rule Book uses Expression as the standard term.

### 3.3.2 Expression Components

Expressions may contain:

1. **Dice notation**: `1d6`, `2d10`, `d20`
2. **Literal integers**: `5`, `10`, `100`
3. **Resource injections**: `[Health]`, `[Strength]`
4. **Arithmetic operators**: `+`, `-`, `*`, `/`
5. **Parentheses**: `(`, `)` for grouping

### 3.3.3 Arithmetic Operators

| Operator | Name | Description |
|----------|------|-------------|
| + | Addition | Adds two values |
| - | Subtraction | Subtracts right value from left value |
| * | Multiplication | Multiplies two values |
| / | Division | Divides left value by right value |

### 3.3.4 Order of Operations

Expressions follow standard mathematical order of operations:

1. Parentheses (innermost first)
2. Multiplication and Division (left to right)
3. Addition and Subtraction (left to right)

**Example**: `2 + 3 * 4`
- Multiply: 3 * 4 = 12
- Add: 2 + 12 = 14
- Result: 14

**Example**: `(2 + 3) * 4`
- Parentheses: 2 + 3 = 5
- Multiply: 5 * 4 = 20
- Result: 20

## 3.4 Resource Injection

### 3.4.1 Syntax

Resource values are injected into Expressions using square bracket notation: `[ResourceName]`

### 3.4.2 Resolution Context

When an Expression contains a resource reference, the value is drawn from the current context:

| Reference | Source |
|-----------|--------|
| `[ResourceName]` | The acting actor's resource value |
| `[Target ResourceName]` | The target actor's resource value |
| `[Self ResourceName]` | Explicitly the acting actor's resource value |

### 3.4.3 Examples

**Example 1**: Basic resource injection

> Kira the Fighter attacks a Goblin. Her Strike action deals `1d6 + [Strength]` damage.
>
> Kira's Strength is 4. She rolls 1d6 and gets 3.
>
> Damage calculation: 3 + 4 = 7 damage to the Goblin.

**Example 2**: Target resource reference

> The Vampire's Life Drain deals damage equal to `[Target Health] / 2`.
>
> The target Villager has 15 Health.
>
> Damage calculation: 15 / 2 = 7 (rounded down).

**Example 3**: Complex Expression

> Magnus the Battlemage uses Empowered Strike: `(1d8 + [Strength]) * 2 - [Target Defense]`
>
> Magnus's Strength: 4
> Target's Defense: 3
> Roll 1d8: 6
>
> Calculation:
> - Inner parentheses: 6 + 4 = 10
> - Multiplication: 10 * 2 = 20
> - Subtraction: 20 - 3 = 17
>
> Result: 17 damage

## 3.5 Special Resolution Rules

### 3.5.1 Division by Zero

Division by zero produces a result of zero rather than an error.

```
Expression: 10 / 0
Result: 0
```

This rule prevents game-halting errors when resource values unexpectedly reach zero.

### 3.5.2 Fractional Results

All division operations round down to the nearest integer (floor division).

```
Expression: 7 / 2
Calculation: 7 / 2 = 3.5
Result: 3 (rounded down)
```

```
Expression: 1 / 3
Calculation: 1 / 3 = 0.333...
Result: 0 (rounded down)
```

### 3.5.3 Negative Intermediate Values

Subtraction may produce negative intermediate values during calculation. These intermediate values are not clamped to zero. However, the final Expression result is always clamped to a minimum of zero.

**Example**: Negative intermediate, positive final
```
Expression: (5 - 8) + 10
Calculation:
  - Parentheses: 5 - 8 = -3 (intermediate, not clamped)
  - Addition: -3 + 10 = 7
Result: 7
```

**Example**: Negative final result
```
Expression: 5 - 8
Calculation: 5 - 8 = -3
Result: 0 (clamped to minimum)
```

**Example**: Negative intermediate, negative final
```
Expression: (5 - 8) + 2
Calculation:
  - Parentheses: 5 - 8 = -3 (intermediate)
  - Addition: -3 + 2 = -1
Result: 0 (clamped to minimum)
```

### 3.5.4 Zero Dice Rolls

Rolling zero dice (`0dY`) produces a result of zero.

```
Expression: 0d6
Result: 0
```

## 3.6 Expression Evaluation Procedure

To evaluate an Expression, follow this procedure:

1. **Substitute resource values**: Replace all `[ResourceName]` references with their current integer values.
2. **Roll all dice**: Replace all dice notation with rolled results.
3. **Evaluate parentheses**: Resolve innermost parentheses first, working outward.
4. **Apply multiplication and division**: Evaluate left to right, rounding division down.
5. **Apply addition and subtraction**: Evaluate left to right, allowing negative intermediates.
6. **Clamp final result**: If the final result is negative, set it to zero.

### 3.6.1 Worked Example

> Theron the Wizard casts Arcane Bolt, dealing `(2d6 + [Intelligence]) * 2 - [Target Defense] + 5` damage.
>
> Given:
> - Theron's Intelligence: 4
> - Target's Defense: 12
> - First d6 roll: 3
> - Second d6 roll: 5
>
> Step 1 - Substitute resources:
> `(2d6 + 4) * 2 - 12 + 5`
>
> Step 2 - Roll dice (2d6 = 3 + 5 = 8):
> `(8 + 4) * 2 - 12 + 5`
>
> Step 3 - Evaluate parentheses:
> `12 * 2 - 12 + 5`
>
> Step 4 - Multiplication/Division:
> `24 - 12 + 5`
>
> Step 5 - Addition/Subtraction (left to right):
> `24 - 12 = 12`
> `12 + 5 = 17`
>
> Step 6 - Final result:
> 17 (positive, no clamping needed)
>
> Theron deals 17 damage.

## 3.7 Checks (Boolean Expressions)

### 3.7.1 Definition

A **Check** is a boolean expression that evaluates to either true or false. Checks are used to determine conditional outcomes in actions, scenes, and features.

**Note**: Some materials use the term "dice-check" interchangeably with Check. This Rule Book uses Check as the standard term.

### 3.7.2 Check Format

Checks compare two Expressions using a comparison operator:

```
[Expression] [Operator] [Expression]
```

### 3.7.3 Comparison Operators

| Operator | Meaning |
|----------|---------|
| = | Equal to |
| != | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

### 3.7.4 Check Examples

**Example 1**: Attack roll

> Sera the Knight attacks a Goblin Warrior. The Check is `1d20 + [Attack] >= [Target Defense]`.
>
> Sera's Attack: 6
> Goblin's Defense: 12
> Roll 1d20: 8
>
> Evaluation: 8 + 6 = 14 >= 12
> Result: TRUE (hit!)

**Example 2**: Resource threshold

> A healing potion's Check: `[Health] < [Health Maximum]`
>
> Actor's Health: 15
> Actor's Health Maximum: 20
>
> Evaluation: 15 < 20
> Result: TRUE (healing can occur)

**Example 3**: Contested roll

> An arm wrestling contest: `1d20 + [Strength] > [Target Strength] + 1d20`
>
> Actor's Strength: 5, rolls 14
> Target's Strength: 4, rolls 12
>
> Evaluation: 14 + 5 = 19 > 4 + 12 = 16
> Result: TRUE (actor wins)

## 3.8 Expression Notation Summary

| Notation | Meaning | Example |
|----------|---------|---------|
| XdY | Roll X dice with Y sides | 2d6 |
| dY | Roll 1 die with Y sides | d20 |
| [Name] | Inject actor's resource value | [Strength] |
| [Target Name] | Inject target's resource value | [Target Health] |
| + - * / | Arithmetic operators | 1d6 + 3 |
| ( ) | Grouping | (1d6 + 2) * 3 |
