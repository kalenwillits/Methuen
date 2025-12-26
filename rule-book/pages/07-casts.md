# Chapter 7: Casts

## 7.1 Overview

A Cast is a grouping mechanism that organizes multiple actors under unified control. Casts simplify initiative management and enable coordinated play among related actors.

## 7.2 Cast Definition

### 7.2.1 Formal Definition

A **Cast** is a group of actors that:
- Share a single controller (player or strategy)
- Share a single initiative value
- Take their turns consecutively during an encounter

### 7.2.2 Cast Properties

| Property | Description |
|----------|-------------|
| Name | Identifier for the cast |
| Controller | Player or strategy controlling the cast |
| Initiative | Shared initiative value for turn order |
| Members | List of actors belonging to the cast |

## 7.3 Cast Membership

### 7.3.1 Assignment

Actors are assigned to casts in one of the following ways:
- Campaign definition (pre-assigned)
- Deployment phase (assigned at encounter start)
- Dynamic assignment (effects that add actors to casts)

### 7.3.2 Single Membership

An actor belongs to exactly one cast at any time. If an effect would assign an actor to a new cast, the actor leaves their current cast first.

### 7.3.3 Solo Actors

Actors not assigned to a multi-member cast are treated as single-member casts. They follow all cast rules but operate independently.

## 7.4 Cast Control

### 7.4.1 Player-Controlled Casts

For casts controlled by players:
- The controlling player makes all decisions for all actors in the cast
- The player determines the order in which cast members act during the cast's turn
- The player may freely interleave actions between cast members

### 7.4.2 Strategy-Controlled Casts

For casts controlled by strategies:
- A sub-initiative determines the order of actor turns within the cast
- Each actor follows their assigned strategy independently
- See Chapter 13 for complete strategy rules

**Note**: Before reading about sub-initiative below, you may want to review Chapter 10 (Initiative) for full details on how turn order is determined.

### 7.4.3 Control Transfer

Control of a cast may transfer during play through:
- Feature effects
- Scene choices
- Campaign events

When control transfers, the new controller immediately assumes all decision-making authority.

## 7.5 Cast Initiative

### 7.5.1 Shared Initiative

All actors in a cast share a single initiative value. This value determines when the cast acts relative to other casts and solo actors in the turn order.

### 7.5.2 Initiative Determination

Cast initiative is determined using the campaign's initiative feature (see Chapter 10). Common methods include:
- Single roll for the entire cast
- Roll by the cast's leader or designated actor
- Fixed value based on cast properties

### 7.5.3 Sub-Initiative

Within a strategy-controlled cast, sub-initiative determines the order of individual actor turns:

1. Each actor in the cast rolls for sub-initiative
2. Actors act in sub-initiative order (highest first)
3. Sub-initiative ties are resolved using the same method as initiative ties

**Example**:
```
Goblin Pack (Cast)
Cast Initiative: 15

Members:
  Goblin Warrior A: Sub-initiative 7
  Goblin Warrior B: Sub-initiative 12
  Goblin Archer: Sub-initiative 3

Turn order within cast: B, A, Archer
```

### 7.5.4 Player Cast Turn Order

For player-controlled casts, the player chooses the order of actor turns. No sub-initiative is required.

## 7.6 Cast Turns

### 7.6.1 Turn Sequence

When a cast's turn begins in the initiative order:

1. **Cast Start**: Resolve any start-of-turn features for the cast
2. **Actor Turns**: Each actor in the cast takes their turn
3. **Cast End**: Resolve any end-of-turn features for the cast

### 7.6.2 Actor Turn Interleaving

For player-controlled casts, actors' actions may be interleaved. This is one of the primary advantages of grouping actors into casts.

**Worked Example: Player Cast Turn**

> **Situation**: The Heroes cast contains Sera (Knight) and Marcus (Wizard). It is the Heroes' turn in the initiative order. Both actors have 3 Action Points.
>
> **The Turn Unfolds**:
>
> 1. **Marcus moves** (3 tiles toward cover, 1 AP spent)
>    - Marcus: 2 AP remaining
>    - Sera: 3 AP remaining
>
> 2. **Sera moves** (3 tiles toward the Orc, 1 AP spent)
>    - Marcus: 2 AP remaining
>    - Sera: 2 AP remaining
>
> 3. **Sera attacks the Orc** with Strike (hits, Orc takes 8 damage, 1 AP spent)
>    - Marcus: 2 AP remaining
>    - Sera: 1 AP remaining
>
> 4. **Marcus casts Magic Missile** at the wounded Orc (auto-hit, Orc takes 6 damage, defeated! 2 AP spent)
>    - Marcus: 0 AP remaining
>    - Sera: 1 AP remaining
>
> 5. **Sera uses Defend** (+2 Defense until end of turn, 1 AP spent)
>    - Marcus: 0 AP remaining
>    - Sera: 0 AP remaining
>
> **End of Cast Turn**: Both actors have spent their Action Points. The Heroes' turn ends and play passes to the next position in the initiative order.

This interleaving allows tactical coordination: Marcus waited to see if Sera's attack would wound the Orc before committing his spell. Sera defended after the threat was eliminated rather than before. The players can adapt their plan as the turn unfolds.

### 7.6.3 Strategy Cast Turns

For strategy-controlled casts, actors complete their full turns in sub-initiative order. Interleaving is not permitted:

**Example**:
```
Enemy Cast with Warrior (sub-init 10) and Mage (sub-init 8)

Turn sequence:
  1. Warrior completes full turn (all actions)
  2. Mage completes full turn (all actions)
```

## 7.7 Cast Relationships

### 7.7.1 Allied Casts

Casts may be designated as allied. Allied cast members:
- Cannot target each other with hostile actions (unless permitted)
- May target each other with beneficial actions
- Share victory/defeat conditions (typically)

### 7.7.2 Opposing Casts

Casts not allied are considered opposing. Opposing cast members:
- May target each other with hostile actions
- Typically cannot target each other with beneficial actions
- Have conflicting objectives

### 7.7.3 Affiliation Rules

Affiliation affects action targeting:

| Acting Cast | Target Cast | Hostile Actions | Beneficial Actions |
|-------------|-------------|-----------------|-------------------|
| Same | Same | Typically No | Yes |
| Allied | Allied | Typically No | Yes |
| Opposed | Opposed | Yes | Typically No |

Campaigns may modify these defaults with Features.

## 7.8 Cast Composition

### 7.8.1 Minimum Size

A cast must contain at least one actor. Empty casts are removed from play.

### 7.8.2 Maximum Size

There is no inherent maximum cast size. Campaigns may impose limits through Features.

### 7.8.3 Cast Leaders

Campaigns may designate a cast leader who:
- Rolls initiative for the cast
- Makes decisions on behalf of the cast
- Has special abilities affecting the cast
- Determines cast defeat if removed

### 7.8.4 Dynamic Membership

Cast membership may change during an encounter:

**Adding Members**:
```
Summoning effects may add actors to the summoner's cast
Reinforcement events may add actors to existing casts
```

**Removing Members**:
```
Defeated actors are removed from their cast
Effects may transfer actors between casts
```

## 7.9 Cast Defeat

### 7.9.1 Individual Defeat

When an actor in a cast is defeated:
- The actor is removed from the cast
- Remaining cast members continue normally
- The cast persists with remaining members

### 7.9.2 Cast Elimination

When all actors in a cast are defeated:
- The cast is removed from the initiative order
- Cast-level features cease to function
- Any effects targeting the cast expire

### 7.9.3 Leader Defeat

If a campaign defines leader-dependent casts:
- Defeating the leader may defeat all members
- Defeating the leader may dissolve the cast
- Specific behavior is defined by Features

## 7.10 Cast Features

### 7.10.1 Cast-Level Features

Features may apply to casts rather than individual actors:

```
Feature: Pack Tactics
Cast Feature
All actors in this cast gain +2 Attack when adjacent
to another member of this cast.
```

### 7.10.2 Leadership Features

Leaders may grant features to their cast:

```
Feature: Inspiring Presence
While the cast leader is active, all other cast members
gain +1 to all resource checks.
```

### 7.10.3 Formation Features

Casts may gain features based on member positions:

```
Feature: Shield Wall
When three or more cast members are adjacent in a line,
all gain +2 Defense against attacks from their front arc.
```

## 7.11 Cast Examples

### 7.11.1 Player Party Cast

```
Cast: Heroes
Controller: Player 1
Members:
  - Elara (Fighter)
  - Theron (Wizard)
  - Mira (Rogue)
Initiative: 1d20 + highest [Dexterity] among members
```

### 7.11.2 Enemy Squad Cast

```
Cast: Goblin Raiders
Controller: Strategy (Aggressive)
Members:
  - Goblin Chief (Leader)
  - Goblin Warrior x3
  - Goblin Archer x2
Initiative: 1d20 (rolled by Chief)
Sub-Initiative: 1d20 per member
```

### 7.11.3 Solo Actor as Cast

```
Cast: Dragon
Controller: Strategy (Territorial)
Members:
  - Ancient Red Dragon
Initiative: 1d20 + 15
```
