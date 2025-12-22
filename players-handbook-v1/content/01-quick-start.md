# Quick Start Guide

Welcome to Methuen! This quick-start guide will get you playing in minutes. For deeper explanations, see the referenced chapters throughout.

## What is Methuen?

**Methuen** is a tactical tabletop game framework focused on resource management and strategic decision-making. Unlike traditional tabletop RPGs:

- **No game master required**: All rules resolve deterministically
- **Resource-driven**: Everything is tracked through measurable resources
- **Tactical positioning**: Grid-based maps with precise movement
- **Standardized framework**: Core rules work across all campaigns

### What You Need

- **Campaign book**: Defines the specific game content
- **Polyhedral dice**: Standard set (d4, d6, d8, d10, d12, d20)
- **Character sheet**: Track your actor's resources and actions
- **Map and markers**: Grid-based map with position markers
- **Pen and paper**: Record keeping

## The Absolute Basics

### Actors

An **actor** is any named entity in the game world—your character, NPCs, enemies, or even environmental elements.

Every actor has:
- **Name**: Unique identifier
- **Location**: Grid coordinates (e.g., 3N 2E)
- **Heading**: Direction faced (N, NE, E, SE, S, SW, W, NW)
- **Resources**: Numerical values tracking everything important
- **Actions**: Operations they can perform

### Resources

A **resource** is any value represented as a positive integer (0 or higher):
- **Capabilities**: Strength, dexterity, intelligence
- **States**: Health, energy, focus
- **Currencies**: Gold, materials, ammunition
- **Counters**: Actions remaining, uses left

**Key Rules**:
- Resources are always ≥ 0 (never negative)
- Resources are whole numbers (no fractions)
- Resources initialize at 0 unless campaign specifies otherwise
- All actors have access to all resources (but values differ)

**Example**: Your actor starts without "Health" recorded. When first referenced, you look up the campaign's initialization rule: "Health = 1d20 + Constitution". You roll 15, add your Constitution of 12, and write "Health: 27" on your sheet.

### Dice Notation

Methuen uses standard polyhedral dice with this notation:

- **XdY**: Roll X dice with Y sides
  - `1d6` = roll one 6-sided die
  - `2d10` = roll two 10-sided dice and add them
  - `3d4` = roll three 4-sided dice and add them

### Grid and Movement

Maps use coordinate grids with 8 directions:
- **Cardinals**: N, E, S, W
- **Diagonals**: NE, SE, SW, NW

**Position notation**: `3N 2E` means 3 spaces North, 2 spaces East from the origin point

## Your First Turn

### 1. Read the Campaign Book

Your campaign book tells you:
- What resources exist and how they initialize
- What actions your actor can perform
- How movement and initiative work
- What the victory condition is

**Start here**: Read the campaign's "Getting Started" or "Character Creation" section.

### 2. Create Your Actor

Follow your campaign's character creation rules:
1. Choose or generate a name
2. Initialize starting resources (roll dice as specified)
3. Record your starting location and heading
4. Note which actions you can perform
5. Fill in any features (special rules about your actor)

### 3. Determine Initiative

**Initiative** determines turn order. Higher initiative acts first.

Your campaign will specify initiative through a **Feature** (a campaign-level rule). Common examples:

```
Initiative Roll (Feature)
Roll 1d20 + [Dexterity] at start of encounter
Highest result goes first each round
```

```
Speed-Based Initiative (Feature)
Initiative equals [Speed]
Highest Speed acts first
```

> For more on Features, see **Chapter 3: Features**.

### 4. Take Actions

When it's your turn, you can perform **actions**. Each action has four components:

- **if**: Condition check (boolean expression that evaluates to true or false)
- **do**: Effects executed when the condition is TRUE
- **then**: Effects that ALWAYS execute (regardless of condition outcome)
- **else**: Effects executed when the condition is FALSE (optional)

**Execution order**: (if) → [true: (do), false: (else)] → (then)

Here's a simple example called `Basic Attack`:

```
Basic Attack (Action)
Range: Adjacent
Target: Single actor

if: [ActionPoints] >= 1
do: [Target Health] -= 1d6
then: [ActionPoints] -= 1
```

**How it works**:

1. **Check condition**: Do you have at least 1 ActionPoint?
2. **If TRUE**: Deal 1d6 damage to the target's Health (this is the `do` effect)
3. **Always**: Reduce ActionPoints by 1 (this is the `then` effect)

Notice there's no `else` component. If you don't have enough ActionPoints, nothing happens in the `do`, but `then` still executes.

**How to perform it**:

1. **Declare**: "I use Basic Attack on the adjacent enemy"
2. **Check condition**: Do I have 1+ ActionPoints?
3. **Resolve outcome**: If yes, roll 1d6 and subtract from target's Health
4. **Execute then**: Subtract 1 ActionPoint (happens whether condition was true or false)
5. **Update sheet**: Record new ActionPoints value

**Important**: The `then` component always executes. This happens regardless of whether the condition was true or false!

> **For complete details on actions**, including component references and advanced examples, see **Chapter 4: Taking Actions**.

### 5. Move Around

Your campaign defines movement through a **Feature**. Common examples:

```
Dexterous Movement (Feature)
Move up to [Dexterity] spaces per turn
```

```
Standard Movement (Feature)
All actors move up to 6 spaces per turn
```

```
AP Movement (Feature)
Spend 1 [ActionPoint] per space moved
```

**Turn structure** (also defined by Features):
- **Flexible**: Move and act in any order
- **Phased**: Movement happens in a specific phase

> For more on Features, see **Chapter 3: Features**.

### 6. End Your Turn

When you're done:
1. Resolve any "end of turn" effects
2. Announce your turn is complete
3. Next actor in initiative order goes

## Quick Example: A Complete Turn

**Setup**:
- Your actor (Raven) is at position 0N 0E, facing North
- Enemy (Goblin) is at position 1N 0E
- Your actionPoints: 3
- Your strength: 4

**Your Turn**:

1. **Check initiative**: You have initiative 15, Goblin has 12. You go first.

2. **Choose action**: You want to attack the Goblin with Basic Attack.

3. **Declare**: "I use Basic Attack on the Goblin"

4. **Check conditions**:
   - Adjacent to Goblin? Yes (1 space away)
   - actionPoints >= 1? Yes (I have 3)
   - ✓ Condition is TRUE

5. **Execute do** (condition was true):
   - Roll 1d6: result is 5
   - Add strength: 5 + 4 = 9
   - Goblin's health -= 9
   - Goblin had 12 health, now has 3

6. **Execute then** (always happens):
   - actionPoints -= 1
   - 3 - 1 = 2 actionPoints remaining

7. **Update sheet**:
   - actionPoints: 3 → 2

8. **Announce**: "Turn complete"

**Goblin's Turn**:
- Goblin performs its action based on behavior rules in the campaign book
- If it's a player-controlled actor, that player decides

## Turn Structure

For a complete turn checklist, see **Quick Reference** (Appendix).

## Victory and Completion

Your campaign defines victory conditions through **Features** or explicit rules:
- Defeat all enemies
- Reach a specific resource threshold
- Survive for X rounds
- Complete an objective

**Example Victory Feature**:
```
Survival Victory (Feature)
Game ends when all player actors are removed from the map
Actors with [Health] > 0 at game end are victorious
```

Check your campaign's victory condition before starting!

## What's Next?

You now know enough to start playing! For deeper understanding:

- **Chapter 2: Introduction** - Framework philosophy and design
- **Chapter 3: Core Concepts** - Detailed rules for actors, resources, dice, and maps
- **Chapter 4: Gameplay** - Reading campaigns, setup, actions, and turn structure
- **Chapter 5: Encounters** - Advanced tactical play
- **Chapter 6: Reference** - Glossary, quick reference, and character sheet

**Pro tip**: Keep the Quick Reference (Chapter 6) handy during your first few games!

---

**Ready to play?** Grab your campaign book and dive in!
