# Chapter 14: Features

## 14.1 Overview

Features are special rules that modify how any part of a campaign operates. They provide the primary mechanism for extending, customizing, and specializing the Methuen framework to support specific campaign designs.

## 14.2 Feature Definition

### 14.2.1 Formal Definition

A **Feature** is a clearly written, unambiguous special rule that:
- Modifies standard game mechanics
- Attaches to a specific game element or applies globally
- Takes precedence according to its scope
- Is defined by the campaign

### 14.2.2 Feature Properties

| Property | Description |
|----------|-------------|
| Name | Unique identifier for the feature |
| Scope | What the feature attaches to or affects |
| Effect | The rule modification it provides |
| Duration | How long the feature remains active |
| Conditions | When the feature applies |

## 14.3 Feature Scope

### 14.3.1 Scope Hierarchy

Features exist at different levels of specificity. This hierarchy determines precedence when features conflict (see also Chapter 1, Section 1.3.3):

| Scope | Description | Precedence |
|-------|-------------|------------|
| Rule Book | Core rules in this document | Highest (supersedes all) |
| Global | Affects entire campaign | Very High |
| Encounter | Affects specific encounter | High |
| Region | Affects area of map | Medium-High |
| Tile | Affects single tile | Medium |
| Cast | Affects actor group | Medium |
| Actor | Affects single actor | Medium-Low |
| Action | Affects single action | Low |
| Temporary | Time-limited effect | Lowest |

**Note**: Higher precedence features override lower precedence features when they conflict. The Rule Book itself is the highest authority; campaign Global Features are the highest-precedence content that campaigns can define.

### 14.3.2 Global Features

**Global** features apply to all applicable situations throughout the campaign:

```
Feature: Health Maximum (Global)
No actor's Health may exceed its initial rolled value.
This applies to all actors in all encounters.
```

Global features are typically defined at the campaign level and cannot be overridden by lower-scope features.

### 14.3.3 Encounter Features

Encounter features apply only during a specific encounter:

```
Feature: Darkness (Encounter)
During this encounter, visibility is limited to 3 tiles.
Actors without Darkvision have -2 to ranged attacks.
```

### 14.3.4 Actor Features

Actor features apply to a specific actor:

```
Feature: Heavy Armor (Actor)
This actor gains +3 Defense.
This actor's movement costs are increased by 1 per tile.
```

### 14.3.5 Action Features

Action features modify specific actions:

```
Feature: Precise Strike (Action)
When using the Strike action, this actor may reroll
one attack die and take the better result.
```

## 14.4 Feature Categories

### 14.4.1 Passive Features

Passive features are always in effect while active:

```
Feature: Natural Armor
This actor has +2 Defense at all times.
```

### 14.4.2 Triggered Features

Triggered features activate when specific conditions are met:

```
Feature: Reactive Strike
When an adjacent enemy uses a ranged attack,
this actor may immediately make a melee attack
against that enemy.
```

### 14.4.3 Activated Features

Activated features require deliberate activation:

```
Feature: Second Wind
Once per encounter, as a free action, this actor
may restore [Constitution] Health.
```

### 14.4.4 Conditional Features

Conditional features only apply when conditions are met:

```
Feature: Pack Tactics
This actor gains +2 Attack when an ally is
adjacent to the same target.
```

## 14.5 Feature Effects

### 14.5.1 Resource Modification

Features may modify how resources work:

```
Feature: Vampiric
When this actor deals damage, restore Health
equal to half the damage dealt (rounded down).
```

### 14.5.2 Action Modification

Features may change how actions function:

```
Feature: Quick Draw
The first ranged attack action each turn
costs 0 Action Points instead of 1.
```

### 14.5.3 Movement Modification

Features may alter movement:

```
Feature: Nimble
This actor ignores difficult terrain.
Diagonal movement costs 1 instead of 1.5.
```

### 14.5.4 Combat Modification

Features may change combat mechanics:

```
Feature: Critical Strike
When the attack roll is a natural 20,
damage is doubled.
```

### 14.5.5 Targeting Modification

Features may change targeting rules:

```
Feature: Guardian
Adjacent allies may not be targeted by
ranged attacks while this actor is active.
```

### 14.5.6 Initiative Modification

Features may affect initiative:

```
Feature: Quick Reflexes
This actor gains +5 to initiative rolls.
```

## 14.6 Feature Duration

### 14.6.1 Permanent Features

Permanent features remain for the campaign duration:

```
Feature: Veteran (Permanent)
This actor has faced countless battles.
+1 to all combat-related checks.
```

### 14.6.2 Encounter Duration

Some features last for a single encounter:

```
Feature: Battle Focus (Encounter)
Gained at encounter start, lost at encounter end.
+2 to Attack during this encounter.
```

### 14.6.3 Turn Duration

Some features last for a number of turns:

```
Feature: Haste (3 Turns)
This actor gains an additional Action Point each turn.
Duration: 3 turns, then expires.
```

### 14.6.4 Round Duration

Some features last for a number of rounds:

```
Feature: Blessing (2 Rounds)
All allies gain +1 to Defense.
Duration: Until end of round 2 after application.
```

### 14.6.5 Conditional Duration

Some features last until a condition is met:

```
Feature: Concentration
This effect persists until the actor takes damage
or voluntarily ends it.
```

## 14.7 Feature Stacking

### 14.7.1 Same-Name Features

Features with identical names do not stack:
- Only one instance applies
- The most recent application replaces previous
- Duration resets to the new application

### 14.7.2 Different-Name Features

Features with different names stack:
- All effects apply simultaneously
- Bonuses and penalties are cumulative
- Conflicting effects are resolved by specificity

### 14.7.3 Stacking Example

```
Actor has:
  Feature: Heavy Armor (+3 Defense)
  Feature: Shield (+2 Defense)
  Feature: Blessed (+1 Defense)

Total Defense bonus: +6 (all stack)

Actor gains another "Blessed" feature:
  The new Blessed replaces the old Blessed
  Total Defense bonus: still +6
```

## 14.8 Feature Conflicts

### 14.8.1 Resolution Order

When features conflict:
1. Higher precedence scope wins
2. If same scope, more specific wins
3. If still tied, campaign specifies resolution
4. If no specification, use most recent

### 14.8.2 Explicit Override

Features may explicitly override others:

```
Feature: Unstoppable (Actor)
This feature overrides all movement restrictions.
This actor may move through impassable terrain
and cannot be immobilized.
```

### 14.8.3 Immunity Features

Some features grant immunity to effects:

```
Feature: Fire Immunity
This actor takes no damage from fire effects.
This overrides all fire damage features.
```

## 14.9 Common Feature Types

### 14.9.1 Defensive Features

```
Feature: Evasion
When targeted by an area attack, this actor
takes half damage on a failed save, no damage
on a successful save.
```

```
Feature: Resistance (Fire)
This actor takes half damage from fire effects.
```

```
Feature: Regeneration
At the start of this actor's turn,
restore 1d4 Health.
```

### 14.9.2 Offensive Features

```
Feature: Extra Attack
When taking the Attack action, this actor
may make two attacks instead of one.
```

```
Feature: Sneak Attack
When attacking a target engaged with an ally,
deal an additional 2d6 damage.
```

```
Feature: Power Strike
This actor may take -2 Attack to gain +4 damage.
```

### 14.9.3 Utility Features

```
Feature: Darkvision
This actor can see normally in darkness.
```

```
Feature: Climb
This actor can move along vertical surfaces
at normal movement speed.
```

```
Feature: Keen Senses
This actor gains +5 to Perception checks.
```

### 14.9.4 Resource Features

```
Feature: Extra Action Point
This actor has 4 Action Points instead of 3.
```

```
Feature: Mana Regeneration
At the start of each turn, restore 1 Mana.
```

```
Feature: Wealthy
This actor starts with 500 Gold instead of 100.
```

## 14.10 Feature Application

### 14.10.1 Gaining Features

Actors gain features through:
- Campaign definition (starting features)
- Scene effects (narrative acquisition)
- Check results (earned features)
- Actions (granted by effects)
- Items (equipment features)
- Level advancement (progression features)

### 14.10.2 Losing Features

Actors lose features through:
- Duration expiration
- Condition resolution
- Dispelling effects
- Item removal
- Campaign events

### 14.10.3 Feature Tracking

Track active features including:
- Feature name
- Source (how acquired)
- Duration remaining
- Conditions for loss
- Effects in play

## 14.11 Campaign Features

### 14.11.1 Campaign-Defining Features

Some features define core campaign mechanics:

```
Feature: Action Point System (Global)
All actors have an Action Points resource.
Action Points reset to 3 at the start of each turn.
Most actions cost 1 Action Point.
```

```
Feature: Health System (Global)
All actors have a Health resource.
When Health reaches 0, the actor is defeated.
Health is initialized as 10 + [Constitution].
```

### 14.11.2 Optional Rule Features

Features can implement optional rules:

```
Feature: Critical Hits (Global, Optional)
A natural 20 on attack rolls is a critical hit.
Critical hits deal double damage.
Enable this feature for more dramatic combat.
```

### 14.11.3 Difficulty Features

Features can adjust campaign difficulty:

```
Feature: Heroic Mode (Global)
All player actors gain +2 to all resources.
All non-player actors have -2 to Attack.
```

```
Feature: Nightmare Mode (Global)
All non-player actors have +20% Health.
Healing effects are reduced by 50%.
```

## 14.12 Standard Features

This section defines standard features that campaigns may use or adapt. These features provide common mechanics that many campaigns need.

### 14.12.1 Defeat at Zero Health (Recommended Default)

```
Feature: Defeat at Zero Health (Global)
Scope: Global (all actors)
Duration: Permanent

Effect:
When an actor's Health resource reaches 0, that actor is
immediately defeated.

A defeated actor:
- Is removed from the map
- No longer takes turns (removed from initiative order)
- Cannot be targeted by actions
- Does not block movement or line of sight

Notes:
- This is the assumed default if a campaign does not specify
  alternative defeat rules.
- Campaigns may override this with features like "Unconscious
  at Zero Health" or "Death Saving Throws."
```

### 14.12.2 Action Point Refresh (Recommended Default)

```
Feature: Action Point Refresh (Global)
Scope: Global (all actors)
Duration: Permanent

Effect:
At the start of each actor's turn, their Action Points resource
resets to 3.

Notes:
- Resource refresh occurs before start-of-turn features trigger.
- Campaigns may specify different Action Point totals.
- Some features may grant additional Action Points.
```

### 14.12.3 Damage Reduction (Common Defensive Mechanic)

```
Feature: Damage Reduction (Actor/Equipment)
Scope: Actor
Duration: While equipped or active

Effect:
When this actor takes damage, reduce the damage by [Armor] before
applying it to Health.

Damage cannot be reduced below 0.

Example:
  Actor has Damage Reduction 3.
  Attack deals 8 damage.
  Reduction: 8 - 3 = 5 damage applied to Health.
```

### 14.12.4 Movement Cost Modifier (Common Terrain Mechanic)

```
Feature: Difficult Terrain (Tile/Region)
Scope: Tile or Region
Duration: Permanent (until terrain changes)

Effect:
Each tile of movement into or through this tile costs 2 movement
instead of 1 (or 3 instead of 1.5 for diagonal).

Notes:
- Movement into difficult terrain is slowed, not blocked.
- Some features may grant immunity to difficult terrain.
```

### 14.12.5 Critical Hits (Optional Combat Mechanic)

```
Feature: Critical Hits (Global, Optional)
Scope: Global
Duration: Permanent

Effect:
When an attack roll results in a natural 20 (the die shows 20
before modifiers), the attack is a critical hit.

On a critical hit:
- The attack automatically hits regardless of target Defense
- Damage dice are rolled twice and summed
- Damage modifiers are applied once (not doubled)

Example:
  Attack normally deals 1d8 + 4 damage.
  On critical hit: 2d8 + 4 damage.
```

### 14.12.6 Flanking Bonus (Optional Positioning Mechanic)

```
Feature: Flanking (Global, Optional)
Scope: Global
Duration: Permanent

Effect:
When two allies are adjacent to the same enemy and positioned
on opposite sides (across from each other), both allies gain
+2 to Attack rolls against that enemy.

"Opposite sides" means the allies are separated by the enemy
along a cardinal or diagonal axis.
```

## 14.13 Feature Writing Guidelines

### 14.13.1 Clarity Requirements

Features must be:
- Unambiguous in effect
- Clear about scope
- Specific about duration
- Explicit about conditions

### 14.13.2 Complete Specification

A well-written feature includes:
- Name (unique identifier)
- Scope (what it applies to)
- Effect (what it does)
- Duration (how long it lasts)
- Conditions (when it applies)
- Interactions (how it works with other features)

### 14.13.3 Example: Complete Feature

```
Feature: Berserker Rage

Scope: Actor
Duration: Until end of encounter or until Health exceeds 50%
Condition: Activates when actor's Health drops below 25%

Effect:
- Gain +4 to Attack
- Gain +2 to damage
- Lose 2 Defense
- Cannot use healing actions on self
- Must attack nearest enemy if able

Interaction:
- Overrides features that prevent attacking
- Stacks with other attack bonuses
- Does not stack with itself
```
