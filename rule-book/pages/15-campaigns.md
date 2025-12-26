# Chapter 15: Campaigns

## 15.1 Overview

A Campaign is the complete content package that uses the Methuen framework to deliver a playable game experience. Campaigns define all actors, maps, encounters, scenes, resources, and features that make up a specific game.

## 15.2 Campaign Definition

### 15.2.1 Formal Definition

A **Campaign** is a book or document that:
- Defines content for play using Methuen rules
- Guides players through encounters and scenes
- Establishes world-specific mechanics via features
- Specifies completion conditions

### 15.2.2 Campaign Properties

| Property | Description |
|----------|-------------|
| Title | Name of the campaign |
| Overview | Summary of campaign premise and goals |
| Resources | Resource definitions for the campaign |
| Features | Global and optional features |
| Actors | Actor definitions |
| Maps | Map layouts and specifications |
| Encounters | Encounter definitions |
| Scenes | Scene content |
| Progression | How content connects |
| Completion | How the campaign ends |

## 15.3 Campaign Structure

### 15.3.1 Component Hierarchy

```
Campaign
|
+-- Global Features
|   +-- Core mechanics
|   +-- Optional rules
|
+-- Resources
|   +-- Definitions
|   +-- Initialization rules
|   +-- Maximums
|
+-- Content
|   +-- Scenes
|   |   +-- Narratives
|   |   +-- Choices
|   |   +-- Checks
|   |
|   +-- Encounters
|       +-- Maps
|       +-- Actors
|       +-- Completion conditions
|
+-- Progression
|   +-- Starting point
|   +-- Transitions
|   +-- Branches
|
+-- Completion
    +-- Victory conditions
    +-- Defeat conditions
    +-- Endings
```

### 15.3.2 Minimal Campaign

At minimum, a campaign requires:
1. At least one scene or encounter
2. Completion conditions
3. Enough actors to populate content

All other elements use framework defaults.

## 15.4 Campaign Content

### 15.4.1 Starting Content

Every campaign begins with:
- An initial scene or encounter
- Starting actor definitions
- Initial resource states

```
Campaign: The Dark Citadel

Starting Scene: "The Village Burns"

Starting Cast: Heroes
  - Aldric the Knight
  - Elena the Mage
  - Finn the Rogue

Starting Resources:
  Party Gold: 100
  Reputation: 0
```

### 15.4.2 Content Flow

Campaigns define how content connects:

```
Scene: The Village Burns
  Transition: Encounter "First Battle"

Encounter: First Battle
  On Victory: Scene "Aftermath"
  On Defeat: Scene "Captured"

Scene: Aftermath
  Choice A: Scene "Pursue"
  Choice B: Scene "Defend"
```

### 15.4.3 Branching Content

Campaigns may include multiple paths:

```
The campaign branches based on player choices:

Path A: The Direct Assault
  Encounters: Gatehouse, Inner Keep, Throne Room

Path B: The Infiltration
  Encounters: Sewers, Dungeon, Throne Room

Path C: The Siege
  Encounters: Camp, Walls (x3), Courtyard, Throne Room
```

## 15.5 Resource Configuration

### 15.5.1 Resource Definitions

Campaigns define available resources:

```
Resources:
  Health: Actor vitality
  Mana: Magical energy
  Action Points: Actions per turn
  Gold: Currency
  Experience: Character growth
  Reputation: Standing with factions
```

### 15.5.2 Initialization Rules

Campaigns specify how resources initialize:

```
Initialization:
  Health: 10 + [Constitution]
  Mana: [Intelligence] * 2
  Action Points: 3 (fixed)
  Gold: 50 (fixed)
  Experience: 0 (fixed)
```

### 15.5.3 Maximum Rules

Campaigns define resource constraints:

```
Maximums:
  Health: Initial value (cannot exceed starting Health)
  Mana: [Intelligence] * 3
  Action Points: 5
  Gold: None (unlimited)
```

## 15.6 Actor Definitions

### 15.6.1 Player Actors

Campaigns define player-controlled actors:

```
Actor: Aldric the Knight
Type: Player
Cast: Heroes

Resources:
  Health: 25
  Strength: 8
  Constitution: 7
  Action Points: 3

Actions:
  - Strike
  - Defend
  - Rally

Features:
  - Heavy Armor
  - Shield Bearer
```

### 15.6.2 Non-Player Actors

Campaigns define enemies and allies:

```
Actor: Goblin Warrior
Type: Non-Player
Strategy: Aggressive

Resources:
  Health: 8
  Strength: 3
  Defense: 2

Actions:
  - Strike
  - Move

Features:
  - Pack Tactics
```

### 15.6.3 Actor Templates

Campaigns may define templates for common actor types:

```
Template: Standard Soldier
Resources:
  Health: 15
  Strength: 5
  Defense: 4
Actions: Strike, Defend, Move
Features: Trained Combatant

Actor: Castle Guard (uses Template: Standard Soldier)
  Additional Features: Loyal to the Crown

Actor: Rebel Fighter (uses Template: Standard Soldier)
  Additional Features: Guerrilla Tactics
```

## 15.7 Map Definitions

### 15.7.1 Map Specification

Campaigns define encounter maps:

```
Map: Castle Courtyard
Dimensions: 20 x 15
Origin: 10N 7E (center)

Regions:
  - Gatehouse (0-2N, 6-8E): Cover
  - Fountain (9-11N, 6-8E): Difficult Terrain
  - Walls (perimeter): Impassable

Deployment Zones:
  - Players: 0-3N, 5-9E
  - Enemies: 15-18N, 5-9E

Events:
  - Reinforcements at round 3 (spawn at 18N 7E)
```

### 15.7.2 Map Visualization

```
####################
#..................#
#..E.E.E.E.........#
#..................#
#......~~~.........#
#......~~~.........#
#......~~~.........#
#..................#
#..P.P.P...........#
##===##############

Legend:
# = Wall
. = Open
~ = Fountain (difficult)
= = Gate
P = Player deployment
E = Enemy deployment
```

## 15.8 Encounter Definitions

### 15.8.1 Encounter Specification

```
Encounter: Castle Assault
Map: Castle Courtyard

Actors:
  Player Cast: Heroes (deployed by player)
  Enemy Cast: Castle Guards
    - Guard Captain x1
    - Castle Guard x4

Initiative: Standard (1d20)

Completion:
  Victory: All enemies defeated
  Defeat: All heroes defeated
  Retreat: All heroes exit via gate

Transitions:
  Victory: Scene "Castle Falls"
  Defeat: Scene "Captured"
  Retreat: Scene "Regroup"
```

### 15.8.2 Encounter Features

```
Encounter Features:
  - Alarm System: If combat lasts 5 rounds, reinforcements arrive
  - Civilian Presence: -10 Reputation for each civilian harmed
  - Dark Corners: Tiles in shadow provide cover
```

## 15.9 Scene Definitions

### 15.9.1 Scene Specification

```
Scene: The Decision
Type: Choice + Check

Narrative:
The rebel leader presents three options for infiltrating
the castle. Each carries different risks and rewards.

Options:
A) Storm the gate (leads to Encounter "Castle Assault")
   Check: [Strength] >= 6 for bonus positioning

B) Scale the walls (leads to Encounter "Wall Climb")
   Check: [Dexterity] >= 7 or take 2d6 damage

C) Use the sewers (leads to Encounter "Sewer Crawl")
   Check: [Constitution] >= 5 or gain "Sickened" condition

Effects:
  All options: Gain 50 Experience for reaching this point
```

## 15.10 Progression System

### 15.10.1 Linear Progression

Simple campaigns use linear progression:

```
Scene 1 -> Encounter 1 -> Scene 2 -> Encounter 2 -> ... -> Ending
```

### 15.10.2 Branching Progression

Complex campaigns use branching:

```
         Scene 1
            |
       Encounter 1
       /    |    \
   Scene   Scene   Scene
   2A      2B      2C
    |       |       |
   Enc     Enc     Enc
   2A      2B      2C
    \       |      /
         Scene 3
            |
       Final Encounter
            |
         Ending
```

### 15.10.3 Hub-Based Progression

Some campaigns use hub structures:

```
        Town Hub
       /   |   \
   Quest Quest Quest
     A     B     C
       \   |   /
        Town Hub
           |
    (After all quests)
           |
     Final Quest
```

## 15.11 Completion Conditions

### 15.11.1 Standard Completion

Campaigns complete when all encounters are finished:

```
Completion: Campaign Complete
When all encounters have been completed (victory or defeat),
the campaign ends with the appropriate ending.
```

### 15.11.2 Feature-Defined Completion

Campaigns may define special completion conditions:

```
Feature: Race Against Time (Global)
The campaign must be completed within 50 total rounds
across all encounters. If round 50 ends before the
final encounter is complete, the campaign ends in defeat.
```

### 15.11.3 Victory Conditions

```
Victory Conditions:
- Defeat the Dark Lord in the final encounter
- OR convince the Dark Lord to surrender (Diplomacy check)
- OR destroy the Dark Crystal (objective in encounter)
```

### 15.11.4 Defeat Conditions

```
Defeat Conditions:
- All heroes are defeated in any encounter
- The Town is destroyed (Reputation falls below -100)
- Time limit exceeded (50 rounds)
```

## 15.12 Campaign Endings

### 15.12.1 Multiple Endings

Campaigns may have multiple endings based on player actions:

```
Ending A: Complete Victory
Condition: Dark Lord defeated, all quests completed
Narrative: Peace returns to the land...

Ending B: Pyrrhic Victory
Condition: Dark Lord defeated, some quests failed
Narrative: The threat is ended, but at great cost...

Ending C: Diplomatic Resolution
Condition: Dark Lord surrendered
Narrative: An uneasy peace begins...

Ending D: Defeat
Condition: Any defeat condition met
Narrative: Darkness covers the land...
```

### 15.12.2 Ending Effects

Endings may have mechanical effects for campaign sequels:

```
Ending A carries forward:
  +100 starting Gold in sequel
  Feature "Heroes of the Realm" (permanent)

Ending B carries forward:
  Normal starting resources
  Some NPCs unavailable in sequel
```

## 15.13 Campaign Design Guidelines

### 15.13.1 Clarity

Campaign content should:
- Clearly present all options and their consequences
- Specify completion conditions explicitly
- Define all custom features unambiguously
- Indicate difficulty and length

### 15.13.2 Balance

Campaigns should:
- Provide appropriate challenge for intended audience
- Offer meaningful choices with distinct outcomes
- Balance resource availability with costs
- Test all paths for playability

### 15.13.3 Completeness

Campaigns must include:
- All referenced actors, maps, and encounters
- All custom features used
- All transition destinations
- Resolution for all branches

### 15.13.4 Rule Precedence

Remember: This Rule Book supersedes campaign content where conflicts exist. Campaigns extend but cannot contradict the core Methuen framework.

## 15.14 Campaign Creation Guide

This section provides guidance for players who want to design their own campaigns.

### 15.14.1 Getting Started

To create a minimal playable campaign:

1. **Define at least one encounter**
   - Create a simple map (10x10 tiles is a good start)
   - Design 2-3 enemy actors
   - Set a completion condition (defeat all enemies)

2. **Define player actors or allow creation**
   - Provide pre-made characters, or
   - Provide character creation rules (resources, actions, features)

3. **Define core actions**
   - Strike (basic attack)
   - Move (movement action)
   - Defend (defensive option)
   - Any special actions for your setting

4. **Use default mechanics**
   - 3 Action Points per turn (see Chapter 4, Section 4.10)
   - Defeat at 0 Health
   - Standard diagonal movement (Chapter 8)

### 15.14.2 Expanding Your Campaign

After you have a working encounter, add:

**Scenes** to connect encounters:
- Introduction scene (sets up the story)
- Victory/defeat scenes
- Choice points between encounters

**More actors** for variety:
- Different enemy types with different strategies
- Allies or neutral characters

**Features** to add depth:
- Environmental effects (darkness, difficult terrain)
- Special abilities for actors
- Optional rules (critical hits, flanking)

### 15.14.3 Testing Your Campaign

Before finalizing:

1. **Play through each encounter**
   - Is it winnable?
   - Is it too easy?
   - Does it take a reasonable number of rounds?

2. **Check resource balance**
   - Do players run out of resources too quickly?
   - Are any actions too powerful or too weak?

3. **Verify completeness**
   - Every scene transition leads somewhere
   - Every actor has required resources defined
   - Every feature effect is clear

### 15.14.4 Campaign Complexity Levels

**Simple** (1-2 hours play time):
- 1-3 encounters
- Minimal scenes
- Pre-made characters
- Standard rules only

**Standard** (4-8 hours play time):
- 5-8 encounters
- Branching scenes
- Character creation or pre-made options
- Some custom features

**Complex** (12+ hours play time):
- 10+ encounters
- Multiple story branches
- Full character progression
- Custom mechanics and features

### 15.14.5 Common Campaign Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Too many special rules | Players cannot remember them | Use standard mechanics, add features sparingly |
| Unwinnable encounters | Player frustration | Test and provide escape options |
| Too little direction | Players do not know what to do | Clear objectives and transitions |
| Unbalanced resources | Game too easy or too hard | Test and adjust numbers |
| Missing definitions | References to undefined content | Create a checklist and verify |

## 15.15 Campaign Example Outline

```
Campaign: The Siege of Ironhold

Overview:
A band of heroes must defend a frontier town against
an invading army. Through tactical encounters and
critical choices, players determine the town's fate.

Global Features:
- Standard Action Point System
- Health with Constitution Modifier
- Reputation Tracking

Resources:
Health, Mana, Action Points, Gold, Reputation, Morale

Content Summary:
- 3 Acts with 12 total scenes
- 8 encounters ranging from skirmishes to sieges
- 4 possible endings

Completion:
Victory: Survive 10 rounds of the final siege
Defeat: Town Morale reaches 0 or all heroes defeated

Estimated Play Time: 8-12 hours
```
