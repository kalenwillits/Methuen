# Movement Systems

## Overview

Movement systems define how actors traverse the map. The framework requires campaigns to define their own movement system.

## Default Movement Systems

### 1. Resource-Based Movement

**Specification**:
```
Feature: Dexterous Movement
Move up to Dexterity spaces per turn
```

**Characteristics**:
- Variable movement per actor
- Rewards high Dexterity
- Simple to track

**Best For**: Games where individual capability variation matters

### 2. Fixed Movement

**Specification**:
```
Feature: Standard Movement
All actors move up to 6 spaces per turn
```

**Characteristics**:
- Same for all actors
- Easy to balance
- Predictable positioning

**Best For**: Games emphasizing tactics over individual stats

### 3. Action Point Movement

**Specification**:
```
Feature: AP Movement
Spend 1 ActionPoint per space moved
```

**Characteristics**:
- Movement competes with actions
- Creates tough decisions
- Highly tactical

**Best For**: Resource management focused games

## Custom Movement Design

Consider:
- How much should actors move?
- Should movement vary by actor?
- Should movement compete with actions?
- How does terrain affect movement?

---

## See Also
- Chapter 3: Maps and Grids
- Chapter 19: Initiative Systems
