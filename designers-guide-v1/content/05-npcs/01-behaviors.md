# NPC Behaviors

## What are Behaviors?

A **Behavior** is a single conditional action rule that defines what an NPC does when specific conditions are met.

**Terminology Clarification**:
- **Behavior**: One conditional action rule (e.g., "Attack if adjacent to enemy")
- **Strategy**: A collection of multiple Behaviors in priority order (see **Chapter: Strategies**)
- **Relationship**: Behaviors are the building blocks that compose Strategies

Behaviors are not used alone - they are always part of a larger Strategy. Think of Behaviors as individual rules, and Strategies as the complete rulebook for an NPC.

## Behavior Structure

```
Behavior: [Name]
Checks: [Conditions to evaluate]
Action: [What to do if checks pass]
```

**Example**:
```
Behavior: Attack Nearest
Checks: 
  - Is there an actor within 5 spaces?
  - Do I have actionPoints >= 1?
Action: Move toward nearest actor, then attack if adjacent
```

## Check Types

- **Resource checks**: Does actor have enough resources?
- **Position checks**: Is target in range?
- **State checks**: Is target valid?
- **Priority checks**: Is this the best option?

## NPC Resource Design

A common mistake is giving NPCs the same resources as player characters. NPCs only need resources that:
1. Drive behavioral decisions
2. Affect action availability
3. Create observable game state

**Principle**: Keep NPC resources minimal and purpose-driven.

### Resources NPCs Typically NEED

**Health**:
- Required: Determines when NPC is defeated
- Drives behaviors: "Flee when Health < X"
- Observable: Players can gauge enemy status

**Action Points** (if using action economy):
- Required: Gates which actions are available
- Drives behaviors: "Attack if ActionPoints >= 1"
- Affects turn-taking: Determines what NPC can do

**Position-Related Resources** (situational):
- Movement points (if using movement economy)
- Range or reach (if variable)
- Only if these create meaningful behavioral choices

### Resources NPCs Typically DON'T NEED

**Attribute Scores** (Strength, Dexterity, Intelligence, etc.):
- ❌ Don't create: Individual attribute scores for every NPC
- ✓ Do create: Attributes only when they vary between NPCs of same type OR drive behavior
- **Why**: If all Goblins have Strength 4, just bake it into their actions directly
- **Exception**: If Goblin Warrior has Strength 6 and Goblin Scout has Strength 2, and this affects damage, then use attributes

**Detailed Inventory**:
- ❌ Don't track: Every item, piece of equipment, consumable
- ✓ Do track: "Arrows remaining" if NPC runs out mid-combat
- **Why**: NPCs rarely make inventory decisions
- **Exception**: If behavior changes based on inventory ("Use potion if Health < 5")

**Experience/Leveling Resources**:
- ❌ Don't create: XP, levels, skill points for NPCs
- **Why**: NPCs don't persist or grow between encounters (usually)
- **Exception**: Campaign npcs that appear in multiple encounters

**Passive Resources**:
- ❌ Don't track: Resources that never change (static values)
- ✓ Do bake: Static bonuses directly into action definitions
- **Why**: Resources should represent *changeable* game state

### Design Pattern: Bake Constants into Actions

Instead of giving every Bandit the same Strength resource, incorporate it directly:

**❌ AVOID:**
```
Bandit (Actor)
Resources: Health 25, ActionPoints 2, Strength 4, Agility 3

Sword Slash (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + [Strength])
then: [ActionPoints] -= 1
```

**✓ PREFER:**
```
Bandit (Actor)
Resources: Health 25, ActionPoints 2

Sword Slash (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 4)
then: [ActionPoints] -= 1
```

**Why this is better:**
- 12 fewer characters to track if you have 12 bandits
- No confusion about which Strength value to use
- Clearer that all Bandits are identical
- Less bookkeeping during play

**When to use attributes:** When variance matters. If you have Bandit (Strength 4), Bandit Leader (Strength 6), and Bandit Recruit (Strength 2), then attributes make sense.

### NPC Resource Checklist

When designing an NPC, ask for each resource:

- [ ] Does this resource change during combat?
- [ ] Do behaviors check this resource?
- [ ] Does this resource vary between NPCs of this type?
- [ ] Would players notice if this resource didn't exist?

If you answer "No" to all four, don't include the resource. Bake its value into actions instead.

### Example: Simplified Draugr

**Overcomplicated Version** (11 resources):
```
Draugr (Actor)
Resources:
  Health: 45
  ActionPoints: 2
  Strength: 5
  Endurance: 4
  Agility: 2
  Willpower: 6
  Defense: 3
  Movement: 4
  Experience: 0
  Level: 5
  MagicResist: 25
```

**Streamlined Version** (3 resources):
```
Draugr (Actor)
Resources:
  Health: 45
  ActionPoints: 2
  Defense: 3

Features:
  - Frost Resistance: 50% (reduces frost damage)
  - Slow: Movement 4 (baked constant)
  - Undead: Immune to poison and fear

Frost Axe (Action)
if: Adjacent to target
do: [Target Health] -= (1d8 + 5), apply Frost 1
then: [ActionPoints] -= 1
```

**What changed:**
- Strength (5) baked into Frost Axe damage: `1d8 + 5`
- Movement (4) moved to Feature as constant
- Endurance, Agility, Willpower removed (no behavioral impact)
- MagicResist simplified to Feature (Frost Resistance)
- Level and Experience removed (not relevant for NPC)
- Defense kept (varies with equipment, players target it)

**Result:** From 11 resources to 3 resources. Draugr is easier to run, behaviors are clearer, and gameplay is unchanged.

## Writing Behaviors

1. Define the condition(s)
2. Specify the action to take
3. Include fallback if checks fail

---

## See Also
- Chapter 22: Strategies
- Chapter 16: Actions Design
