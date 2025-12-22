# Features

## What are Features?

**Features** are passive rules that describe how actors can interact or be interacted with.

## Feature Characteristics

- Always active or conditionally triggered
- Do not require actor decision to use
- Modify existing rules rather than create new actions
- Written in plain English with clear conditions

## Feature Types

### Campaign Features

Features that apply to the entire game or all actors.

**Initiative Features**:
```
Initiative Roll (Feature)
Roll 1d20 + [Dexterity] at start of encounter
Highest result goes first each round
```

```
Speed-Based Initiative (Feature)
Initiative equals [Speed]
Highest Speed acts first each round
Fixed for entire encounter
```

**Victory Condition Features**:
```
Elimination Victory (Feature)
Game ends when all actors of one side are removed from the map
Surviving side wins
```

```
Resource Victory (Feature)
Game ends when any player reaches [Gold] >= 100
That player wins immediately
```

**Environmental Features**:
```
Burning Tiles (Feature)
Actors ending their turn on "fire" tiles take 1d4 damage
Fire spreads to adjacent grass tiles each round
```

```
High Ground Advantage (Feature)
Actors on elevated tiles add +2 to all attack expressions
Against targets on lower elevation only
```

### Movement Features
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
Diagonal movement costs 2 [ActionPoints]
```

### Action Economy Features
```
Single Action Per Turn (Feature)
Each actor may perform exactly 1 action per turn
```

```
Action Point Economy (Feature)
Actors have [ActionPoints] resource
Most actions cost 1-3 [ActionPoints]
[ActionPoints] refresh at start of each turn
```

### Actor Features

Features for specific actors or actor types.

**Resistance Features**:
```
Fire Immunity (Feature)
This actor takes no damage from fire-based effects
```

```
Damage Reduction (Feature)
Subtract 3 from all incoming damage (minimum 0 damage)
```

**Triggered Features**:
```
Wounded (Feature)
When [Health] drops below 5, movement costs double
Effect ends when [Health] increases above 5
```

```
Last Stand (Feature)
When [Health] drops to 1, add +5 to all attack expressions
Effect ends when [Health] changes
```

**Modification Features**:
```
Precise (Feature)
Add +2 to all accuracy-based expressions
```

```
Swift (Feature)
This actor may move 2 additional spaces per turn
```

## Feature Composition

Features can reference or build upon other Features, game states, or map conditions.

**Referencing Game State**:
```
Tactical Advantage (Feature)
If this actor has higher ground (determined by map elevation), add +2 to all attack expressions
```

**Conditional Stacking**:
```
Desperate Fighter (Feature)
When [Health] < 10, add +1 to all attack expressions
When [Health] < 5, add an additional +2 (total +3)
```

**Multi-Condition Features**:
```
Flanking Bonus (Feature)
When this actor and an ally are adjacent to the same target
And on opposite sides of that target
Both actors add +3 to attack expressions against that target
```

**Feature Interactions**:
```
Cover System (Feature)
Actors adjacent to wall tiles gain +3 [Defense]

Mobility Training (Feature)
This actor ignores Cover System benefits from enemies
But still receives Cover System benefits themselves
```

## Common Feature Patterns

### Conditional Features ("When X, then Y")

**Pattern**: Check a condition, apply an effect
```
Low Health Trigger (Feature)
When [Health] < threshold, apply modification
```

**Examples**:
- Wounded (movement penalty when hurt)
- Berserker Rage (damage bonus when low health)
- Desperation (free action when near death)

**Design Use**: Create dynamic gameplay that changes based on game state

### Modification Features ("Add/subtract Z to expression")

**Pattern**: Flat or percentage modifier to calculations
```
Stat Modifier (Feature)
Add/subtract value to specific expressions
```

**Examples**:
- Precise (+2 to accuracy)
- Tough (-2 to incoming damage)
- Swift (+2 movement spaces)

**Design Use**: Differentiate actors with passive bonuses

### Restriction Features ("Cannot do X")

**Pattern**: Prevent specific actions or behaviors
```
Limitation (Feature)
This actor cannot perform specific action or enter specific state
```

**Examples**:
- Water Restriction (cannot enter water tiles)
- Heavy Armor (cannot use ranged actions)
- Pacifist (cannot deal damage)

**Design Use**: Create balanced trade-offs for powerful abilities

### Triggered Features ("When condition, effect")

**Pattern**: Event triggers automatic effect
```
Event-Based (Feature)
When specific event occurs, apply one-time or ongoing effect
```

**Examples**:
- On Damage (trigger when hit)
- On Death (trigger when eliminated)
- Start of Turn (trigger each turn)

**Design Use**: Add interactivity without requiring player choices

### Scaling Features ("Effect scales with X")

**Pattern**: Effect magnitude depends on resource or condition
```
Scaling Effect (Feature)
Effect strength based on resource value or condition count
```

**Examples**:
- Dexterous Movement (movement scales with Dexterity)
- Strength Damage (damage scales with Strength)
- Gold Advantage (benefits scale with Gold accumulated)

**Design Use**: Reward resource investment, create build variety

## Modeling Equipment as Features

In Methuen, equipment is typically modeled as **Features** rather than inventory items. This approach creates cleaner gameplay with less bookkeeping.

### Equipment as Features: The Pattern

Instead of tracking items in inventory slots, equipment becomes Features that actors possess.

**Traditional Item System** (not recommended):
```
Warrior (Actor)
Resources: Health 30, ActionPoints 3
Inventory:
  - Iron Sword (item)
  - Wooden Shield (item)
  - Leather Armor (item)

Attack (Action)
if: Adjacent to target AND has weapon equipped
do: [Target Health] -= (1d6 + weapon damage bonus)
then: [ActionPoints] -= 1
```

**Methuen Feature System** (recommended):
```
Warrior (Actor)
Resources: Health 30, ActionPoints 3
Features:
  - Iron Blade Training: +2 to melee damage
  - Shield Bearer: +2 Defense
  - Light Armor: +1 Defense

Attack (Action)
if: Adjacent to target
do: [Target Health] -= (1d6 + 2)
then: [ActionPoints] -= 1
```

**Why Features work better:**
- No inventory management needed
- Equipment bonuses baked into calculations
- Clear presentation (features list = current equipment)
- Easy to swap (remove old feature, add new feature)

### Equipment Feature Categories

**Weapon Features**
```
Iron Blade Training (Feature)
+2 to melee damage

Bow Training (Feature)
+2 to ranged damage
Requires: Arrows resource

Ancient Nord Blade (Feature)
+3 to melee damage
Additional: Apply 1d4 frost damage on melee hits
```

**Armor Features**
```
Heavy Armor (Feature)
+1 Defense
-1 Movement (penalty for bulk)

Light Armor (Feature)
+1 Defense

Shield Bearer (Feature)
+2 Defense
```

**Accessory Features**
```
Enchanted Ring of Magicka (Feature)
Magicka Maximum +10

Necromancer Robes (Feature)
Magicka regeneration +3 per turn

Amulet of Kings (Feature)
+3 to all base resources (Strength, Agility, Endurance, Intellect, Willpower)
```

### Equipment Progression Pattern

Use loot as Feature replacement rather than inventory accumulation:

**Encounter 1 Loot:**
```
Ancient Nord Blade (Feature) - found in chest
Replaces: Iron Blade Training
Upgrade: +2 damage → +3 damage + 1d4 frost
```

**Encounter 2 Loot:**
```
Ebony Greatsword (Feature) - boss drop
Replaces: Ancient Nord Blade
Upgrade: +3 damage + 1d4 frost → +4 damage
```

**How it works:**
- Player has "Iron Blade Training" feature at campaign start
- Finds Ancient Nord Blade, removes old feature, adds new one
- Finds Ebony Greatsword, removes Ancient Nord Blade, adds new one
- Character sheet always shows current equipment as active features

**Benefits:**
- No inventory limits to track
- Clear progression path
- Always know what bonuses are active
- Easy to reference during play

### Consumables: The Exception

Some equipment should use Resources instead of Features:

**Use Resources for:**
- Items with limited uses (potions, scrolls)
- Items that deplete (arrows, lockpicks)
- Items that are counted (gold, materials)

**Use Features for:**
- Permanent equipment (weapons, armor)
- Items that provide passive bonuses
- Items that don't run out

**Example - Arrows:**
```
Archer (Actor)
Resources: Health 25, ActionPoints 3, Arrows 30
Features: Bow Training (+2 ranged damage)

Ranged Shot (Action)
if: [Arrows] >= 1 AND target within 15 spaces
do: [Target Health] -= (1d6 + 2), [Arrows] -= 1
then: [ActionPoints] -= 1
```

**Example - Health Potions:**
```
Adventurer (Actor)
Resources: Health 20, ActionPoints 3, HealthPotions 2

Use Potion (Action)
if: [HealthPotions] >= 1
do: [Health] += 2d8, [HealthPotions] -= 1
then: [ActionPoints] -= 1
```

### Equipment Upgrade Example: Complete Flow

**Starting Equipment (Character Creation):**
```
Warrior (Actor)
Features:
  - Iron Blade Training: +2 melee damage
  - Heavy Armor: +1 Defense, -1 Movement
  - Shield Bearer: +2 Defense
```

**After Encounter 2 (looted Ancient Nord Blade):**
```
Warrior (Actor)
Features:
  - Ancient Nord Blade: +3 melee damage, +1d4 frost damage
  - Heavy Armor: +1 Defense, -1 Movement
  - Shield Bearer: +2 Defense
```
(Removed "Iron Blade Training", added "Ancient Nord Blade")

**After Encounter 3 (looted Ancient Heavy Armor):**
```
Warrior (Actor)
Features:
  - Ancient Nord Blade: +3 melee damage, +1d4 frost damage
  - Ancient Heavy Armor: +5 Defense, -1 Movement
  - Shield Bearer: +2 Defense
```
(Removed "Heavy Armor", added "Ancient Heavy Armor")

**Final Boss Drops (chose Daedric Mace over Enchanted Ebony Armor):**
```
Warrior (Actor)
Features:
  - Daedric Mace: +5 melee damage
  - Ancient Heavy Armor: +5 Defense, -1 Movement
  - Shield Bearer: +2 Defense
```
(Removed "Ancient Nord Blade", added "Daedric Mace")

### Equipment Trading and Choice

Some campaigns allow players to choose loot or trade equipment:

**Multiple Equipment Found:**
```
Treasure Chest contains:
- Ebony Greatsword (Feature): +4 melee damage
- Enchanted Ebony Armor (Feature): +6 Defense

Choose one (cannot carry both)
```

**Trading Between Players:**
```
Warrior gives Shield Bearer (Feature) to Archer
Archer now has: Bow Training, Light Armor, Shield Bearer
Warrior now has: Iron Blade Training, Heavy Armor
```

This works because features can be freely added/removed - they're not physical objects with persistence.

### Design Checklist for Equipment Features

When modeling equipment, ask:

- [ ] Does this equipment provide a passive bonus? → Use Feature
- [ ] Does this equipment run out or have limited uses? → Use Resource
- [ ] Can this equipment be upgraded/replaced? → Design as replaceable Feature
- [ ] Does having this equipment change available actions? → Reference feature in action conditions
- [ ] Do all variants stack or replace each other? → Document stacking rules in campaign

**Stacking Example:**
```
Multiple armor pieces can stack:
- Light Armor: +1 Defense (torso)
- Shield Bearer: +2 Defense (hand)
- Helmet: +1 Defense (head)
Total: +4 Defense

Weapons replace each other (can only use one):
- Iron Blade Training: +2 damage
- Ebony Greatsword: +4 damage
Cannot have both - replacing weapon removes old feature
```

## Writing Features

**Template**:
```
Feature Name (Feature)
Clear description of the passive rule
Trigger condition (if applicable): Effect when triggered
```

**Formatting Rules**:
1. Always label with **(Feature)**
2. Use plain language
3. Reference resources with [brackets]
4. Specify exact numbers
5. State conditions precisely

**Be Specific**:
- Define exact numbers, not ranges
- State conditions precisely
- Clarify when feature applies
- Define what happens when conditions end

**Good Examples**:
```
Regeneration (Feature)
At start of this actor's turn, [Health] += 1d4
Cannot exceed maximum Health
```

**Bad Example**:
```
Fast Healing
Sometimes heal a bit
```
(Vague: When? How much? Under what conditions?)

---

## See Also
- Chapter 15: Effects
- Chapter 16: Actions
- Reference: Feature Template
