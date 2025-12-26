# Chapter 11: Encounters

## 11.1 Overview

Encounters are the tactical, turn-based phase of Methuen gameplay. During encounters, actors occupy positions on a map and take sequential turns performing actions. Encounters are the primary arena for tactical decision-making and resource management.

## 11.2 Encounter Definition

### 11.2.1 Formal Definition

An **Encounter** is a game phase characterized by:
- Actors positioned on a map grid
- Turn-based action execution
- Initiative-ordered turn sequence
- Defined completion conditions

### 11.2.2 Encounter Properties

| Property | Description |
|----------|-------------|
| Map | The grid on which the encounter takes place |
| Actors | Participants in the encounter |
| Casts | Actor groupings for control and initiative |
| Completion | Conditions that end the encounter |
| Features | Special rules for this encounter |

## 11.3 Encounter Phases

Encounters proceed through three distinct phases:

### 11.3.1 Deployment Phase

During deployment:
1. The map is established
2. Actors are placed on starting positions
3. Initial headings are set
4. Starting resources are verified

**Deployment Methods**:

| Method | Description |
|--------|-------------|
| Fixed | Actors placed at campaign-specified positions |
| Zone | Actors placed within designated deployment zones |
| Player Choice | Players choose positions within constraints |
| Random | Positions determined by dice or random selection |

### 11.3.2 Initiative Phase

During initiative:
1. Each actor or cast determines their initiative value
2. Initiative values are compared and ordered
3. Ties are resolved (see Chapter 10)
4. The turn order is established

### 11.3.3 Turns Phase

During turns:
1. Actors/casts take turns in initiative order
2. Each turn follows the turn structure (see Section 11.5)
3. Rounds repeat until completion conditions are met

## 11.4 Encounter Start

### 11.4.1 Pre-Encounter Setup

Before an encounter begins:
1. The triggering scene or event concludes
2. The encounter map is presented
3. Encounter-specific features are announced
4. Completion conditions are stated (if known)

### 11.4.2 Deployment Procedure

Standard deployment procedure:

**Step 1: Identify Deployment Zones**
- The campaign specifies deployment zones for each side
- Mark these zones clearly on the map
- Announce any special deployment rules (hidden placement, restricted tiles, etc.)

**Step 2: Player Deployment (typically first)**
- Players place their actors within their designated zone
- Each actor must occupy a valid tile
- Multiple actors may share tiles unless prohibited
- Record each actor's location

**Step 3: Set Player Headings**
- Each player actor chooses their starting heading (N, NE, E, etc.)
- Default is North if not specified
- Record headings

**Step 4: Non-Player Deployment**
- Non-player actors are placed per campaign instructions
- May be placed by Game Master or per fixed positions
- Hidden deployment (if used) keeps positions secret until revealed

**Step 5: Set Non-Player Headings**
- Set headings per campaign instructions
- Default is toward the nearest opposing actor or toward center

**Step 6: Verify All Positions**
- Confirm no actors are in impassable tiles
- Confirm all actors are within valid zones
- Resolve any placement conflicts

**Step 7: Initialize Resources**
- Verify starting resources for all actors (Health, Action Points, etc.)
- Apply any pre-encounter effects
- Record initial values

**Step 8: Confirm Readiness**
- All participants confirm deployment is complete
- Proceed to Initiative Phase

### 11.4.3 Hidden Deployment

Some encounters use hidden deployment:

```
Feature: Hidden Setup
Each side deploys actors secretly. Positions are revealed
when the Turns phase begins or when actors gain line of
sight to each other.
```

## 11.5 Turn Structure

### 11.5.1 Turn Sequence

Each actor's turn follows this sequence:

```
START PHASE
    |
    v
Resolve start-of-turn features
    |
    v
ACTION PHASE
    |
    v
Perform actions (as few or as many as desired/allowed)
    |
    v
END PHASE
    |
    v
Resolve end-of-turn features
    |
    v
TURN COMPLETE
```

### 11.5.2 Start Phase

At the start of an actor's turn, resolve effects in this order:

1. **Resource Refresh**: Action Points reset to their starting value (default: 3)
2. **Start-of-Turn Features**: Features that trigger "at the start of your turn" resolve
3. **Duration Expiration**: Effects that last "until the start of your turn" end now
4. **Conditions**: Apply any ongoing conditions (damage over time, etc.)
5. **Ready to Act**: The actor may now take actions

**Timing Clarification**: Resource refresh happens first, before start-of-turn features trigger. This means a feature that costs Action Points can use the refreshed points.

**Common Start-of-Turn Effects**:
```
Action Points reset to 3
Temporary effects from previous turn expire
Ongoing damage is applied (e.g., Burning: take 1d6 damage)
Regeneration effects restore resources
```

### 11.5.3 Action Phase

During the action phase:
1. The actor may perform any number of actions
2. Actions consume resources (typically Action Points)
3. The actor may choose to perform no actions
4. The action phase ends when the actor declares it complete or cannot perform more actions

**Action Phase Guidelines**:
- There is no inherent limit on action count
- Resource limits (Action Points) typically constrain actions
- The order of actions is the actor's choice
- Actions resolve completely before the next action begins

### 11.5.4 End Phase

At the end of an actor's turn:
1. End-of-turn features trigger in order of specificity
2. Duration-based effects tick down
3. End-of-turn conditions are resolved
4. Control passes to the next actor in initiative order

**Common End-of-Turn Effects**:
```
Burning: Take 1d6 fire damage at end of turn
Rally: Allies within 3 tiles gain 1 Morale
Concentration: Check if maintained
```

## 11.6 Rounds

### 11.6.1 Round Definition

A **Round** is a complete cycle through the initiative order, where every actor has taken one turn.

### 11.6.2 Round Tracking

Track the current round number for:
- Time-based effects
- Round-triggered events
- Duration countdowns
- Tactical planning

### 11.6.3 Start and End of Round

**Start of Round**:
- Occurs before the first actor's turn in the round
- Triggers round-start features and events
- Resets round-based resources

**End of Round**:
- Occurs after the last actor's turn in the round
- Triggers round-end features and events
- Advances round counter

```
Feature: Reinforcement Schedule
At the start of round 3, deploy 2 Goblin Warriors at the east entrance.
At the start of round 5, deploy 1 Goblin Chief at the east entrance.
```

## 11.7 Completion Conditions

### 11.7.1 Requirement

Every encounter must have defined completion conditions. Campaigns specify these conditions through Features.

### 11.7.2 Common Completion Types

**Defeat All Enemies**:
```
Feature: Elimination
The encounter ends when all actors in opposing casts are defeated.
```

**Objective Completion**:
```
Feature: Reach the Exit
The encounter ends when a player actor ends their turn on the Exit tile.
```

**Survival**:
```
Feature: Hold the Line
The encounter ends successfully when round 10 begins with at least
one player actor active.
```

**Resource Threshold**:
```
Feature: Gather Resources
The encounter ends when the party's collective Gold reaches 100.
```

### 11.7.3 Victory and Defeat

Completion conditions typically specify outcome:
- **Victory**: Players achieved the objective
- **Defeat**: Players failed the objective
- **Neutral**: Neither clear victory nor defeat

Outcomes may affect subsequent scenes or campaign progression.

### 11.7.4 Forced Ending

Some effects can end encounters immediately:

```
Feature: Retreat
If all player actors are on the Retreat zone at the end of a round,
the encounter ends in retreat. Players escape but the objective fails.
```

## 11.8 Actions During Encounters

### 11.8.1 Available Actions

Actors may perform actions that are:
- Defined in the campaign as available to all actors
- Specific to that actor's definition
- Granted by features or effects
- Available as reactions (during other turns)

### 11.8.2 Action Limits

Common limiting mechanisms:

| Limit Type | Description |
|------------|-------------|
| Action Points | Resource consumed by actions |
| Once per Turn | Action may only be used once per turn |
| Once per Round | Action may only be used once per round |
| Once per Encounter | Action may only be used once per encounter |
| Cooldown | Action unavailable for X turns after use |

### 11.8.3 Free Actions

Some actions have no cost:

```
Speak
do: The actor says something in character
Note: This is a free action with no resource cost.
```

## 11.9 Tactical Guidance

This section provides optional tactical advice for players.

### 11.9.1 Positioning

- **Use cover**: Tiles with cover features reduce incoming damage
- **Control chokepoints**: Narrow passages limit enemy movement options
- **Avoid flanking**: Position actors so enemies cannot get behind them
- **Maintain line of sight**: Stay where you can see (and target) enemies
- **Consider retreat paths**: Know how to get out if things go badly

### 11.9.2 Focus Fire

Concentrating attacks on a single enemy often outperforms spreading damage:
- Defeating one enemy removes their actions from the fight
- A wounded enemy at full action capacity is still dangerous
- Exception: area effects that can damage multiple enemies efficiently

### 11.9.3 Resource Management

- **Save some Action Points**: Having 1 AP for a reaction or emergency Defend is valuable
- **Track enemy resources**: Know when enemies are low on Health or abilities
- **Use powerful abilities early**: Shorter fights mean less total damage taken
- **Heal before critical**: Do not wait until 1 Health to heal

### 11.9.4 Action Economy

The side that gets more actions typically wins:
- Abilities that grant extra actions are very strong
- Abilities that deny enemy actions (stun, immobilize) are very strong
- A cast with more actors has a significant advantage

### 11.9.5 Pacing Your Session

For Game Masters and campaign designers:
- Most encounters should last 3-6 rounds
- Longer encounters can feel like slogs; shorter ones may feel anticlimactic
- Vary encounter length throughout a session
- Consider "escape valve" mechanics (retreat, negotiation) for long fights

## 11.10 Encounter Flow Control

### 11.10.1 Pausing Encounters

Encounters may be paused for:
- Scene interruptions (events trigger scenes)
- Rule clarifications
- Player breaks
- Nested encounters (rare)

### 11.10.2 Scene Interruptions

When an event triggers a scene:
1. The encounter pauses
2. The scene is resolved
3. The encounter resumes at the point of interruption
4. Any effects from the scene are applied

### 11.10.3 Resuming Encounters

When resuming a paused encounter:
1. Verify current turn position
2. Apply any state changes from the interruption
3. Continue with the current phase

## 11.11 Multiple Encounters

### 11.11.1 Sequential Encounters

Campaigns may chain encounters:
- State persists between encounters (resources, conditions)
- Different maps or the same map with changes
- Connected by scenes or immediate transition

### 11.11.2 Multi-Map Encounters

Some encounters span multiple connected maps:
- Actors may move between map sections
- Initiative order is shared across all sections
- Completion conditions may span multiple maps

## 11.12 Encounter Records

### 11.12.1 State Tracking

During encounters, track:
- Initiative order and current position
- Round number
- Actor positions and headings
- Resource values
- Active effects and durations
- Features and conditions

### 11.12.2 History

Optionally track:
- Actions taken
- Dice rolls
- Resource changes
- Turn-by-turn progression

## 11.13 Encounter Summary

### 11.13.1 Phase Flow

```
ENCOUNTER START
    |
    v
DEPLOYMENT PHASE
  - Place actors
  - Set headings
  - Verify positions
    |
    v
INITIATIVE PHASE
  - Roll initiative
  - Establish order
  - Resolve ties
    |
    v
TURNS PHASE
  +-> Round Start
  |   |
  |   v
  |   Actor Turn (in initiative order)
  |     - Start Phase
  |     - Action Phase
  |     - End Phase
  |   |
  |   v
  |   [Next actor until all have acted]
  |   |
  |   v
  |   Round End
  |   |
  |   +-- Check completion conditions
  |   |     |
  |   |     +-- [Not met] -> Continue to next round
  |   |     |
  +---+     +-- [Met] -> Exit Turns Phase
              |
              v
ENCOUNTER END
  - Determine outcome
  - Apply consequences
  - Transition to next scene or encounter
```
