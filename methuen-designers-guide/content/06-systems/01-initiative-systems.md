# Initiative Systems

## Overview

Initiative determines turn order. Campaigns must define how initiative is determined and when it's rolled.

## Default Initiative Systems

### 1. Simple Roll

**Specification**:
```
Initiative: Roll 1d20
Highest goes first, re-roll ties
Roll at start of encounter
```

**Characteristics**:
- Random turn order
- Quick to resolve
- No stat advantage

**Best For**: Simple, fast-paced games

### 2. Resource-Modified Roll

**Specification**:
```
Initiative: Roll 1d10 × Dexterity
Highest goes first, re-roll ties  
Roll at start of encounter
```

**Characteristics**:
- Rewards high stats
- More consistent than pure random
- Still has variance

**Best For**: Games where stats matter

### 3. Static Initiative

**Specification**:
```
Initiative: Equal to Speed resource
Highest goes first, ties broken by d20 roll
Fixed for entire encounter
```

**Characteristics**:
- Completely predictable
- No randomness
- Stat-based advantage

**Best For**: Strategic, planning-focused games

## Custom Initiative Design

Consider:
- How random should turn order be?
- Should stats influence initiative?
- When is initiative determined?
- Does initiative ever change mid-encounter?

---

## See Also
- Chapter 6: Turn Structure
- Chapter 18: Movement Systems
