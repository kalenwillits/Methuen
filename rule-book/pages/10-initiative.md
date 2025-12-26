# Chapter 10: Initiative

## 10.1 Overview

Initiative determines the order in which actors and casts take their turns during encounters. The initiative system ensures consistent, fair turn ordering while allowing campaigns to customize the determination method.

## 10.2 Initiative Definition

### 10.2.1 Formal Definition

**Initiative** is a numerical value assigned to each actor or cast that determines their position in the turn order. Higher initiative values act before lower initiative values.

### 10.2.2 Initiative Properties

| Property | Description |
|----------|-------------|
| Value | Numerical score determining turn position |
| Order | Descending (highest acts first) |
| Scope | Determined per encounter |
| Persistence | Typically fixed for encounter duration |

## 10.3 Default Initiative

### 10.3.1 Default Initiative Feature

When a campaign does not define an initiative feature, the following default applies:

```
Default Initiative
When an actor or cast is first deployed to a map, roll 1d100.
Turn order is in descending order.
Ties are resolved by the two tied actors or casts rolling 1d100,
placing the higher-rolling actor or cast before the lower-rolling
actor or cast in the turn order.
```

### 10.3.2 Default Procedure

1. Each actor or cast rolls 1d100
2. Record all initiative values
3. Order actors/casts from highest to lowest
4. Resolve any ties (see Section 10.5)
5. Turn order is established for the encounter

## 10.4 Campaign Initiative Features

### 10.4.1 Custom Initiative

Campaigns may define alternative initiative systems using Global Features.

**Example: Dexterity-Based Initiative**
```
Initiative Feature
When an actor or cast is deployed, roll 1d20 + [Dexterity].
Turn order is in descending order.
```

**Example: Fixed Initiative**
```
Initiative Feature
Actors act in order of their [Speed] resource, highest first.
No dice are rolled.
```

**Example: Card-Based Initiative**
```
Initiative Feature
Draw a card for each actor or cast from a shuffled deck.
Order from highest card (Ace high) to lowest.
```

### 10.4.2 Cast Initiative Methods

For casts, initiative may be determined by:
- A single roll for the entire cast
- The highest roll among cast members
- The leader's roll
- A fixed value based on cast properties

**Example: Leader Rolls**
```
Cast Initiative
The cast leader rolls 1d20 + [Tactics].
All cast members share this initiative value.
```

**Example: Best of Cast**
```
Cast Initiative
Each cast member rolls 1d20 + [Dexterity].
The cast uses the highest result among its members.
```

## 10.5 Tie Resolution

### 10.5.1 Standard Tie Resolution

When two or more actors or casts have the same initiative value:

1. The tied participants each roll 1d100
2. The higher roll acts before the lower roll
3. If still tied, repeat the roll
4. Continue until all ties are resolved

### 10.5.2 Alternative Tie Resolution Methods

Campaigns may specify alternative tie-breaking methods:

**Resource Comparison**
```
Tie Resolution
If initiative values are tied, the actor with higher [Dexterity]
acts first. If still tied, roll 1d100.
```

**Player Priority**
```
Tie Resolution
If initiative values are tied, player-controlled actors
act before non-player actors. Among same-controlled actors,
roll 1d100.
```

**Clockwise Order**
```
Tie Resolution
If initiative values are tied, resolve in clockwise order
starting from the current game master's position.
```

### 10.5.3 Tie Resolution for Casts

When casts tie in initiative:
- The casts complete the tie-breaking procedure
- The winning cast takes their entire cast turn first
- Within each cast, normal sub-initiative or player choice applies

## 10.6 Initiative Order

### 10.6.1 Establishing Order

The initiative order is established during the Initiative phase of an encounter:

1. All actors/casts roll for initiative (or calculate fixed values)
2. Values are recorded and sorted in descending order
3. Ties are resolved
4. The final order is the turn sequence for the encounter

### 10.6.2 Order Representation

Initiative order is typically tracked as a list:

```
Initiative Order:
1. Elara (Fighter) - 18
2. Goblin Pack (Cast) - 15
3. Theron (Wizard) - 12
4. Orc Champion - 10
5. Mira (Rogue) - 8
```

### 10.6.3 Round Structure

A **round** is complete when all actors and casts in the initiative order have taken their turns:

```
Round 1:
  Elara acts
  Goblin Pack acts (all members)
  Theron acts
  Orc Champion acts
  Mira acts

Round 2:
  Elara acts
  ...
```

## 10.7 Initiative Modifications

### 10.7.1 Delayed Actions

Some systems allow actors to delay their turn:

```
Delay Action
An actor may choose to delay their turn, acting later
in the initiative order. The actor's initiative becomes
one less than the current actor when they choose to act.
```

### 10.7.2 Ready Actions

Some systems allow actors to ready actions:

```
Ready Action
An actor may ready an action with a specified trigger.
The actor's turn ends. When the trigger occurs,
the readied action executes immediately.
```

### 10.7.3 Initiative Changes

Effects may modify initiative during an encounter:

```
Haste
do: Target's initiative increases by 10 until end of encounter
    Re-sort initiative order
```

```
Slow
do: Target's initiative decreases by 10 until end of encounter
    Re-sort initiative order
```

## 10.8 Special Initiative Cases

### 10.8.1 Surprise

Campaigns may include surprise mechanics that affect initiative:

```
Feature: Surprise Round
If one side is unaware of the other at encounter start,
the aware side takes a full round of actions before
normal initiative begins.
```

### 10.8.2 Joining Combat

When actors join an encounter after it has begun:

```
Feature: Late Arrival
Actors deployed after initiative is determined roll initiative
immediately and are inserted into the turn order at their
rolled position. They act normally when their turn comes.
```

### 10.8.3 Leaving Combat

When actors leave an encounter:
- They are removed from the initiative order
- Other positions are not affected
- If they return, they re-roll initiative

## 10.9 Sub-Initiative

### 10.9.1 Purpose

**Sub-Initiative** determines turn order for actors within a strategy-controlled cast. While the cast has a single initiative value, each member has a sub-initiative for internal ordering.

### 10.9.2 Sub-Initiative Procedure

1. Each actor in the cast rolls for sub-initiative
2. Order actors from highest to lowest
3. Resolve ties using standard tie resolution
4. Actors act in sub-initiative order during the cast's turn

### 10.9.3 Sub-Initiative Example

```
Goblin Pack Initiative: 15

Sub-Initiative Rolls:
  Goblin Chief: 14
  Goblin Warrior A: 8
  Goblin Warrior B: 11
  Goblin Archer: 6

Turn Order Within Cast:
  1. Goblin Chief (14)
  2. Goblin Warrior B (11)
  3. Goblin Warrior A (8)
  4. Goblin Archer (6)
```

### 10.9.4 Player Casts

Player-controlled casts do not use sub-initiative. The controlling player determines the order of actor turns within the cast.

## 10.10 Initiative Procedure Summary

### 10.10.1 Start of Encounter

1. **Deployment Phase** completes
2. **Initiative Phase** begins
3. Each actor/cast determines initiative value
4. Values are sorted in descending order
5. Ties are resolved
6. Initiative order is finalized
7. **Turns Phase** begins

### 10.10.2 During Encounter

```
For each round:
    For each position in initiative order:
        If position is an actor:
            Actor takes their turn
        If position is a cast:
            Determine internal turn order
            Each cast member takes their turn
    End of round
```

### 10.10.3 Initiative Tracking

Maintain the initiative order throughout the encounter:
- Mark completed turns
- Track round number
- Note any modifications to initiative values
- Update order when actors join or leave

## 10.11 Physical Tracking Methods

For tabletop play, consider these methods for tracking initiative:

### 10.11.1 Initiative Cards

Create a card for each actor or cast with their name and initiative value. Arrange cards in order, moving completed actors to a "done" pile each round.

### 10.11.2 Tokens on Track

Use a numbered track (1-20 or similar) and place tokens at each actor's initiative value. Move a marker along the track to indicate the current turn.

### 10.11.3 Tent Cards

Fold index cards into tent shapes and place them on the table edge in initiative order. The leftmost card is the current actor; move completed actors to the right.

### 10.11.4 Digital Tools

Many virtual tabletop systems and companion apps provide automatic initiative tracking with drag-and-drop reordering.

### 10.11.5 Best Practices

Regardless of method:
- Announce whose turn it is and who is next ("Sera, you're up. Marcus, you're on deck.")
- Keep the tracker visible to all players
- Update immediately when initiative changes
- Clearly mark round boundaries
