# Chapter 8: Maps and Tiles

## 8.1 Overview

Maps define the spatial environment for encounters. They provide the grid system for actor positioning, movement, and range calculations.

## 8.2 Map Definition

### 8.2.1 Formal Definition

A **Map** is a grid-based graph that:
- Defines the spatial layout for an encounter
- Contains tiles organized in a regular pattern
- May include regions, features, and events
- Serves as the foundation for all spatial mechanics

### 8.2.2 Map Properties

| Property | Description |
|----------|-------------|
| Name | Identifier for the map |
| Dimensions | Width and height in tiles |
| Origin | Reference point for coordinate system |
| Tiles | Individual grid squares |
| Regions | Named groups of tiles |
| Features | Special rules affecting the map |

## 8.3 Grid System

### 8.3.1 Grid Structure

Maps use a square grid system. Each square in the grid is a tile, and tiles are arranged in rows and columns.

```
   W <---+---> E
         |
    +----+----+----+----+
    |    |    |    |    |
  N +----+----+----+----+
  ^ |    |    | O  |    |   O = Origin
  | +----+----+----+----+
  | |    |    |    |    |
  v +----+----+----+----+
  S |    |    |    |    |
    +----+----+----+----+
```

### 8.3.2 Coordinate System

Locations on the map are expressed relative to the origin using cardinal directions.

**Format**: `[X][Direction] [Y][Direction]`

**Examples**:
| Notation | Meaning |
|----------|---------|
| `0N 0E` | The origin |
| `3N 2E` | 3 tiles north, 2 tiles east of origin |
| `1S 4W` | 1 tile south, 4 tiles west of origin |
| `0N 3E` | Same row as origin, 3 tiles east |

### 8.3.3 Origin Placement

The origin is a reference point, not necessarily a corner. Campaigns specify origin placement. Common placements:
- Center of the map
- Southwest corner
- A tactically significant location

## 8.4 Tiles

### 8.4.1 Tile Definition

A **Tile** is a single square unit of the map grid. Each tile has:

| Property | Description |
|----------|-------------|
| Location | Coordinate position on the map |
| Features | Special rules affecting the tile |
| Events | Triggers that activate under conditions |
| Occupants | Actors currently on the tile |

### 8.4.2 Tile States

Tiles may exist in various states:

**Passable**: Actors can enter and occupy the tile.

**Impassable**: Actors cannot enter the tile. Examples:
- Walls
- Deep water (for non-swimming actors)
- Solid obstacles

**Occupied**: Contains one or more actors. By default, multiple actors may share a tile. Campaigns may restrict this with Features.

**Blocked**: Line of sight cannot pass through the tile.

### 8.4.3 Tile Features

Tiles may have features that affect actors or actions:

```
Feature: Difficult Terrain
Movement into this tile costs double movement.
```

```
Feature: Cover
Actors on this tile gain +2 Defense against ranged attacks.
```

```
Feature: Hazardous
Actors entering or starting their turn on this tile
take 1d6 damage.
```

### 8.4.4 Tile Events

Events trigger when specific conditions are met:

```
Event: Pressure Plate
Trigger: An actor enters this tile
Effect: Begin Scene "Trap Activated"
```

```
Event: Exit Point
Trigger: A player actor ends their turn on this tile
Effect: Encounter ends with victory
```

## 8.5 Regions

### 8.5.1 Region Definition

A **Region** is a named collection of tiles that share common properties. Regions simplify map design by applying features and events to multiple tiles at once.

### 8.5.2 Region Properties

| Property | Description |
|----------|-------------|
| Name | Identifier for the region |
| Tiles | List of tiles belonging to the region |
| Features | Special rules for all tiles in the region |
| Events | Triggers for the region |

### 8.5.3 Region Examples

```
Region: Lava Field
Tiles: All tiles from 2N 3W to 5N 1E
Features:
  - Hazardous (2d6 fire damage)
  - Impassable to non-flying actors
```

```
Region: Forest
Tiles: [3N 2E], [3N 3E], [4N 2E], [4N 3E]
Features:
  - Difficult Terrain
  - Provides Cover
  - Blocks line of sight
```

### 8.5.4 Overlapping Regions

Tiles may belong to multiple regions. When regions overlap:
- All applicable features apply
- Events trigger independently
- Conflicting effects are resolved by specificity (more specific wins)

## 8.6 Distance Measurement

### 8.6.1 Cardinal Distance

Movement or measurement along cardinal directions (N, E, S, W) counts 1 tile per space moved.

```
Actor at 0N 0E moving to 3N 0E:
Distance: 3 tiles
```

### 8.6.2 Diagonal Distance

Movement or measurement along diagonal directions (NE, SE, SW, NW) uses a cumulative calculation with a factor of 1.5, rounded up at the end.

**Diagonal Movement Cost Calculation**:
1. Count the total number of diagonal tiles moved
2. Multiply by 1.5
3. Round up to the nearest whole number
4. This is the total movement cost in tiles

| Diagonal Tiles | Calculation | Movement Cost |
|----------------|-------------|---------------|
| 1 | 1 x 1.5 = 1.5 | 2 tiles |
| 2 | 2 x 1.5 = 3.0 | 3 tiles |
| 3 | 3 x 1.5 = 4.5 | 5 tiles |
| 4 | 4 x 1.5 = 6.0 | 6 tiles |
| 5 | 5 x 1.5 = 7.5 | 8 tiles |
| 6 | 6 x 1.5 = 9.0 | 9 tiles |

**Example**: An actor moves 3 tiles diagonally (NE, NE, NE).
- Diagonal tiles: 3
- Calculation: 3 x 1.5 = 4.5
- Rounded up: 5
- Movement cost: 5 tiles

**Important**: This is a cumulative calculation applied to the total diagonal movement, not calculated per tile. You do not pay 2 tiles for each diagonal move; instead, you pay 1.5 tiles per diagonal (rounded at the end).

### 8.6.3 Combined Distance

For paths combining cardinal and diagonal movement, calculate each component and sum:

```
Actor at 0N 0E moving to 3N 2E:
  Option A (3 north, then 2 east): 3 + 2 = 5 tiles
  Option B (2 diagonal NE, then 1 north): 3 + 1 = 4 tiles
```

Actors may choose any valid path; shortest distance is typically used for range calculations.

**Detailed Example of Combined Movement**:

> An actor wants to move from 0N 0E to 4N 3E.
>
> **Path**: 3 diagonal moves (NE, NE, NE) then 1 cardinal move (N)
>
> **Calculation**:
> - Diagonal cost: 3 x 1.5 = 4.5, rounded up = 5 tiles
> - Cardinal cost: 1 tile
> - Total cost: 5 + 1 = 6 tiles
>
> If the actor has 6 movement, they can complete this path.

### 8.6.4 Range Calculation

To calculate range between two actors:
1. Determine the shortest path in tiles
2. Apply diagonal distance factor for any diagonal movement
3. The result is the range in tiles

**Example**:
```
Actor A at 0N 0E
Actor B at 3N 3E

Shortest path: 3 diagonal moves
Distance: 3 x 1.5 = 4.5, rounded up = 5 tiles
Range: 5
```

**Range Quick Reference**:

For targets at equal distance north/south and east/west (pure diagonal):

| Position | Diagonal Tiles | Range |
|----------|----------------|-------|
| 1N 1E | 1 | 2 |
| 2N 2E | 2 | 3 |
| 3N 3E | 3 | 5 |
| 4N 4E | 4 | 6 |
| 5N 5E | 5 | 8 |

### 8.6.5 Adjacency

Two tiles are **adjacent** if they share an edge (cardinal adjacent) or corner (diagonal adjacent). Adjacent tiles are within range 1 of each other.

| Adjacency Type | Positions | Range |
|----------------|-----------|-------|
| Cardinal | N, E, S, W | 1 |
| Diagonal | NE, SE, SW, NW | 1 |

All adjacent tiles are considered range 1 for game mechanics, despite diagonal tiles being geometrically farther.

## 8.7 Line of Sight

### 8.7.1 Definition

**Line of Sight** (LoS) determines whether one actor can see another. Many actions require line of sight to the target.

### 8.7.2 Determination

To determine line of sight:
1. Draw an imaginary line from the center of the actor's tile to the center of the target's tile
2. If the line passes through any blocking tile, line of sight is blocked
3. If the line passes through only non-blocking tiles, line of sight exists

### 8.7.3 Blocking Conditions

Line of sight is blocked by:
- Walls and solid obstacles
- Certain terrain features (as specified)
- Large actors (if specified by campaign)

Line of sight is NOT blocked by:
- Other actors (by default)
- Transparent obstacles (windows, etc.)
- Low obstacles (unless specified)

### 8.7.4 Partial Cover

When line of sight passes along the edge of blocking terrain:
- Line of sight exists
- The target may have cover (bonus to Defense)
- Specific cover rules are defined by campaign Features

## 8.8 Map Features

### 8.8.1 Global Map Features

Features that apply to the entire map:

```
Feature: Darkness
All actors have maximum visibility of 3 tiles
unless they have Darkvision.
```

```
Feature: Unstable Ground
At the end of each round, roll 1d6. On a 1,
a random passable tile becomes impassable.
```

### 8.8.2 Environmental Features

Features representing environmental conditions:

| Feature | Effect |
|---------|--------|
| Fog | Maximum visibility 5 tiles |
| Rain | Ranged attacks have -2 to hit |
| Wind | Movement costs +1 per tile |
| Ice | Actors must make checks to avoid falling |

## 8.9 Map Events

### 8.9.1 Event Triggers

Events on maps may trigger based on:
- Actor entry (stepping on a tile)
- Actor exit (leaving a tile)
- Turn start (actor begins turn on tile)
- Turn end (actor ends turn on tile)
- Action use (action performed on or from tile)
- Time (specific round number)

### 8.9.2 Event Effects

Events may cause:
- Scene interruption (pause encounter, run scene)
- Deployment (spawn new actors)
- Feature activation (apply new features)
- Resource modification (damage, healing, etc.)
- Map changes (terrain alteration)

### 8.9.3 Event Example

```
Event: Reinforcement Arrival
Trigger: Round 3 begins
Effect:
  1. Deploy Goblin Warrior x2 at tiles 5N 1E, 5N 2E
  2. Add deployed actors to Enemy cast
  3. Roll sub-initiative for new actors
```

## 8.10 Map Visualization

### 8.10.1 Requirements

Campaigns must ensure:
- Tiles with special features are clearly identifiable
- Regions are visually distinguishable
- Events locations are marked (if known to players)
- Impassable terrain is obvious

### 8.10.2 Notation Conventions

Common map notation:

| Symbol | Meaning |
|--------|---------|
| . | Passable tile |
| # | Wall/Impassable |
| ~ | Water |
| ^ | Difficult terrain |
| * | Hazard |
| @ | Actor |
| O | Origin |
