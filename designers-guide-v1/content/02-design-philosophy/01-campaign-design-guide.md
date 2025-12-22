# Campaign Design Guide

## Welcome Campaign Designers

This chapter begins Part II of the handbook—the comprehensive guide to creating Methuen campaigns. If you haven't read Part I (Fundamentals), do so now to understand the player experience you're designing for.

## What is Campaign Design?

As a campaign designer, you'll create all the content that makes an Methuen game playable:

- Resources and their initialization rules
- Actions actors can perform
- Features and effects
- Maps and encounters
- Win/loss conditions

The framework provides structure; you provide content.

## Design Philosophy

### Standardization Enables Portability

Players who learn Methuen can play any campaign without re-learning core rules. Your job is to work within the framework while creating unique experiences.

**Design Within Constraints**:
- Use if/do/then/else for actions
- Resources are positive integers only
- Expressions use supported operators
- Grid-based positioning

**Innovate Through Content**:
- Choose which resources matter
- Define creative actions
- Design interesting maps
- Create compelling scenarios

### Precision Over Ambiguity

Methuen has no game master to adjudicate unclear situations. Every rule must be unambiguous:

**Good**: "Move up to Dexterity spaces per turn"
**Bad**: "Move a reasonable distance"

**Good**: "Deal 1d6+Strength damage"
**Bad**: "Deal significant damage"

**Good**: "If Health reaches 0, actor is removed from map"
**Bad**: "If Health gets too low, something bad happens"

### Balance Complexity and Accessibility

**Start Simple**: New campaigns should have:
- 5-10 core resources
- 3-5 basic actions per actor
- Clear objectives
- Straightforward maps

**Add Depth Gradually**: Introduce complexity through:
- Additional actions
- Resource interactions
- Environmental mechanics
- Advanced scenarios

## Scope and Player Count

### Determining Scope

**One-Shot** (1-3 hours):
- Single map
- Clear objective
- 3-5 resources
- 5-8 actions

**Short Campaign** (4-10 hours):
- 2-4 maps
- Progressive difficulty
- 6-10 resources
- 10-15 actions

**Long Campaign** (10+ hours):
- Multiple maps/world
- Complex systems
- 10+ resources
- 15+ actions
- Progression mechanics

### Player Count

Define recommended player counts:

**Solo**: One player, one or more actors
**Small Group**: 2-3 players
**Large Group**: 4-6 players
**Massive**: 7+ players (requires careful design)

Design considerations:
- Turn length increases with player count
- Complexity should decrease as player count increases
- Balance encounters for expected actor count

## Genre and Theme

Methuen supports many genres:

### Tactical Scenarios
Resource management in direct conflict situations

### City Building
Constructing and developing structures over time

### Resource Gathering
Collecting, processing, and trading materials

### Farming/Simulation
Managing crops, livestock, or other renewable resources

**Your theme doesn't change the framework**—only the content flavor.

## Playtesting

Before publishing your campaign:

###  Solo Playtest
Play both sides yourself to check:
- Rules clarity
- Balance issues
- Missing definitions
- Pacing problems

### Group Playtest
Have others play to discover:
- Confusing rules
- Unintended strategies
- Engagement level
- Actual play time

### Iterate
Revise based on feedback:
- Clarify ambiguous rules
- Rebalance overpowered elements
- Add missing content
- Simplify where needed

## Campaign Book Structure

Organize your campaign book for easy reference:

**1. Introduction**
- Theme and genre
- Recommended players
- Required materials
- Estimated play time

**2. Setup Guide**
- Actor creation steps
- Starting resources
- Map placement
- Initial scenario

**3. Resource Glossary**
- Alphabetical resource list
- Initialization rules
- Special properties

**4. Action Reference**
- All available actions
- Organized by category or alphabetically

**5. Features and Effects**
- Passive rules
- Triggered effects
- Environmental mechanics

**6. Maps and Scenarios**
- Map layouts
- Tile properties
- Encounter details
- Objectives

**7. Quick Reference**
- Turn structure summary
- Common calculations
- Important tables

### Encounter Chapters vs Entity Definitions

For multi-encounter campaigns, separate **scenario descriptions** from **entity definitions**:

**Encounter Chapters** (describe what happens):
- Map layouts
- Enemy placement and starting positions
- Objectives and victory conditions
- Environmental features specific to this encounter
- Loot and rewards
- **Reference** entities defined elsewhere

**Entity Definition Chapter** (define reusable components):
- Player actions (Melee Strike, Ranged Shot, Flames, etc.)
- NPC actors (Bandit, Draugr, Necromancer, Boss, etc.)
- NPC strategies and behaviors
- Shared features
- **Do NOT repeat** in encounter chapters

### Why Separate Them?

**Before (Mixed Content - Harder to Use)**:
```
Chapter 3: Encounter 1 - The Road
Map: [map layout]
Enemies: 3 Bandits at positions...
Victory: Defeat all bandits

Bandit (Actor)
Health: 25
ActionPoints: 2
Melee Strike (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 4)
then: [ActionPoints] -= 1

---

Chapter 4: Encounter 2 - Dark Crypt
Map: [map layout]
Enemies: 3 Draugr at positions...
Victory: Defeat all draugr

Draugr (Actor)
Health: 45
ActionPoints: 2
Frost Touch (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 3), apply Frost 1
then: [ActionPoints] -= 1
```

**Problem**: Entity definitions are scattered. If you want to know what a Bandit can do, you have to flip back to Chapter 3. If Bandits appear in Chapter 5, do you copy-paste the definition or reference Chapter 3?

**After (Separated - Easier to Use)**:
```
Chapter 3: Encounter 1 - The Road
Map: [map layout]
Enemies: 3 Bandits (see Ch 8) at positions X, Y, Z
Victory: Defeat all bandits
New Mechanics: Half Cover
Loot: 37 gold, Health Potion

---

Chapter 4: Encounter 2 - Dark Crypt
Map: [map layout]
Enemies: 3 Draugr (see Ch 8) at positions A, B, C
Victory: Defeat all draugr
New Mechanics: Darkness, Traps
Loot: 65 gold, Ancient Nord Blade

---

Chapter 8: Entity Definitions

Bandit (Actor)
Health: 25
ActionPoints: 2

Strategy: Aggressive Melee
Behavior 1: Attack if adjacent
Behavior 2: Move toward nearest enemy

Melee Strike (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 4)
then: [ActionPoints] -= 1

---

Draugr (Actor)
Health: 45
ActionPoints: 2
Features: Frost Resistance 50%, Undead

Strategy: Relentless Assault
Behavior 1: Use Frost Touch if adjacent
Behavior 2: Move toward nearest enemy

Frost Touch (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 3), apply Frost 1
then: [ActionPoints] -= 1
```

**Benefits**:
- All NPC definitions in one place (easy reference)
- Encounters are concise (just scenario details)
- Can reuse entities across multiple encounters
- Players know where to look for rules
- No duplication or inconsistency

### Recommended Structure for Multi-Encounter Campaigns

```
Chapter 1: Introduction
Chapter 2: Setup (character creation)
Chapter 3: Encounter 1
Chapter 4: Encounter 2
Chapter 5: Encounter 3
Chapter 6: Encounter 4 (final)
Chapter 7: Quick Reference
Chapter 8: Entity Definitions ← All actors, actions, strategies here
```

### What Goes in Each Type of Chapter

**Encounter Chapters Include:**
- Map layout (ASCII art, grid notation)
- Enemy names, quantities, starting positions
- Victory/defeat conditions
- New mechanics introduced
- Loot table or specific rewards
- Narrative/flavor text
- **References** to entity definitions (e.g., "see Ch 8")

**Encounter Chapter Example:**
```
# Encounter 2: Outer Crypts

## Map

[ASCII map grid here]

## Enemies

- 3× Draugr (see Ch 8: Entity Definitions)
  - Draugr 1: Position 5N 3E, facing South
  - Draugr 2: Position 8N 8E, facing West
  - Draugr 3: Position 2N 10E, facing South

## New Mechanics

- Darkness: Ranged and spell attacks have -5 penalty
- Traps: Pressure plates deal 1d6 damage when stepped on

## Victory Condition

Defeat all Draugr and reach the exit (12N 6E)

## Loot

- Gold: 65 (distributed among defeated enemies)
- Ancient Nord Blade (Feature): +3 melee dmg, +1d4 frost
```

**Entity Definition Chapter Includes:**
- Complete actor definitions (resources, features)
- All actions with full if/do/then/else structures
- NPC strategies and behaviors
- Shared features used across campaign
- **Do NOT include:** Encounter-specific details

**Entity Definition Chapter Example:**
```
# Entity Definitions

## Player Actions

### Melee Strike (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 2)
then: [ActionPoints] -= 1

### Ranged Shot (Action)
if: [Arrows] >= 1 AND target within 15 spaces
do: [Target Health] -= (1d6 + 2), [Arrows] -= 1
then: [ActionPoints] -= 1

## NPC Actors

### Bandit (Actor)
Resources:
  Health: 25
  ActionPoints: 2
  Defense: 1

Strategy: Aggressive Melee (see Strategies section)

### Draugr (Actor)
Resources:
  Health: 45
  ActionPoints: 2
  Defense: 3

Features:
  - Frost Resistance: 50%
  - Undead: Immune to poison and fear

Strategy: Relentless Assault (see Strategies section)

## NPC Actions

### Frost Touch (Action)
Available to: Draugr
if: Adjacent to target
do: [Target Health] -= (1d6 + 3), apply Frost 1
then: [ActionPoints] -= 1

## NPC Strategies

### Aggressive Melee (Strategy)
Behavior 1: If adjacent to enemy, use Melee Strike
Behavior 2: If enemy within 10 spaces, move toward enemy
Behavior 3: Move randomly

### Relentless Assault (Strategy)
Behavior 1: If adjacent to enemy, use Frost Touch
Behavior 2: If enemy within sight, move toward nearest enemy
Behavior 3: (None - always performs Behavior 2)
```

### When to Use This Pattern

**Use Separate Encounter/Entity Chapters When:**
- Campaign has 3+ encounters
- NPCs appear in multiple encounters
- You want clean, referenceable structure
- You value avoiding duplication

**Use Mixed Content (Entities in Encounters) When:**
- Single-encounter campaign
- Each encounter has unique enemies (no reuse)
- Campaign is very short (1-2 hours)

### Quick Decision Guide

| Campaign Size | Structure |
|---------------|-----------|
| 1 encounter | Mixed (entities in encounter) |
| 2 encounters | Mixed acceptable |
| 3-4 encounters | **Separate chapters recommended** |
| 5+ encounters | **Separate chapters required** |

## Design Principles

### Economy of Resources

Don't create resources that:
- Are only used once
- Duplicate other resources
- Add complexity without depth

### Meaningful Choices

Every action should present decisions:
- Spend resources now or save?
- Target this actor or that one?
- Move closer or maintain distance?

### Clear Feedback

Players should always know:
- Current game state
- Available options
- Consequences of choices

### Fail States

Define clearly what happens when:
- Resources reach zero
- Objectives fail
- Time/turns run out

## Progressive Complexity in Multi-Encounter Campaigns

When designing campaigns with multiple encounters, introduce mechanics gradually rather than overwhelming players with everything at once.

### The Onboarding Curve

**Encounter 1: Foundation**
- Core mechanics only (movement, basic actions, health/AP)
- Simple map with minimal terrain features
- Straightforward objective (defeat enemies, reach location)
- Focus: Learning the framework

**Encounter 2: First Expansion**
- Introduce 1-2 new mechanics (cover, elevation, consumables)
- Build on core mechanics from Encounter 1
- Slightly more complex map
- Focus: Tactical options expand

**Encounter 3: Combination**
- Add 1-2 more mechanics (status effects, special tiles)
- Combine mechanics from Encounters 1 and 2
- Multi-phase combat or objectives
- Focus: Mastery through combination

**Encounter 4+: Full Complexity**
- All mechanics available
- Complex interactions
- Strategic depth
- Focus: Applying mastery

### Example: Tactical Fantasy Campaign

**Encounter 1 - Roadside Ambush**:
- New: Half Cover (basic terrain interaction)
- Actions: Melee Strike, Ranged Shot, Move
- Map: Simple road with rocks for cover
- Enemies: 3 basic bandits
- Lesson: Cover matters for positioning

**Encounter 2 - Dark Crypt**:
- New: Darkness (-5 ranged penalty), Traps, Consumables (potions)
- Carried Forward: Half Cover, basic actions
- Map: Crypt with dark rooms and pressure plates
- Enemies: 3 tougher undead
- Lesson: Environment affects tactics

**Encounter 3 - Ritual Chamber**:
- New: Ice Slicks (movement challenge), Elevation (+2 ranged from high ground), Lockpicking
- Carried Forward: Darkness, Cover, Traps, Consumables
- Map: Multi-level chamber with hazards
- Enemies: Elite enemy + caster (2 total, but harder)
- Lesson: Positioning and resource management are crucial

**Encounter 4 - Final Showdown**:
- New: Boss mechanics (multi-phase, special abilities), Interactive objects (destroy altar to weaken boss)
- Carried Forward: ALL previous mechanics
- Map: Large arena with all terrain types
- Enemies: Boss + minions with coordinated strategy
- Lesson: Apply everything learned

### Design Pattern: Mechanic Introduction

For each new mechanic, follow this structure:

**1. Introduce Clearly**
- Name the mechanic in encounter description
- Explain the rule before play starts
- Show an example in the map setup

**2. Make It Matter**
- The new mechanic should affect the encounter outcome
- Not optional or ignorable
- Creates new tactical decisions

**3. Limit Simultaneous Novelty**
- Introduce 1-2 new mechanics per encounter, not 5
- Give players time to understand each one
- Build confidence before adding more

**4. Callback Previous Mechanics**
- Don't drop old mechanics when adding new ones
- Show how they interact
- Reward players who remember earlier lessons

### Mechanic Complexity Tiers

Organize mechanics by cognitive load:

**Tier 1 - Core Mechanics** (Encounter 1):
- Movement and range
- Basic attacks
- Health and Action Points
- Defeat conditions

**Tier 2 - Tactical Modifiers** (Encounter 2-3):
- Cover and concealment
- Elevation
- Difficult terrain
- Status effects (burning, poison, etc.)

**Tier 3 - Resource Systems** (Encounter 3-4):
- Consumables (potions, ammo)
- Secondary resources (Stamina, Magicka)
- Loot and equipment
- Skill checks

**Tier 4 - Advanced Interactions** (Encounter 4+):
- Multi-phase encounters
- Environmental triggers
- Boss mechanics
- Coordinated enemy behaviors

### Pacing Guidelines

**Too Fast**: Introducing 5 new mechanics in Encounter 1
- Players are overwhelmed
- Miss important rules
- Feel lost and frustrated

**Too Slow**: Same mechanics for all 6 encounters
- Players are bored
- No sense of progression
- Campaign feels repetitive

**Good Pace**: 1-2 new mechanics per encounter, building on previous
- Players feel challenged but competent
- Clear sense of progression
- Each encounter feels fresh

### Testing Your Complexity Curve

After designing your encounters, verify:

- [ ] Encounter 1 has minimal mechanics (4-6 total)
- [ ] Each subsequent encounter adds 1-2 new mechanics
- [ ] Previous mechanics remain relevant
- [ ] Final encounter uses most/all mechanics
- [ ] No single encounter has more than 8-10 active mechanics
- [ ] New mechanics are explained before they matter

### Exception: One-Shot Scenarios

Single-encounter scenarios can introduce more mechanics simultaneously because there's no onboarding curve to manage. However, still limit total complexity to prevent overwhelm:

- One-shot: 6-8 mechanics maximum
- Multi-encounter campaigns: 4-6 mechanics in Encounter 1, scale to 10-12 by finale

## Narrative Structure and Story Pacing

While Methuen is a deterministic framework focused on tactical gameplay, campaigns can still tell compelling stories through scenario design and environmental storytelling.

### The Role of Narrative in Methuen

**What Methuen Does NOT Have:**
- Branching dialogue trees
- Character-driven plot choices
- Narrative consequences of player decisions
- Story-driven character development

**What Methuen DOES Support:**
- Environmental storytelling through map design
- Progressive difficulty creating tension arc
- Themed encounters building to climax
- Victory conditions that resolve story premise

### Story Structure for Multi-Encounter Campaigns

Use the classic three-act structure mapped to encounters:

**Act 1: Setup (Encounters 1-2)**
- Establish the threat or goal
- Introduce the world through mechanics and flavor text
- Teach core gameplay
- End with escalation (hint at bigger threat)

**Act 2: Escalation (Encounters 3-4)**
- Raise the stakes
- Introduce complications (new enemy types, environmental challenges)
- Push players to use learned skills
- Build toward confrontation

**Act 3: Resolution (Final Encounter)**
- Climactic battle or challenge
- All mechanics come together
- Clear victory/defeat outcome
- Narrative payoff

### Example: "The Skyrim Conspiracy" Narrative Arc

**Act 1: Setup**
- **Encounter 1 (The Road)**: Hired to investigate bandit activity. Simple roadside ambush. *Hook*: Bandits have unusual coordination and equipment.
- **Encounter 2 (Outer Crypts)**: Trail leads to ancient crypt. Fight undead Draugr. *Escalation*: Discover evidence of necromantic ritual preparation.

**Act 2: Escalation**
- **Encounter 3 (Inner Sanctum)**: Deeper in crypt, find Necromancer raising Draugr army. Defeat elite Draugr Wight. *Complication*: Necromancer escapes, ritual is nearly complete.

**Act 3: Resolution**
- **Encounter 4 (Ritual Chamber)**: Confront Harkan the Undying attempting to become a lich. Multi-phase boss fight with altar destruction mechanic. *Climax*: Prevent ritual, save Skyrim. *Resolution*: Campaign victory.

**Narrative Techniques Used:**
- Each encounter reveals more information (bandits → undead → necromancer → lich ritual)
- Physical progression deeper into crypt mirrors story escalation
- Loot and environmental details tell story (ancient texts, ritual preparations)
- Final boss name and goal callback initial hook

### Environmental Storytelling Techniques

**Map Design as Narrative:**
```
Encounter 2: Outer Crypts
Map shows: Collapsed burial chambers, broken coffins, disturbed graves
Narrative implication: Someone has been desecrating this tomb recently
```

**Loot as Story Clues:**
```
Encounter 2 Loot includes: "Necromancer's Journal Fragment"
Flavor text: "...the ritual requires three dozen souls... the surface dwellers will serve..."
Narrative payoff: Foreshadows Encounter 4's mass resurrection attempt
```

**Enemy Composition as Worldbuilding:**
```
Encounter 3: Draugr Wight (elite) + Necromancer
Narrative implication: The Necromancer is experimenting with more powerful undead
Design payoff: Prepares players for even stronger boss in Encounter 4
```

### Flavor Text vs. Mechanical Text

Separate story elements from rules:

**Mechanical (Required):**
```
Victory Condition: Defeat all enemies
```

**Flavor (Optional, enhances experience):**
```
Victory Condition: Defeat all enemies

"As Harkan's form crumbles to ash, the dark energy dissipates. The ritual is broken.
Skyrim is safe... for now."
```

**Best Practice:** Write mechanical rules first, add flavor text after. Flavor enhances but never replaces clear rules.

### Narrative Pacing Guidelines

**Encounter Length and Story Beats:**
- **Short encounters (15-30 min)**: One story beat (reveal clue, introduce threat)
- **Medium encounters (30-60 min)**: Two story beats (complication + partial resolution)
- **Boss encounters (60-90 min)**: Three story beats (confrontation + escalation + resolution)

**Information Delivery:**
- **Before encounter**: Setup (why are we here? what's the goal?)
- **During encounter**: Environmental details (map features, enemy behaviors suggest story)
- **After encounter**: Payoff (loot with story implications, what changed?)

### Campaign Tone Through Mechanics

Different mechanics support different narrative tones:

**Heroic Fantasy** (Players are powerful):
- Generous starting resources
- Powerful loot progression
- Minion-style enemies (many weak foes)
- Heroic last stands (mechanics that reward low health)

**Survival Horror** (Players are vulnerable):
- Limited resources (ammo, health)
- Scarce healing
- Dangerous environment (traps, hazards)
- Fleeing as viable strategy

**Tactical Military** (Players are professional):
- Cover and positioning crucial
- Ammunition tracking
- Coordinated enemy behaviors
- Objectives beyond "kill all enemies"

**Epic Conquest** (Players are commanders):
- Large-scale battles
- Resource management (troops, supplies)
- Territory control objectives
- Long-term progression

Match your mechanical design to your intended narrative tone.

### Optional: Emergent Narrative

Players create their own stories through gameplay. Support this by:

**Memorable Moments Through Design:**
- Critical successes/failures (natural 20/1 on d20)
- Clutch victories (win with 1 HP remaining)
- Tactical brilliance (clever use of environment)
- Dramatic failures (total party wipe)

**Track Player Choices:**
```
Running Tally (optional resource)
[BanditsKilled], [StealthKills], [PotionsUsed], [CiviliansRescued]

Award different titles at campaign end based on playstyle
```

### Narrative Checklist

For each campaign, verify:

- [ ] Each encounter has clear setup (why are we here?)
- [ ] Story escalates from encounter to encounter
- [ ] Final encounter provides narrative resolution
- [ ] Map design supports theme and story
- [ ] Loot or environmental details hint at larger narrative
- [ ] Victory condition resolves the story premise
- [ ] Flavor text enhances without obscuring mechanics
- [ ] Tone matches mechanical design

### When to Skip Narrative

Not all campaigns need story:

**Skip narrative focus when:**
- Creating pure tactical puzzles
- Designing arena combat scenarios
- Building mechanical demonstrations
- Testing new systems

**Focus on narrative when:**
- Creating campaign-length experiences
- Targeting players who value immersion
- Building themed content (historical, literary adaptation)
- Designing memorable one-shots

---

## See Also

- **Chapters 12-20**: Detailed design guidelines for each system
- **Chapter 21**: Templates - Reusable formats
- **Chapter 22**: Glossary - All framework terms
