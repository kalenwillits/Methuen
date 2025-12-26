# Chapter 1: Introduction

## 1.1 What is Methuen?

Methuen is a framework for turn-based tabletop games. It provides the rules engine for tactical encounters, narrative scenes, and everything that connects them into a complete campaign.

When you play a Methuen game, you control actors on a grid-based map, making tactical decisions about movement, attacks, and abilities. You roll dice to determine outcomes, manage resources like health and action points, and navigate branching narratives that respond to your choices and successes. Every decision matters: the positioning you choose, the actions you spend, the risks you take. Victory feels earned because it emerges from the choices you made under pressure.

The framework supports role-playing games, tactical strategy games, interactive fiction, and solo play with automated opponents. Whether you want a Game Master narrating the story or a fully deterministic experience you can play alone, Methuen provides the structure.

### 1.1.1 What You Will Do

In a typical Methuen session, you will:

- **Deploy your actors** onto a tactical map, choosing positions and facing directions
- **Take turns** in initiative order, spending action points to move, attack, defend, and use special abilities
- **Roll dice** to determine whether attacks hit, how much damage they deal, and whether skill checks succeed
- **Make decisions** during narrative scenes that affect the story and unlock different paths
- **Track resources** as health depletes, abilities recharge, and currencies are spent
- **Achieve objectives** ranging from defeating all enemies to reaching an exit to surviving a set number of rounds

The tactical encounters are the heart of play: positioning matters, action economy creates meaningful choices, and the interplay between your actors and theirs produces emergent tactical situations.

### 1.1.2 Design Principles

The framework operates on these foundational principles:

1. **Determinism**: Given identical inputs, the same rules produce the same outputs. Randomness enters only through explicit dice mechanics.
2. **Resource Management**: All game states are tracked through numerical resources that actors possess and modify.
3. **Phased Gameplay**: Games progress through defined phases (scenes and encounters) with distinct rules governing each.
4. **Extensibility**: Campaigns define specific content while adhering to the core Methuen rule set.

## 1.2 Purpose of This Document

This Rule Book serves as the authoritative technical reference for the Methuen framework. It defines:

- All core terminology and their precise meanings
- The complete rule set governing gameplay
- Procedures for resolving game mechanics
- The relationship between framework components
- Default mechanics that apply when campaigns do not specify alternatives

When conflicts arise between this document and campaign-specific content, this Rule Book takes precedence unless a campaign explicitly states otherwise through a Feature (see Chapter 14).

## 1.3 How to Use This Book

### 1.3.1 Document Structure

This Rule Book is organized into the following chapters:

| Chapter | Title | Content |
|---------|-------|---------|
| 1 | Introduction | Framework overview and document usage |
| 2 | Playing Methuen | Game loop, turn structure, first session guidance |
| 3 | Dice and Expressions | Dice notation, mathematical expressions, resource injection |
| 4 | Resources | Resource rules, initialization, defaults, and constraints |
| 5 | Actors | Actor properties and capabilities |
| 6 | Actions | Action structure and execution |
| 7 | Casts | Actor groupings and shared control |
| 8 | Maps and Tiles | Grid system, spatial mechanics |
| 9 | Movement | Movement rules and patterns |
| 10 | Initiative | Turn order determination |
| 11 | Encounters | Turn-based tactical gameplay |
| 12 | Scenes | Narrative and decision phases |
| 13 | Strategies | Non-player actor control systems |
| 14 | Features | Special rules and modifications |
| 15 | Campaigns | Campaign structure and completion |

Additionally, the appendices provide:

| Appendix | Title | Content |
|----------|-------|---------|
| A | Glossary | Alphabetical definitions of all terms |
| B | Example of Play | Narrative walkthrough of a complete encounter |
| C | Quick Reference | Turn structure, action resolution, common calculations |

### 1.3.2 Reading Conventions

The following conventions are used throughout this document:

- **Bold text** indicates defined terms that appear in the Glossary (Appendix A).
- `Monospace text` indicates game notation, such as dice expressions or resource names.
- Code blocks contain example Features, Actions, or other structured game content.

Cross-references appear as "see Chapter X" or "see Section X.Y" and point to related content elsewhere in this book.

### 1.3.3 Rule Precedence

When multiple rules could apply to a situation, resolve them using this hierarchy (highest precedence first):

1. **This Rule Book** (highest precedence)
2. **Campaign Global Features**
3. **Encounter Features**
4. **Region Features**
5. **Tile Features**
6. **Cast Features**
7. **Actor Features**
8. **Action Features**
9. **Temporary Effects** (lowest precedence)

A rule of lower precedence cannot contradict a rule of higher precedence unless explicitly permitted by the higher-precedence rule.

**Note**: This hierarchy matches the Feature Scope Hierarchy defined in Chapter 14. When in doubt, more specific rules take precedence over more general rules at the same level.

## 1.4 Components Required for Play

A Methuen game session requires the following:

1. **This Rule Book**: The governing document for all gameplay.
2. **A Campaign Book**: Defines specific content, actors, maps, and scenarios.
3. **Dice**: Standard polyhedral dice as required by the campaign (commonly d4, d6, d8, d10, d12, d20, d100).
4. **Tracking Materials**: Paper, tokens, or digital tools for recording resource values.
5. **Maps**: Grid-based representations of encounter spaces (physical or digital).
6. **Tokens or Miniatures**: Representations of actors for spatial tracking during encounters.

## 1.5 The Game Loop

A Methuen game follows this fundamental structure:

```
Campaign Start
    |
    v
+--------+     +-----------+
| Scene  | --> | Encounter |
+--------+     +-----------+
    ^               |
    |               |
    +---------------+
          |
          v
    Campaign End
```

1. **Campaign Start**: Initialize campaign-defined resources and establish starting conditions.
2. **Scene Phase**: Process narrative content, player choices, and Checks.
3. **Encounter Phase**: Execute turn-based tactical gameplay on a map.
4. **Repeat**: Alternate between scenes and encounters as defined by the campaign.
5. **Campaign End**: The campaign concludes when completion conditions are met.

## 1.6 Players and Roles

Methuen supports the following participant roles:

### 1.6.1 Players

Players control one or more actors (organized into Casts) during encounters. Player responsibilities include:

- Making decisions for controlled actors
- Tracking resources for controlled actors
- Executing actions according to the rules
- Engaging with the campaign narrative

### 1.6.2 Game Master (Optional)

Some campaigns designate a Game Master who:

- Interprets ambiguous rules
- Controls non-player actors (if not using Strategies)
- Narrates scenes
- Manages campaign progression

### 1.6.3 Automated Control

Non-player actors may be controlled by Strategies (see Chapter 13), enabling fully automated or solo gameplay without a Game Master.

## 1.7 Quick Start Guide

If you want to begin playing immediately:

**Learn by example?** If you prefer seeing the game in action before reading the rules, skip ahead to Appendix B: Example of Play. It walks through a complete encounter with two players, showing initiative, actions, strategy-controlled enemies, and victory conditions.

### 1.7.1 Essential Reading

At minimum, read these sections before your first session:

1. **Chapter 2: Playing Methuen** - Understand the game loop and turn structure
2. **Chapter 4, Section 4.10: Default Mechanics** - Know what happens when you take damage and how many actions you get
3. **Chapter 6, Section 6.3: Action Structure** - Understand how actions resolve
4. **Appendix C: Quick Reference** - Keep this handy during play

### 1.7.2 First Session Setup

1. Choose a campaign book
2. Create or select your actors as directed by the campaign
3. Set up the first encounter map
4. Roll initiative
5. Begin taking turns

### 1.7.3 Default Assumptions

Unless your campaign specifies otherwise, assume these defaults:

- Actors start each turn with **3 Action Points**
- An actor reaching **0 Health is defeated** and removed from the encounter
- **Most actions cost 1 Action Point**
- **Movement is provided by campaign-defined actions** (Methuen does not assume inherent movement)
- Higher initiative acts first

See Chapter 4, Section 4.10 for complete default mechanics.

## 1.8 Definitions Preview

The following terms are used throughout this Rule Book and are formally defined in Appendix A:

- **Actor**: An entity that participates in encounters
- **Action**: An operation an actor performs
- **Resource**: A numerical value tracking actor states
- **Feature**: A special rule modifying standard gameplay
- **Campaign**: The complete game content package
- **Encounter**: A turn-based tactical phase
- **Scene**: A narrative or decision phase between encounters
- **Check**: A boolean expression determining success or failure
- **Expression**: A mathematical formula calculating numerical results
