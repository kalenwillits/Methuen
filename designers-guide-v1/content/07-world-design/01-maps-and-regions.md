# Maps and Regions

## Map Design

Maps are grids where gameplay occurs.

## Map Elements

### Grid Size
Define dimensions: 20×20, 50×50, etc.

### Origin Point
Where is 0N 0E?

### Boundaries
Which tiles are valid positions?

## Regions

Group tiles with shared properties:
```
Region: Deep Forest
Tiles: All "Forest" tiles 5+ spaces from roads
Properties: Movement cost ×2, blocks line of sight
```

## Tile Types

Define tile categories:
- Terrain type (forest, plains, water)
- Movement cost
- Special properties
- Visual appearance

---

## See Also
- Chapter 3: Maps and Grids (player perspective)
- Chapter 24: Tiles and Terrain
