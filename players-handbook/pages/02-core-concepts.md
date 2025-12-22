# Core Concepts

## Actors

An **actor** is any named entity in the game—your character, enemies, NPCs, or environmental elements.

Every actor has:

**Name**
Unique identifier (e.g., "Raven", "Goblin Scout")

**Location**
Grid coordinates showing position (e.g., 3N 2E means 3 spaces North, 2 spaces East from origin)

**Heading**
Direction faced: N, NE, E, SE, S, SW, W, NW

**Resources**
Numerical values tracking everything important (see Resources below)

**Actions**
Operations the actor can perform

## Resources

A **resource** is any value represented as a positive integer (0 or higher).

Resources measure:
- **Capabilities**: Strength, Dexterity, Intelligence
- **States**: Health, Energy, Focus
- **Currencies**: Gold, Materials, Ammunition
- **Counters**: Actions Remaining, Turns Survived

### Resource Rules

**Resources are always ≥ 0**
Cannot drop below zero. If an operation would make a resource negative, it becomes 0 instead.

**Resources are whole numbers**
No fractions. Division results are rounded down.

**Resources start at 0 by default**
Unless your campaign specifies otherwise.

**All actors have access to all resources**
Your campaign defines what resources exist. Every actor can use every resource, but values differ per actor.

### Initialization

Resources don't need to be recorded until first used. When a resource appears in gameplay:

1. Check if your campaign defines an initialization rule
2. If yes, apply it (roll dice, calculate from other resources)
3. If no, the resource starts at 0
4. Record the value on your character sheet

**Example**: An enemy deals damage to your Health, but you haven't initialized Health yet. Check your campaign book. It says "Health = 1d20 + Constitution". You roll 15, add your Constitution of 12, and record "Health: 27". Then subtract the damage.

### Resource Maximums

Some resources have maximum values. Campaigns define these using Features (special rules).

**Example Feature**:
```
Health Maximum
Health cannot exceed its initial rolled value
```

Common resources with maximums:
- Health (prevents infinite healing)
- Energy (limits resource regeneration)
- ActionPoints (often capped at 3)

Resources without maximums:
- Gold (accumulates indefinitely)
- Counters (no upper bound)

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

### Special Rules

**Division by zero = 0**
`10/0` equals `0`

**Negative results = 0**
`5 - 8` equals `0` (not -3)

**Fractions round down**
`7/2` equals `3` (not 3.5)

## Grid and Movement

### Directions

**Cardinals**: N, E, S, W
**Diagonals**: NE, SE, SW, NW

### Position Notation

`3N 2E` means 3 spaces North, 2 spaces East from origin

### Distance

**Adjacent**: 1 space away (cardinal or diagonal)
**Range**: Number of spaces between actors

### Movement Costs

Defined by your campaign. Common patterns:
- Cardinal movement: 1 point
- Diagonal movement: 1.5 points (rounded up)

## Campaigns

A **campaign** is the collection of content that defines your specific game.

Campaigns define:
- Which resources exist and how they initialize
- What actions actors can perform
- How movement and initiative work
- Maps and encounters
- Victory conditions

**The Framework** (this handbook) provides core rules.
**The Campaign** (campaign book) provides specific content.
