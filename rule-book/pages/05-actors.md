# Chapter 5: Actors

## 5.1 Overview

An Actor is any named entity that participates in the game. Actors are the primary units of interaction within Methuen, capable of taking turns, performing actions, occupying space, and tracking resources.

## 5.2 Actor Definition

### 5.2.1 Formal Definition

An **Actor** is an entity that possesses:
- A unique name within its context
- Spatial properties (location and heading) during encounters
- Resource values
- A set of available actions
- Zero or more features

### 5.2.2 Actor Types

Actors fall into two categories based on control:

| Type | Description | Control Method |
|------|-------------|----------------|
| Player Actor | Controlled by a human player | Player decisions |
| Non-Player Actor | Not controlled by a human player | Strategy or Game Master |

Both types follow identical rules. The distinction affects only how decisions are made during play.

## 5.3 Actor Properties

### 5.3.1 Name

Every actor has a unique name that identifies it within the game context. Names are used for:
- Targeting by actions
- Narrative references
- Resource tracking
- Initiative ordering

**Naming Rules**:
- Names must be unique within a single encounter
- Names are case-sensitive
- Names may not contain special notation characters (`[]`, `{}`, etc.)

### 5.3.2 Location

During encounters, each actor occupies a position on the map grid, expressed as coordinates relative to the origin.

**Location Format**: `XD YD`

Where X and Y are distances and D are cardinal directions.

**Examples**:
- `0N 0E` - The origin
- `3N 2E` - 3 spaces north, 2 spaces east of origin
- `5S 1W` - 5 spaces south, 1 space west of origin

**Location Rules**:
- Actors occupy exactly one tile at a time (unless modified by a Feature)
- Multiple actors may occupy the same tile (unless prohibited by a Feature)
- Location is only tracked during encounter phases

### 5.3.3 Heading

Heading indicates the direction an actor is facing. Heading affects:
- Radial calculations
- Directional abilities (if defined by campaign)
- Visual representation

**Valid Headings**:

| Heading | Direction |
|---------|-----------|
| N | North |
| NE | Northeast |
| E | East |
| SE | Southeast |
| S | South |
| SW | Southwest |
| W | West |
| NW | Northwest |

**Heading Rules**:
- All actors have a heading at all times during encounters
- Default heading is N (north) unless specified otherwise
- Heading changes do not consume movement unless specified by a Feature

### 5.3.4 Radial

Radials provide directional information relative to an actor's current heading, using clock-face notation. This allows actions and features to reference directions like "in front of" or "to the left" without knowing the actor's absolute heading.

**Radial Values**:

| Radial | Position | Description |
|--------|----------|-------------|
| 12 | Directly ahead | Same as heading |
| 3 | Directly right | 90 degrees clockwise from heading |
| 6 | Directly behind | Opposite of heading |
| 9 | Directly left | 90 degrees counter-clockwise from heading |

**Intermediate Radials**:

| Radial | Position |
|--------|----------|
| 1-2 | Forward-right diagonal |
| 4-5 | Rear-right diagonal |
| 7-8 | Rear-left diagonal |
| 10-11 | Forward-left diagonal |

**Radial Mapping by Heading**:

| Heading | 12 (Front) | 3 (Right) | 6 (Back) | 9 (Left) |
|---------|------------|-----------|----------|----------|
| N | N | E | S | W |
| NE | NE | SE | SW | NW |
| E | E | S | W | N |
| SE | SE | SW | NW | NE |
| S | S | W | N | E |
| SW | SW | NW | NE | SE |
| W | W | N | E | S |
| NW | NW | NE | SE | SW |

**Example**: An actor facing East (heading E) has radial 12 pointing East, radial 3 pointing South, radial 6 pointing West, and radial 9 pointing North.

**Note**: Radials are only used in campaigns that explicitly reference them. Many campaigns use only absolute directions (N, E, S, W).

### 5.3.5 Resources

Each actor has values for all resources defined in the campaign. Resources are tracked using lazy initialization (see Chapter 4).

**Resource Access**:
- An actor's own resource: `[ResourceName]`
- Another actor's resource: `[Target ResourceName]` or `[ActorName ResourceName]`

### 5.3.6 Actions

Each actor has a set of actions they may perform. Actions are defined by:
- The campaign (standard actions available to all or some actors)
- The actor's definition (actor-specific actions)
- Features (actions granted by special rules)

See Chapter 6 for complete action rules.

### 5.3.7 Features

Features are special rules that modify how an actor operates. Actor features may:
- Grant new actions
- Modify existing actions
- Change resource behavior
- Alter movement capabilities
- Provide conditional effects

See Chapter 14 for complete feature rules.

## 5.4 Actor Definition Format

Campaigns define actors using a structured format. A complete actor definition includes:

```
Actor: [Name]
Location: [Starting Location]
Heading: [Starting Heading]
Resources:
  [Resource]: [Value]
  [Resource]: [Value]
Actions:
  [Action Name]
  [Action Name]
Features:
  [Feature Name]
  [Feature Name]
```

### 5.4.1 Minimal Actor Definition

At minimum, an actor requires only a name:

```
Actor: Training Dummy
```

All other properties use defaults:
- Location: Determined at deployment
- Heading: N
- Resources: Initialized when accessed
- Actions: None (unless provided by campaign defaults)
- Features: None

### 5.4.2 Complete Actor Definition Example

```
Actor: Knight Commander
Location: 5N 3E
Heading: S
Resources:
  Health: 45
  Strength: 8
  Defense: 6
  Action Points: 3
Actions:
  Strike
  Shield Bash
  Rally
  Move
Features:
  Leadership Aura
  Heavy Armor
```

## 5.5 Actor States

### 5.5.1 Active State

An actor in active state:
- Takes turns during encounters
- May perform actions
- May be targeted by actions
- Occupies space on the map

### 5.5.2 Inactive State

An actor may become inactive through various means (defined by Features). Inactive actors:
- Do not take turns
- Cannot perform actions
- May or may not be targetable (as defined)
- May or may not occupy space (as defined)

**Common Inactive Conditions**:
- Defeated (Health reduced to 0)
- Removed from play
- Stunned or incapacitated
- Not yet deployed

### 5.5.3 State Transitions

Campaigns define conditions for state transitions using Features.

**Example**:
```
Feature: Defeat
When an actor's Health reaches 0, that actor becomes
inactive and is removed from the map.
```

## 5.6 Actor Relationships

### 5.6.1 Affiliation

Campaigns may define affiliations that group actors for targeting purposes.

**Common Affiliations**:
- Ally: Same cast or friendly cast
- Enemy: Opposing cast
- Neutral: Neither ally nor enemy

### 5.6.2 Targeting

Actors may target other actors with actions. Targeting rules:
- An actor may target itself unless prohibited
- An actor may target allies unless prohibited
- An actor may target enemies unless prohibited
- Range and line of sight may restrict valid targets

### 5.6.3 Adjacency

Two actors are adjacent if their occupied tiles are adjacent (sharing an edge or corner). Adjacency is used for:
- Melee range actions
- Opportunity reactions
- Area effects

## 5.7 Actor Lifecycle

### 5.7.1 Creation

Actors are created when:
- Defined by the campaign at start
- Spawned during an encounter by an effect
- Introduced through a scene

### 5.7.2 Deployment

Actors are deployed to a map during the deployment phase of an encounter. Deployment establishes:
- Initial location
- Initial heading
- Active state

### 5.7.3 Participation

Active actors participate in encounters by:
- Rolling initiative (or using cast initiative)
- Taking turns in initiative order
- Performing actions
- Being affected by other actors' actions

### 5.7.4 Removal

Actors are removed from an encounter when:
- A defeat condition is met
- An effect removes them
- The encounter ends

### 5.7.5 Persistence

Actor state (resources, features) may persist between encounters as defined by the campaign. Persistent actors retain their resource values and acquired features.

## 5.8 Special Actor Types

### 5.8.1 Object Actors

Some actors represent objects rather than characters. Object actors:
- May have limited or no actions
- Often have simplified resource sets
- May be interacted with by other actors

**Example**: Door, Treasure Chest, Trap

### 5.8.2 Environmental Actors

Environmental actors represent dynamic map elements. They:
- May affect areas rather than single tiles
- Often operate on automatic triggers
- May not take traditional turns

**Example**: Moving Platform, Spreading Fire, Collapsing Floor

### 5.8.3 Composite Actors

Some actors occupy multiple tiles. Composite actors:
- Have a primary tile (location) and secondary tiles
- May be targeted at any occupied tile
- Have special movement rules

**Example**: Large Creature (2x2 tiles), Dragon (3x3 tiles)

Composite actors require explicit Feature definitions for their behavior.

## 5.9 Actor Creation

Actor creation is the process of defining a new actor's properties before play begins. While specific methods vary by campaign, this section describes the general framework and common approaches.

### 5.9.1 Campaign-Defined Creation

Each campaign specifies its own actor creation system. A campaign's creation rules typically define:

- Which resources actors possess and their starting ranges
- How resource values are determined (random, assigned, or purchased)
- What actions and features are available
- Any restrictions based on actor type, class, or role

When playing a campaign, follow its creation rules exactly. The guidance below describes common patterns you may encounter.

### 5.9.2 Common Creation Methods

Campaigns typically use one of these approaches for determining resource values:

**Random Generation**
```
Roll dice for each resource according to campaign formulas.
Example: Strength = 1d6+2 (range 3-8)
```
Random generation creates variety but may produce unbalanced actors.

**Point Buy**
```
Receive a budget of points (e.g., 25 points).
Spend points to increase resources from a base value.
Higher values cost more points.
```
Point buy ensures balanced actors and gives players control over their build.

**Template Selection**
```
Choose a predefined template (class, archetype, or role).
The template provides fixed starting values.
```
Templates speed creation and ensure viable actor builds.

**Hybrid Methods**
```
Combine approaches: select a template, then customize with
limited point allocation or random rolls for specific resources.
```

### 5.9.3 Creation Procedure

A typical actor creation process follows these steps:

1. **Choose a name** - Select a unique identifier for the actor
2. **Determine core resources** - Use the campaign's method to set primary resource values
3. **Calculate derived resources** - Apply any formulas (e.g., Health = 10 + Constitution)
4. **Select actions** - Choose from available actions or receive them from a class/template
5. **Select features** - Choose or receive special rules that modify the actor
6. **Record the actor definition** - Document all properties in the standard format

### 5.9.4 Player Actor Example

**Creating a Fighter for "The Dark Citadel" campaign:**

```
Step 1: Choose a Name
  Actor: Sera Brightblade

Step 2: Roll or Assign Capabilities (per campaign rules)
  Strength:     6 (rolled 1d6+2)
  Dexterity:    4 (rolled 1d6)
  Constitution: 5 (rolled 1d6+1)
  Intelligence: 3 (rolled 1d6-1)
  Wisdom:       4 (rolled 1d6)

Step 3: Calculate Derived Resources
  Health: 10 + Constitution = 15
  Health Maximum: 15

Step 4: Select Actions (Fighter class provides)
  Strike, Defend, Move, Shield Bash

Step 5: Select Features (Fighter class provides)
  Heavy Armor (+2 Defense)
  Shield Bearer (+1 Defense when wielding shield)

Final Actor Definition:
  Actor: Sera Brightblade
  Resources:
    Health: 15 (Maximum: 15)
    Strength: 6
    Dexterity: 4
    Constitution: 5
    Intelligence: 3
    Wisdom: 4
    Defense: 5 (base 2 + Heavy Armor + Shield)
    Action Points: 3
  Actions: Strike, Defend, Move, Shield Bash
  Features: Heavy Armor, Shield Bearer
```

### 5.9.5 Comparison: Player Actor vs Enemy Actor

| Property | Sera Brightblade (Player) | Goblin Warrior (Enemy) |
|----------|---------------------------|------------------------|
| Control | Player decisions | Strategy: Aggressive |
| Health | 15 | 8 |
| Strength | 6 | 3 |
| Defense | 5 | 2 |
| Actions | Strike, Defend, Move, Shield Bash | Strike, Move |
| Features | Heavy Armor, Shield Bearer | Pack Tactics |
| Complexity | High (many options) | Low (simple behavior) |

Player actors typically have more resources, options, and features. Enemy actors are designed for simpler, faster play during encounters.
