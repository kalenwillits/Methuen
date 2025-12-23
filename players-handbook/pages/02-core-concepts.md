# Core Concepts

## Actors

An **actor** is any named entity in the game—your character, enemies, objects,
or environmental elements.

Every actor has:

**Name**
Unique identifier

**Location**
Grid coordinates showing during an encounter(e.g., 3N 2E means 3 spaces North, 2 spaces East from origin)

**Heading**
Direction the actor is facing: N, NE, E, SE, S, SW, W, NW

**Resources**
Numerical values tracking qualities for an actor.

**Actions**
Operations the actor can perform

## Casts
Casts are groups of actors controlled by a single player or *strategy* that
share the same initiative. Turn order within a cast is up to the controlling
player.  For casts controlled by a strategy, a *sub-initiate* will need to be
used.

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
Unless your campaign defines a feature that initializes the resource differently.

**All actors have access to all resources**
Your campaign defines what resources exist within the world. Every actor
implicitly has a value for every resource. But not all actors need to track
every resource if they don't use them. These untracked resources are `unkown`
until used. Then they are initialized and recorded for that actor. This is called *lazy initialization*.

**Lazy Initialization**
1. Check if your campaign defines an initialization rule for a given resource.
2. If yes, apply it (roll dice, calculate from other resources)
3. If no, the resource starts at 0
4. Record the value for the actor.

**Example**: An enemy deals damage to your Health, but you haven't initialized Health yet. Check your campaign book. It says "Health = 1d20 + Constitution". You roll 15, add your Constitution of 12, and record "Health: 27". Then subtract the damage.

### Resource Maximums

Some resources have maximum values. Campaigns define these using Features (special rules).

**Example Feature**:
```
Health Maximum
Health cannot exceed its initial rolled value
```

Common resources and features:
- Health (prevents infinite healing)
- Energy (limits resource regeneration)
- Action Points (Resets to 3 at the start of an actor's turn)

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

### Distance

**Adjacent**: 1 space away (cardinal or diagonal)
**Range**: Number of spaces between actors
Across the grid on direct cardinal directions, (North, East, South, West), is
measured as one space. Measuring diagonally, (North-East, North-West,
South-East, South-West), is measured by a factor of **1.5** rounded up.
This is a simplification of the Pythagorean theorem, given a (1, 1) square
would result in a diagonal distance of 1.41421.

### Actor Movement 
*Movement* is not directly defined in the Methuen framework and requires an
action to be defined by the campaign for actors to move at all. Some common
patterns are:
- A fixed movement system:
```
Fixed Movement
do: Move an actor 3 spaces
then: [Moves Per Turn] -= 1
```
- Resource based movement system:
```
Agile Movement
do: Move an actor [Agility] spaces
then: [Moves Per Turn] -= 1
```

## Scenes
A scene a textual-based interaction presented to players in the campaign. A
scene can contain narrative for role-playing that lead to *checks* or choices
determining how or what next encounter the players will lead into.
Not all campaigns will have multiple encounters, such as strategical war games
that span many actors of one encounter. However, all campaigns must have a
*setup* scene that guide's it's players through creating the first actors
required for the first encounter.

## Encounters
Encounters are actors on a grid. Each actor or *cast* of actors will take
turns where they can perform actions. 
