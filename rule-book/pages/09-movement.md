# Chapter 9: Movement

## 9.1 Overview

Movement allows actors to change their position on the map during encounters. Unlike some game systems, Methuen does not assume a universal movement speed or free movement each turn. Instead, movement is handled through actions and features, giving campaigns full control over mobility.

Most campaigns provide movement actions to all actors. This chapter describes how movement works regardless of how a campaign implements it.

## 9.2 Movement Fundamentals

### 9.2.1 Movement as Actions

Movement in Methuen is provided by campaigns, not built into the core framework. This design choice allows campaigns to create varied movement systems. Actors can move when:
- The campaign defines a movement action for them (most common)
- A feature grants movement capability
- An effect causes forced movement

**Note**: Nearly all campaigns provide basic movement. If you are creating a campaign, see Section 9.3 for common movement patterns you can adopt.

### 9.2.2 Movement Costs

Movement actions typically consume resources:
- Action Points
- Movement Points (a dedicated resource)
- Turn-limited uses
- Other campaign-defined costs

## 9.3 Common Movement Patterns

Most campaigns provide movement actions to all actors. Here are common patterns campaigns use:

```
Movement Options Diagram (from tile marked @)

Cardinal Movement (cost: 1 each):
    N
  W @ E
    S

Diagonal Movement (cost: 1.5 each, see Chapter 8):
  NW   NE
    \ /
     @
    / \
  SW   SE

Typical 3-Tile Movement Range:
    . . N . .
    . . | . .
    NW--@--NE
    . . | . .
    . . S . .

With 3 movement, actor can reach any
adjacent tile or tiles 2-3 cardinal
steps away, accounting for diagonal costs.
```

Campaigns typically implement one of these movement systems:

### 9.3.1 Fixed Movement

All actors move a fixed number of tiles per movement action.

```
Move
do: Move actor up to 3 tiles
then: [Moves Per Turn] -= 1
```

**Characteristics**:
- Predictable movement ranges
- Simple to track
- No resource dependency

### 9.3.2 Resource-Based Movement

Movement distance is determined by a resource value.

```
Agile Movement
do: Move actor up to [Agility] tiles
then: [Moves Per Turn] -= 1
```

**Characteristics**:
- Variable movement by actor
- Allows movement enhancement through resource modification
- Enables movement reduction effects

### 9.3.3 Action Point Movement

Each tile of movement costs action points.

```
Step
do: Move actor 1 tile
then: [Action Points] -= 1
```

**Characteristics**:
- Fine-grained movement control
- Movement competes with other actions for resources
- Tactical trade-offs between movement and action

### 9.3.4 Free Movement Phase

Movement occurs as a separate phase, not consuming actions.

```
Feature: Movement Phase
At the start of each actor's turn, before actions,
the actor may move up to [Speed] tiles.
```

**Characteristics**:
- Guaranteed movement each turn
- Actions remain fully available
- Separates tactical decisions

## 9.4 Diagonal Movement

### 9.4.1 Distance Calculation

When moving diagonally, the distance factor of 1.5 (rounded up) applies to movement costs.

| Movement | Cardinal Cost | Diagonal Cost |
|----------|---------------|---------------|
| 1 tile | 1 | 2 |
| 2 tiles | 2 | 3 |
| 3 tiles | 3 | 5 |

### 9.4.2 Application Example

```
Actor has 5 movement points.

Cardinal movement only:
  Can move up to 5 tiles in any cardinal direction.

Diagonal movement only:
  1 diagonal = 2 points (3 remaining)
  2 diagonals = 3 points (2 remaining)
  3 diagonals = 5 points (0 remaining)
  Maximum: 3 diagonal tiles

Combined movement:
  2 cardinal (2 points) + 1 diagonal (2 points) = 4 points spent
  Remaining: 1 point (1 more cardinal tile possible)
```

### 9.4.3 Campaign Variations

Campaigns may modify diagonal costs through Features:

```
Feature: Simplified Diagonals
Diagonal movement costs the same as cardinal movement.
```

```
Feature: True Distance
Diagonal movement costs 1.41 tiles (round to nearest).
```

## 9.5 Movement Restrictions

### 9.5.1 Impassable Tiles

Actors cannot enter impassable tiles. If a movement path would cross an impassable tile, the actor must find an alternate route.

### 9.5.2 Difficult Terrain

Difficult terrain increases movement costs:

```
Feature: Difficult Terrain
Movement into this tile costs double the normal amount.
```

**Example**:
```
Actor moves 2 tiles, second tile is difficult terrain.
Normal cost: 2
Difficult terrain cost: 1 + 2 = 3
```

### 9.5.3 Occupied Tiles

By default, actors may share tiles with other actors. Campaigns may restrict this:

```
Feature: No Stacking
Actors cannot enter tiles occupied by opposing actors.
Actors may move through tiles occupied by allied actors
but cannot end movement there.
```

### 9.5.4 Movement Through Enemies

Campaigns may permit or prohibit movement through enemy-occupied tiles:

```
Feature: Engagement
Actors cannot move through tiles occupied by enemy actors
unless using a special movement type (Fly, Teleport, etc.).
```

## 9.6 Movement Types

### 9.6.1 Standard Movement

Normal movement along the ground, subject to terrain and obstacles.

### 9.6.2 Flying Movement

Movement that ignores ground-based obstacles:

```
Feature: Flying
This actor ignores difficult terrain and may move
over impassable ground tiles. The actor must end
movement on a valid tile.
```

### 9.6.3 Teleportation

Instantaneous relocation ignoring intervening space:

```
Teleport
do: Move actor to target tile within 5 tiles
then: [Mana] -= 10

Note: Teleportation ignores line of sight, difficult
terrain, and obstacles. Target tile must be valid.
```

### 9.6.4 Burrowing Movement

Movement through solid obstacles:

```
Feature: Burrow
This actor may move through impassable ground tiles.
The actor cannot end movement in an impassable tile.
```

### 9.6.5 Swimming Movement

Movement through water tiles:

```
Feature: Swim
This actor treats water tiles as passable.
```

## 9.7 Forced Movement

### 9.7.1 Definition

**Forced Movement** occurs when an actor is moved by an effect rather than their own action. Forced movement:
- Does not consume the affected actor's resources
- May ignore the actor's normal movement restrictions
- Is typically caused by another actor's action

### 9.7.2 Push

Push moves the target directly away from the source:

```
Shield Bash
if: 1d20 + [Strength] >= [Target Defense]
do: [Target Health] -= 1d6
    Push target 2 tiles away from actor
then: [Action Points] -= 1
```

### 9.7.3 Pull

Pull moves the target directly toward the source:

```
Grappling Hook
if: 1d20 + [Dexterity] >= [Target Defense]
do: Pull target up to 3 tiles toward actor
then: [Action Points] -= 1
```

### 9.7.4 Slide

Slide moves the target in a direction chosen by the source:

```
Telekinetic Shove
if: 1d20 + [Will] >= [Target Will]
do: Slide target 2 tiles in any direction
then: [Action Points] -= 1
```

### 9.7.5 Forced Movement Restrictions

Unless otherwise specified:
- Forced movement cannot push actors into impassable tiles
- If forced movement would push an actor into an impassable tile, the movement stops at the last valid tile
- Forced movement may trigger tile events (entering hazards, etc.)

## 9.8 Movement and Heading

### 9.8.1 Heading Changes

By default, changing heading (facing direction) does not cost movement:

```
An actor at 0N 0E facing North may:
1. Turn to face East (no cost)
2. Move 3 tiles East
Total movement cost: 3 tiles
```

### 9.8.2 Heading Restrictions

Campaigns may impose heading costs:

```
Feature: Facing Matters
Changing heading by 45 degrees costs 1 movement.
Changing heading by 90 degrees costs 2 movement.
Changing heading by 135+ degrees costs 3 movement.
```

### 9.8.3 Movement Direction and Heading

Movement does not automatically change heading. After moving, an actor retains their previous heading unless they explicitly change it or a Feature requires alignment.

## 9.9 Movement Reactions

### 9.9.1 Opportunity Actions

Campaigns may define reactions triggered by movement:

```
Opportunity Attack (Reaction)
Trigger: An adjacent enemy moves away from this actor
if: 1d20 + [Attack] >= [Target Defense]
do: [Target Health] -= 1d6
then: [Reaction Points] -= 1
```

### 9.9.2 Movement Interruption

Some reactions may interrupt movement:

```
Intercept (Reaction)
Trigger: An enemy moves within 2 tiles of this actor
do: This actor may move up to 2 tiles toward the enemy.
    Movement is then interrupted.
then: [Reaction Points] -= 1
```

### 9.9.3 Safe Movement

Campaigns may define movement that avoids reactions:

```
Careful Step
do: Move actor 1 tile without provoking reactions
then: [Action Points] -= 1
```

```
Disengage
do: Until end of turn, this actor's movement does not
    provoke opportunity attacks
then: [Action Points] -= 1
```

## 9.10 Movement Procedure

To execute movement:

1. **Declare movement action**: Actor announces the movement action being used
2. **Determine movement allowance**: Calculate available movement based on action/resources
3. **Plot path**: Determine the path from current location to destination
4. **Calculate costs**: Sum movement costs for each tile (including terrain modifiers)
5. **Verify validity**: Confirm path is valid (no impassable tiles, sufficient movement)
6. **Execute movement**: Move the actor along the path
7. **Resolve triggers**: Process any events or reactions triggered by movement
8. **Update position**: Record new location
9. **Update heading**: If heading changed, record new heading
10. **Pay costs**: Deduct movement costs from resources
