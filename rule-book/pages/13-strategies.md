# Chapter 13: Strategies

## 13.1 Overview

Strategies provide deterministic control systems for non-player actors. By defining ranked lists of behaviors, strategies enable automated decision-making during encounters without requiring a Game Master.

## 13.2 Strategy Definition

### 13.2.1 Formal Definition

A **Strategy** is a ranked set of behaviors that:
- Controls a non-player actor's decisions
- Evaluates conditions to select actions
- Executes deterministically given the same game state
- Runs through all behaviors each turn

### 13.2.2 Strategy Properties

| Property | Description |
|----------|-------------|
| Name | Identifier for the strategy |
| Behaviors | Ordered list of conditional actions |
| Priority | Lower-numbered behaviors evaluate first |
| Scope | Actor(s) the strategy controls |

## 13.3 Behavior Structure

### 13.3.1 Behavior Components

A **Behavior** is an action with an additional condition:

| Component | Description | Required |
|-----------|-------------|----------|
| when | Condition for behavior activation | Yes (except final) |
| if | Action condition (standard action if) | No |
| do | Effects when conditions are met | Yes |
| then | Effects that always execute | No |
| else | Effects when action condition fails | No |

### 13.3.2 Behavior Format

```
Behavior: [Name]
Priority: [Number]
when: [Activation Condition]
if: [Action Condition]
do: [Effects]
then: [Guaranteed Effects]
else: [Failure Effects]
```

### 13.3.3 When vs If

The `when` and `if` conditions serve different purposes:

| Condition | Purpose | Effect if False |
|-----------|---------|-----------------|
| when | Determines if this behavior activates | Skip to next behavior |
| if | Standard action success check | Execute else, then continue |

## 13.4 Strategy Execution

### 13.4.1 Execution Flow

On a non-player actor's turn:

```
Start at Behavior Priority 1
    |
    v
+-> Evaluate 'when' condition
|   |
|   +-- [FALSE] --> Move to next priority behavior
|   |
|   +-- [TRUE] --> Execute action (if/do/then/else)
|       |
|       v
|   Check if 'do' was possible
|       |
|       +-- [YES] --> Behavior satisfied, restart from priority 1
|       |
|       +-- [NO] --> Move to next priority behavior
|
+-- If no more behaviors can execute, turn ends
```

### 13.4.2 Behavior Satisfaction

A behavior is **satisfied** when:
- Its `when` condition is true AND
- The `do` effect successfully executes

When a behavior is satisfied:
- The strategy restarts from the highest priority behavior
- This allows re-evaluation based on new game state

### 13.4.3 Turn Completion

A turn ends when:
- No behavior's `when` condition is true, OR
- No behavior's `do` effect can be executed, OR
- All available resources are exhausted

### 13.4.4 Execution Example

```
Strategy: Aggressive Warrior

Behavior 1: Attack Adjacent Enemy
Priority: 1
when: An enemy is adjacent
if: [Action Points] >= 1
do: Perform Strike action on adjacent enemy
then: (None)

Behavior 2: Move Toward Nearest Enemy
Priority: 2
when: No enemy is adjacent
if: [Action Points] >= 1
do: Move toward nearest enemy
then: (None)

Behavior 3: End Turn
Priority: 3
(No when condition - always runs when reached)
do: End turn
```

**Execution Trace**:
```
Turn Start: Actor has 3 Action Points, no adjacent enemy

1. Check Behavior 1: "An enemy is adjacent" = FALSE
   Skip to Behavior 2

2. Check Behavior 2: "No enemy is adjacent" = TRUE
   Execute: Move toward nearest enemy
   Action Points: 3 -> 2
   Behavior satisfied, restart from Behavior 1

3. Check Behavior 1: "An enemy is adjacent" = FALSE
   Skip to Behavior 2

4. Check Behavior 2: "No enemy is adjacent" = TRUE
   Execute: Move toward nearest enemy
   Action Points: 2 -> 1
   Now adjacent to enemy
   Behavior satisfied, restart from Behavior 1

5. Check Behavior 1: "An enemy is adjacent" = TRUE
   Execute: Strike action on adjacent enemy
   Action Points: 1 -> 0
   Behavior satisfied, restart from Behavior 1

6. Check Behavior 1: "An enemy is adjacent" = TRUE
   Check if: [Action Points] >= 1 = FALSE
   Cannot execute 'do', skip to Behavior 2

7. Check Behavior 2: Cannot execute (no Action Points)
   Skip to Behavior 3

8. Behavior 3: End turn
   Turn complete
```

## 13.5 Common Strategy Patterns

### 13.5.1 Aggressive Strategy

Prioritizes attacking enemies:

```
Strategy: Aggressive

1. Attack (when: adjacent enemy, do: attack)
2. Charge (when: ranged attack available, do: ranged attack)
3. Advance (when: not adjacent to enemy, do: move toward enemy)
4. End Turn
```

### 13.5.2 Defensive Strategy

Prioritizes survival and protection:

```
Strategy: Defensive

1. Heal Self (when: [Health] < [Health Max] / 2, do: heal)
2. Defend (when: adjacent enemy, do: defensive stance)
3. Retreat (when: [Health] < [Health Max] / 4, do: move away)
4. Attack (when: adjacent enemy, do: attack)
5. Hold Position (do: end turn)
```

### 13.5.3 Support Strategy

Prioritizes helping allies:

```
Strategy: Support

1. Heal Ally (when: ally [Health] < half, do: heal ally)
2. Buff Ally (when: ally in combat, do: apply buff)
3. Move to Ally (when: ally out of range, do: move toward ally)
4. Attack (when: adjacent enemy, do: attack)
5. End Turn
```

### 13.5.4 Tactical Strategy

Complex decision-making:

```
Strategy: Tactical

1. Finish Wounded (when: adjacent enemy [Health] < 5, do: attack)
2. Escape Danger (when: [Health] < 10 and adjacent enemies > 1, do: disengage)
3. Focus Fire (when: ally adjacent to enemy, do: attack that enemy)
4. Attack Weakest (when: adjacent enemy, do: attack lowest health)
5. Position (when: not in optimal position, do: move to flank)
6. Advance (do: move toward objective)
```

## 13.6 Targeting Rules

### 13.6.1 Target Selection

When a behavior could apply to multiple targets, use these priority rules:

| Priority | Rule |
|----------|------|
| 1 | Lowest Health (most likely to defeat) |
| 2 | Highest Threat (most dangerous) |
| 3 | Nearest (least movement required) |
| 4 | Random (if still tied) |

### 13.6.2 Campaign Overrides

Campaigns may specify different targeting priorities:

```
Strategy: Hunter
Target Priority: Highest [Health] first (seeks challenge)
```

### 13.6.3 Ally Targeting

When targeting allies (for support):

| Priority | Rule |
|----------|------|
| 1 | Lowest Health (most in need) |
| 2 | Highest Value (most important) |
| 3 | Nearest (easiest to reach) |

## 13.7 Movement Behaviors

### 13.7.1 Move Toward

Move to reduce distance to target:

```
when: distance to target > 1
do: Move along shortest path toward target
```

### 13.7.2 Move Away

Move to increase distance from threat:

```
when: adjacent to threat
do: Move along path that maximizes distance from threat
```

### 13.7.3 Move to Position

Move to a specific tactical position:

```
when: not at optimal position
do: Move to position that provides cover and line of sight
```

### 13.7.4 Pathfinding

For movement behaviors:
1. Calculate shortest valid path to destination
2. Move along path up to movement allowance
3. Avoid hazards if alternative paths exist
4. Stop if path is blocked

## 13.8 Conditional Expressions

### 13.8.1 Resource Conditions

```
when: [Health] < [Health Max] / 2
when: [Action Points] >= 2
when: [Mana] > 0
```

### 13.8.2 Position Conditions

```
when: adjacent to enemy
when: within 5 tiles of ally
when: in cover
when: flanking an enemy
```

### 13.8.3 State Conditions

```
when: enemy is Stunned
when: ally is Wounded
when: self is not Engaged
```

### 13.8.4 Count Conditions

```
when: number of adjacent enemies > 2
when: number of allies within 3 tiles < 1
when: number of enemies on map > 5
```

## 13.9 Strategy Assignment

### 13.9.1 Actor Assignment

Actors are assigned strategies in their definition:

```
Actor: Goblin Warrior
Strategy: Aggressive
```

### 13.9.2 Cast Assignment

All actors in a cast may share a strategy:

```
Cast: Goblin Horde
Strategy: Swarm Tactics
Members: All goblins use this strategy
```

### 13.9.3 Dynamic Assignment

Strategies may change during play:

```
Feature: Morale Break
When cast leader is defeated, all remaining cast
members switch to Strategy: Panicked
```

## 13.10 Strategy Variations

### 13.10.1 Parameterized Strategies

Strategies may include parameters:

```
Strategy: Guard Position [X]
1. Attack (when: adjacent enemy, do: attack)
2. Return (when: distance from [X] > 2, do: move toward [X])
3. Hold (do: end turn at [X])
```

### 13.10.2 Conditional Strategy Selection

Different situations may call for different strategies:

```
Feature: Adaptive Tactics
If [Health] > [Health Max] / 2: Use Strategy Aggressive
If [Health] <= [Health Max] / 2: Use Strategy Defensive
```

### 13.10.3 Hybrid Behaviors

Single actors may draw from multiple strategies:

```
Actor: Elite Guard
Behaviors from Strategy: Defensive (priorities 1-3)
Behaviors from Strategy: Aggressive (priorities 4-6)
```

## 13.11 Final Behavior Rule

### 13.11.1 Guaranteed Termination

The final behavior in a strategy does not require a `when` condition. This ensures:
- The strategy always has a valid action
- Turns cannot loop indefinitely
- Default behavior exists for unexpected situations

### 13.11.2 Common Final Behaviors

```
End Turn (do: end turn)
Wait (do: take no action, end turn)
Defend (do: enter defensive stance, end turn)
```

## 13.12 Strategy Debugging

### 13.12.1 Tracing Execution

Track strategy execution for debugging:
1. Log each behavior evaluation
2. Record when/if condition results
3. Note which actions execute
4. Track behavior restarts

### 13.12.2 Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Infinite loop | Behavior always satisfied, never blocked | Add resource costs or limits |
| Never acts | When conditions never true | Broaden conditions or reorder |
| Wrong target | Targeting rules unclear | Specify explicit targeting |
| Ignores threats | Priority order wrong | Reorder behaviors |

## 13.13 Simplified Strategy Templates

For manual play without automation tools, use these simplified templates. Run through the behaviors in order until one applies.

### 13.13.1 Simple Aggressive

Use when enemies should attack relentlessly.

```
Simple Aggressive
1. If adjacent to enemy: Attack the enemy with lowest Health
2. If not adjacent to enemy: Move toward nearest enemy
3. End turn
```

**At the table**: "Attack if you can, otherwise move closer."

### 13.13.2 Simple Defensive

Use when enemies should protect themselves.

```
Simple Defensive
1. If Health below half: Use healing action if available, else Defend
2. If adjacent to enemy: Attack
3. Stay in current position
4. End turn
```

**At the table**: "Heal or defend when hurt, otherwise attack."

### 13.13.3 Simple Ranged

Use for archers, mages, or other ranged attackers.

```
Simple Ranged
1. If enemy is adjacent: Move away to create distance
2. If enemy is in range: Use ranged attack on nearest enemy
3. If no enemy in range: Move toward an enemy
4. End turn
```

**At the table**: "Keep distance and shoot."

### 13.13.4 Simple Support

Use for healers or buff-focused actors.

```
Simple Support
1. If ally is below half Health: Heal that ally
2. If ally has no buff and can be buffed: Apply buff
3. If adjacent to enemy: Attack
4. Move toward ally with lowest Health
5. End turn
```

**At the table**: "Keep allies healthy, buff if possible."

### 13.13.5 Using Simplified Strategies

When running a strategy manually:

1. Start at behavior 1
2. Check if the condition applies
3. If yes: do the action, then start over from behavior 1
4. If no: move to the next behavior
5. Repeat until the actor's Action Points are exhausted or you reach "End turn"

Most turns require only 2-4 decisions using these templates.
