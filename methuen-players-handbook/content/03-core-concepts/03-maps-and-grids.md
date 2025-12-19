# Maps and Grids

## Maps

**Definition**: A **map** is a grid of tiles that contains actors' spatial information and defines boundaries for gameplay.

### Map Components

Every map may include:

1. **Grid**: A coordinate system for actor positions
2. **Origin**: The reference point (0,0) for coordinates
3. **Boundaries**: Limits defining where actors can exist
4. **Tiles**: Individual grid spaces with potential properties
5. **Regions**: Collections of similar or related tiles

## The Grid System

Methuen uses a cardinal direction grid system for actor positioning.

### Coordinate Notation

Locations are expressed as distances from the map's origin:

**Format**: `X Direction, Y Direction`

**Examples**:
- `5N 3W`: Five spaces north, three spaces west from origin
- `10S 7E`: Ten spaces south, seven spaces east from origin
- `0N 0E`: The origin point itself

### The Eight Directions

```
NW    N    NE
  \   |   /
   \  |  /
W ---+--- E
   /  |  \
  /   |   \
SW    S    SE
```

**Cardinal Directions** (4): N, E, S, W
**Diagonal Directions** (4): NE, SE, SW, NW

## Actor Location

Every actor has a **location** property indicating their position on the current map.

### Location Changes

Actors change location through:
- **Movement**: Using movement actions or features
- **Forced Repositioning**: Effects that move actors (push, pull, teleport)
- **Transitions**: Moving between maps in a world

### Occupancy

Multiple actors can occupy the same tile unless a campaign feature restricts this.

## Heading

**Definition**: An actor's **heading** is the direction they are facing.

### Heading Values

Actors face one of the eight directions: N, NE, E, SE, S, SW, W, NW

### Why Heading Matters

Heading determines:
- **Radial positioning**: Where other actors/objects are relative to the actor
- **Facing-dependent actions**: Some actions may only work in certain directions
- **Vision and awareness**: Campaigns may limit perception based on heading

### Radial Directions

**Definition**: **Radial** refers to the cardinal direction relative to an actor's heading.

If an actor faces North, their radials are:
- **Front**: N
- **Front-right**: NE
- **Right**: E
- **Back-right**: SE
- **Back**: S
- **Back-left**: SW
- **Left**: W
- **Front-left**: NW

**Example**: "Spawn an actor 1d6 spaces away on the NE radial" means:
1. Determine the actor's heading (e.g., facing North)
2. The NE radial from North heading is Northeast
3. Roll 1d6 (e.g., roll 4)
4. Place the new actor 4 spaces Northeast

## Movement Costs

### Standard Movement

Moving one space in a cardinal direction (N, E, S, W) typically costs 1 movement resource.

### Diagonal Movement

Moving diagonally (NE, SE, SW, NW) costs **1.5× the resources of cardinal movement**, rounded up.

**Examples**:
- If cardinal movement costs 1, diagonal costs 2 (1.5 rounded up)
- If cardinal movement costs 2, diagonal costs 3 (3.0, no rounding needed)

**Note**: The specific cost of movement is defined by campaign features.

## Tiles and Regions

### Tiles

**Definition**: A **tile** is a single grid coordinate on a map.

Tiles may have:
- **Type**: Terrain classification (forest, road, water, etc.)
- **Properties**: Movement modifiers, triggers, visual blocking
- **Events**: Actions or effects triggered by entering/exiting

### Regions

**Definition**: A **region** is a collection of similar or related tiles on a map.

Regions allow:
- Grouping tiles with shared properties
- Defining areas for campaign scenarios
- Creating zone-based effects

**Example**: A "Deep Forest" region might include all forest tiles 5+ spaces from any road.

## Worlds

**Definition**: A **world** is a collection of maps.

Worlds enable:
- Large-scale campaigns across multiple locations
- Map transitions and travel
- Persistent actor states between maps

