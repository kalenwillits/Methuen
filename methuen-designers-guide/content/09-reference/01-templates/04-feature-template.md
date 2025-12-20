# Feature Template

## Quick Template

```
Feature Name (Feature)
Clear description of the passive rule in plain language
[Trigger condition (if applicable)]: [Effect when triggered]
```

## When to Use Features

### Feature vs Effect vs Action Decision Guide

**Use a Feature when:**
- The rule is always active or automatically triggered
- No player decision is required to activate it
- It modifies existing game mechanics
- It describes "how things work" in your campaign

**Use an Effect when:**
- You need to make a specific, one-time change
- It's part of an action's if/do/then/else structure
- It describes "what happens"

**Use an Action when:**
- Players need to deliberately choose to do something
- It has costs, conditions, and effects
- It describes "what actors can do"

### Examples

| Game Rule | Correct Type | Why |
|-----------|--------------|-----|
| "Move up to 6 spaces per turn" | Feature | Always active, no decision |
| "[Target Health] -= 1d6" | Effect | Specific change, part of action |
| "Basic Attack" (if/do/then/else) | Action | Player chooses to attack |
| "Immune to fire damage" | Feature | Always active modification |
| "When Health < 5, movement costs double" | Feature | Automatic trigger |
| "Create wall at target location" | Effect | Specific change |

## Feature Naming Conventions

**Good Names** (Descriptive, clear purpose):
- Dexterous Movement (describes what it does)
- Injured (describes the state)
- Fire Immunity (describes the protection)
- Regeneration (describes the effect)

**Bad Names** (Vague, unclear):
- Special Ability (what ability?)
- Bonus (what bonus? when?)
- Trait #3 (meaningless)
- Super Power (too vague)

**Naming Guidelines**:
1. Use descriptive words that explain the Feature
2. Keep names concise (1-3 words typically)
3. Make it memorable and thematic
4. Use adjectives that describe the game effect

## Plain Language Guidelines

Features should be written in clear, everyday language that anyone can understand.

### Good Plain Language

```
Regeneration (Feature)
At start of this actor's turn, [Health] += 1d4
Cannot exceed maximum Health
```
- Clear trigger ("at start of turn")
- Specific effect ("[Health] += 1d4")
- Defined limitation ("cannot exceed maximum")

### Bad Plain Language

```
Healing Trait
Actor heals sometimes when conditions are met
```
- Vague trigger ("sometimes")
- Unclear effect ("heals" - how much?)
- Undefined conditions ("when conditions are met" - which conditions?)

### Writing Checklist

When writing a Feature, ensure:
- [ ] Trigger is specific ("When [Health] < 5", not "when hurt")
- [ ] Numbers are exact ("add +2", not "add a bonus")
- [ ] Timing is clear ("at start of turn", not "eventually")
- [ ] Scope is defined ("this actor", "all actors", "target")
- [ ] Limitations are stated ("cannot exceed max", "once per turn")
- [ ] Uses [bracket] notation for resources

## Common Pitfalls

### Pitfall 1: Ambiguous Conditions

**Bad**:
```
Strong Fighter (Feature)
When strong, add bonus to attacks
```
What does "strong" mean? How much bonus?

**Good**:
```
Mighty Striker (Feature)
When [Strength] >= 15, add +3 to all attack expressions
```

### Pitfall 2: Undefined Scope

**Bad**:
```
Defense Bonus (Feature)
Actors get more defense
```
Which actors? How much? When?

**Good**:
```
Shield Training (Feature)
This actor has +3 [Defense]
```

### Pitfall 3: Unclear Timing

**Bad**:
```
Healing (Feature)
Actor heals over time
```
When? How often? How much?

**Good**:
```
Natural Healing (Feature)
At start of this actor's turn, [Health] += 2
Cannot heal if actor moved last turn
```

### Pitfall 4: Missing Limitations

**Bad**:
```
Powerful Attack (Feature)
Add damage to all attacks
```
How much? Is there a limit?

**Good**:
```
Critical Strike (Feature)
Once per encounter, this actor may add +2d6 to one attack
Mark when used
```

### Pitfall 5: Using Action Structure

**Bad**:
```
Quick Movement (Feature)
if: [ActionPoints] >= 1
do: Move 3 spaces
then: [ActionPoints] -= 1
```
This is an Action, not a Feature!

**Good**:
```
Swift (Feature)
This actor may move 2 additional spaces per turn
```

## Complete Examples

### Campaign Feature Example

```
Initiative Roll (Feature)
All actors roll 1d20 + [Dexterity] at start of encounter
Highest result goes first each round
Re-roll ties
```

**Why this works**:
- Clearly campaign-wide ("all actors")
- Specific timing ("at start of encounter")
- Explicit rules ("re-roll ties")
- Uses resource notation ([Dexterity])

### Actor Feature Example

```
Wounded (Feature)
When this actor's [Health] drops below 5, movement costs double
Effect ends when [Health] increases above 5
```

**Why this works**:
- Clear trigger (specific Health threshold)
- Specific effect (movement costs ×2)
- Defined ending condition
- Scoped to actor ("this actor")

### Triggered Feature Example

```
Last Stand (Feature)
When this actor's [Health] drops to 1, add +5 to all attack expressions
Effect ends when [Health] changes from 1
```

**Why this works**:
- Precise trigger ([Health] = 1)
- Quantified benefit (+5)
- Clear scope (all attack expressions)
- Defined ending

## Feature Testing Checklist

After writing a Feature, verify:

- [ ] Name is descriptive and clear
- [ ] Labeled with **(Feature)**
- [ ] Written in plain language
- [ ] All triggers are specific and measurable
- [ ] All effects use exact numbers
- [ ] Resources use [bracket] notation
- [ ] Scope is clear (this actor, all actors, target, etc.)
- [ ] Timing is specified (when does it activate?)
- [ ] Limitations are stated (can it stack? once per turn?)
- [ ] Ending conditions defined (if triggered)
- [ ] No ambiguous terms ("sometimes", "bonus", "strong")
- [ ] Fits campaign balance and theme
- [ ] Players can understand it without designer explanation

---

## See Also

- **Chapter 14: Features** - Complete guide to designing Features
- **Chapter 15: Effects** - When to use Effects instead
- **Chapter 16: Actions** - When to use Actions instead
- **Quick Reference** - Feature patterns and examples
