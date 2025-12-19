# Turn Structure Design

## Overview

Define how actors use their turns: flexible or phased.

## Default Turn Structures

### 1. Flexible Turn Structure

**Specification**:
```
Actors may perform actions and movement in any order
Total actions limited by action economy features
Total movement limited by movement features
```

**Characteristics**:
- Maximum player freedom
- More complex to track
- Enables tactical combos

**Best For**: Experienced players, tactical depth

### 2. Phased Turn Structure

**Specification**:
```
Phase 1: Start of Turn (triggers resolve)
Phase 2: Movement (all movement occurs)
Phase 3: Action (all actions occur)
Phase 4: End of Turn (triggers resolve)
Cannot return to previous phases
```

**Characteristics**:
- Clear structure
- Easier for new players
- Prevents some tactics

**Best For**: Beginner-friendly games, simpler play

## Custom Turn Structure

You can define your own phases or hybrid systems:
```
Phase 1: Quick Action or Movement
Phase 2: Standard Action
Phase 3: Bonus Action (if available)
```

---

## See Also
- Chapter 6: Turn Structure (player perspective)
