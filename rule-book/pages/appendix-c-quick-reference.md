# Appendix C: Quick Reference

This appendix provides quick reference cards for common game procedures.

## C.1 Turn Structure

```
START OF TURN
1. Action Points reset to 3 (default)
2. Start-of-turn effects trigger
3. "Until start of turn" effects expire

ACTION PHASE
- Perform actions (any order, any number)
- Each action costs resources (usually 1 AP)
- End when out of resources or by choice

END OF TURN
1. End-of-turn effects trigger
2. "Until end of turn" effects expire
3. Pass to next actor in initiative
```

## C.2 Action Resolution

```
1. DECLARE action and target

2. VERIFY action is valid
   - Actor has the action
   - Target is in range
   - Prerequisites met

3. ROLL for the condition (if any)
   [Expression] [Operator] [Expression]
   Example: 1d20 + Attack >= Target Defense

4. APPLY effects
   - SUCCESS (if true or no condition): Apply "do" effects
   - FAILURE (if false): Apply "else" effects
   - ALWAYS: Apply "then" effects (costs go here)

5. COMPLETE
```

## C.3 Checks and Expressions

### Dice Notation
| Notation | Meaning |
|----------|---------|
| 1d20 | Roll one 20-sided die |
| 2d6 | Roll two 6-sided dice, sum results |
| d8 | Shorthand for 1d8 |

### Operators
| Operator | Meaning |
|----------|---------|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division (round down) |

### Comparisons
| Operator | Meaning |
|----------|---------|
| = | Equal to |
| != | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |

### Resource Injection
| Syntax | Meaning |
|--------|---------|
| [Health] | Your Health value |
| [Target Defense] | Target's Defense value |

## C.4 Default Mechanics

| Default | Rule |
|---------|------|
| Action Points per turn | 3 |
| Defeat condition | Health reaches 0 |
| Diagonal movement cost | 1.5 tiles (round up at end) |
| Resource minimum | 0 (cannot go negative) |

## C.5 Distance and Range

### Cardinal Movement
- Each tile costs 1 movement

### Diagonal Movement
1. Count total diagonal tiles moved
2. Multiply by 1.5
3. Round up

| Diagonals | Cost |
|-----------|------|
| 1 | 2 |
| 2 | 3 |
| 3 | 5 |
| 4 | 6 |
| 5 | 8 |

## C.6 Encounter Flow

```
DEPLOYMENT
  Place actors on map
  Set headings
  Verify positions
      |
      v
INITIATIVE
  Roll 1d100 per actor/cast
  Higher goes first
  Ties: re-roll 1d100, higher wins
      |
      v
TURNS
  Each actor takes a turn (in order)
  Round = everyone acts once
  Repeat until completion condition
      |
      v
ENCOUNTER END
  Victory, defeat, or other outcome
  Transition to next scene
```

## C.7 Common Actions

### Strike (Basic Attack)
```
Range: Melee (adjacent)
if: 1d20 + Attack >= Target Defense
do: Target Health -= 1d8 + Strength
then: Action Points -= 1
```

### Move
```
do: Move up to 3 tiles
then: Action Points -= 1
```

### Defend
```
do: +2 Defense until end of turn
then: Action Points -= 1
```

## C.8 Strategy Quick Reference (For Running Enemies)

### Aggressive
1. If adjacent: Attack lowest Health enemy
2. If not adjacent: Move toward nearest enemy
3. End turn

### Defensive
1. If Health < 50%: Heal or Defend
2. If adjacent: Attack
3. End turn

### Ranged
1. If enemy adjacent: Move away
2. If enemy in range: Ranged attack
3. If not in range: Move toward enemy
4. End turn

## C.9 Common Calculations

### Attack Roll
```
1d20 + [Attack] >= [Target Defense]
```

### Damage
```
[Weapon Die] + [Strength or Modifier]
```

### Healing
```
[Current Health] + [Healing Amount]
(Cannot exceed maximum)
```

### Movement Cost (Mixed Path)
```
Cardinal tiles + (Diagonal tiles x 1.5, rounded up)
```

## C.10 Timing Reference

### Start of Turn (in order)
1. Resource refresh
2. Start-of-turn features
3. Duration expiration

### End of Turn (in order)
1. End-of-turn features
2. Duration countdown

### Reactions
- Trigger interrupts current action
- Reaction resolves completely
- Original action continues

## C.11 Rule Precedence (Highest to Lowest)

1. This Rule Book
2. Campaign Global Features
3. Encounter Features
4. Region Features
5. Tile Features
6. Cast Features
7. Actor Features
8. Action Features
9. Temporary Effects

## C.12 Session Checklist

### Before Play
- [ ] Rule Book available
- [ ] Campaign book available
- [ ] Dice ready
- [ ] Character sheets updated
- [ ] Map prepared
- [ ] Tokens/miniatures ready
- [ ] Initiative tracker ready

### During Encounter
- [ ] Track initiative order
- [ ] Track round number
- [ ] Track actor positions
- [ ] Track Health and AP
- [ ] Track active effects and durations

### End of Session
- [ ] Record final resource values
- [ ] Note active features
- [ ] Record campaign progress
