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
