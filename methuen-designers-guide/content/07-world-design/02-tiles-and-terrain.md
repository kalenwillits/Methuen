# Tiles and Terrain

## Tile Properties

Each tile type can have:

### Movement Cost
```
Plains: 1 movement per space
Forest: 2 movement per space
Mountain: Impassable
```

### Triggers
```
Lava: Actors entering take 1d6 damage
Healing Spring: Actors starting turn here gain 2 health
```

### Vision
```
Wall: Blocks line of sight
Forest: Partial cover
Open: No obstruction
```

## Dynamic Tiles

Tiles can change:
```
Action: Light Fire
then: Target tile becomes "Burning" for 5 turns
```

---

## See Also
- Chapter 23: Maps and Regions
- Chapter 3: Maps and Grids
