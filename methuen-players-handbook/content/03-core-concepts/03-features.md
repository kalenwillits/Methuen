# Features

## What are Features?

**Features** are campaign-level rules written in plain language. They describe how things work in your specific campaign, from how actors move to special abilities your character might have.

Features can be attached to:
- **The campaign itself**: Rules that apply to everyone (initiative, movement, victory conditions)
- **Actors**: Special abilities or limitations for specific characters
- **Actions**: Conditional effects or modifications
- **Effects**: How certain game mechanics work

**Key characteristic**: Features are written in clear, everyday language. If a rule is stated plainly and describes how something works, it's likely a Feature.

## Reading Features in Campaign Books

When you read a campaign book, Features are labeled with **(Feature)** and include:

**Name**: What the Feature is called
**Rule**: How it works, written in plain language
**Trigger** (optional): When it activates or under what conditions

**Example**:
```
Injured (Feature)
When this actor's [Health] < 5, movement distance is reduced by 3 spaces
```

## Common Feature Categories

### Campaign Features

These apply to all actors or the entire game.

**Initiative Feature**:
```
Initiative Roll (Feature)
All actors roll 1d20 + [Dexterity] at encounter start
Highest result acts first each round
```

**Victory Feature**:
```
Elimination Victory (Feature)
Game ends when all actors of one side are removed from the map
Surviving side wins
```

### Movement Features

Define how actors move on the map.

**Dexterous Movement**:
```
Dexterous Movement (Feature)
Move up to [Dexterity] spaces per turn
```

**Standard Movement**:
```
Standard Movement (Feature)
All actors move up to 6 spaces per turn
```

**AP Movement**:
```
AP Movement (Feature)
Spend 1 [ActionPoint] per space moved
Diagonal movement costs 2 [ActionPoints]
```

### Action Economy Features

Define how many actions actors can take.

**Single Action**:
```
Single Action Per Turn (Feature)
Each actor may perform exactly 1 action per turn
```

**Action Point Economy**:
```
Action Point Economy (Feature)
Actors have [ActionPoints] resource
Most actions cost 1-3 [ActionPoints]
[ActionPoints] refresh at start of each turn
```

### Actor Features

Special rules for specific actors or types.

**Injured**:
```
Injured (Feature)
When this actor's [Health] < 5, movement distance is reduced by 3 spaces
```

**Fire Immunity**:
```
Fire Immunity (Feature)
This actor takes no damage from fire-based effects
```

**Swift**:
```
Swift (Feature)
This actor may move 2 additional spaces per turn
```

**Regeneration**:
```
Regeneration (Feature)
At the start of this actor's turn, [Health] += 1d4
Cannot exceed maximum Health
```

### Triggered Features

Features that activate when specific conditions are met.

**Wounded**:
```
Wounded (Feature)
When [Health] drops below 5, movement costs double until healed
```

**Defensive Stance**:
```
Defensive Stance (Feature)
When this actor does not move during their turn, [Defense] += 3 until next turn
```

**Last Stand**:
```
Last Stand (Feature)
When [Health] drops to 1, add +5 to all attack expressions
Effect ends when [Health] changes
```

### Modification Features

Features that modify expressions or effects.

**Precise**:
```
Precise (Feature)
Add +2 to all accuracy-based expressions
```

**Tough**:
```
Tough (Feature)
Subtract 2 from all incoming damage (minimum 0 damage)
```

**Lucky**:
```
Lucky (Feature)
Once per encounter, may re-roll any single die
Must use the second result
```

## Features vs Effects vs Actions

Understanding the difference helps you read campaign books correctly.

### Features (Passive, Ongoing)

Rules that are always active or trigger automatically:
- "Move up to 6 spaces per turn"
- "Immune to fire damage"
- "Cannot enter water tiles"
- "When [Health] < 5, movement costs double"

### Effects (Active, Specific)

Immediate changes that happen when triggered:
- "[Target Health] -= 1d6"
- "Move target 3 spaces North"
- "[Gold] += 5"
- "Target becomes poisoned"

### Actions (Player-Initiated)

Things actors can deliberately choose to do:
- "Basic Attack" (has if/do/then/else structure)
- "Cast Spell" (costs resources, has effects)
- "Move" (uses movement Feature rules)

**Think of it this way**:
- **Features** = "How things work"
- **Effects** = "What happens"
- **Actions** = "What you can do"

## How Features Interact with Actions

Features often modify how actions work.

**Example: Movement Action + Movement Feature**

If your campaign has:
```
Dexterous Movement (Feature)
Move up to [Dexterity] spaces per turn
```

And you have Dexterity = 4, then when you use a Move action, you can move up to 4 spaces.

**Example: Attack Action + Modification Feature**

If you have:
```
Precise (Feature)
Add +2 to all accuracy-based expressions
```

Then an action like:
```
Aimed Shot (Action)
if: 1d20 + [Accuracy] > [Target Defense]
do: [Target Health] -= 2d6
then: [ActionPoints] -= 2
```

Becomes `1d20 + [Accuracy] + 2` due to your Precise Feature.

## Features and Your Actor

When creating your actor, you'll note:

1. **Campaign Features** that affect everyone (initiative, movement, action economy)
2. **Actor Features** specific to your character (special abilities, limitations)
3. **Conditional Features** that might trigger during play

**On your character sheet**:
```
Actor: Agile Scout

Features:
- Dexterous Movement (Campaign): Move up to [Dexterity] per turn
- Swift (Actor): +2 additional movement spaces
- Wounded (Triggered): Movement costs double when [Health] < 5
```

## Where to Find Features

**In Campaign Books**:
- **Setup section**: Campaign-wide Features (initiative, movement, victory)
- **Actor section**: Special Features for specific actor types
- **Action descriptions**: Features that modify specific actions
- **Glossary**: Quick reference for all Features

**During Play**:
- Reference your character sheet for your actor's Features
- Check campaign rules for universal Features
- Ask gamemaster or check campaign book when unsure

## Examples from Different Campaign Types

### Tactical Combat Campaign
```
Initiative Roll (Feature)
Roll 1d20 + [Dexterity] at encounter start

Single Action Economy (Feature)
Each actor performs 1 action per turn

Cover System (Feature)
Actors adjacent to wall tiles gain +3 [Defense]
```

### Resource Management Campaign
```
Standard Initiative (Feature)
Turn order: Player 1, Player 2, Environment

Harvest System (Feature)
Adjacent resource tiles can be harvested for materials

Building Feature (Feature)
Structures provide passive benefits each turn
```

### Exploration Campaign
```
Speed-Based Initiative (Feature)
Initiative equals [Speed], highest acts first

Discovery Feature (Feature)
Revealing unexplored tiles grants +1 [XP]

Fatigue Feature (Feature)
After 10 turns without rest, [ActionPoints] maximum decreases by 1
```

## Common Questions

**Q: Can Features be changed during play?**
A: Some Features are triggered or conditional. Permanent Features (like "Fire Immunity") don't change, but triggered Features (like "Wounded") activate based on conditions.

**Q: What if a Feature contradicts an action?**
A: Features modify how actions work. If a Feature says "Cannot use ranged actions" and you try a ranged action, the Feature prevents it.

**Q: Can I gain new Features during play?**
A: Your campaign defines whether Features can be gained. Some campaigns allow earning Features through advancement, others keep Features fixed.

**Q: How do I know if something is a Feature?**
A: If it describes an ongoing rule in plain language (not an if/do/then/else action structure), it's likely a Feature.

---

## See Also

- **Chapter 1: Quick Start** - Features in play examples
- **Chapter 2: Actors and Resources** - How Features affect actors
- **Chapter 4: Taking Actions** - How Features interact with actions
- **Designer's Guide: Chapter 14** - Creating Features for your own campaigns
