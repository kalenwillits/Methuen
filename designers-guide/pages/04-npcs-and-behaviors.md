# NPCs and Behaviors

NPCs are autonomous actors controlled by predefined behaviors and strategies.

## NPC Structure

**Behavior**
One conditional action rule: "Attack if adjacent to enemy"

**Strategy**
Collection of behaviors in priority order. NPCs execute the first behavior whose checks pass.

## Behavior Structure

```
Behavior: [Name]
Checks: [Conditions]
Action: [What to do if checks pass]
```

**Example**:
```
Behavior: Attack Nearest
Checks:
  - Enemy within 5 spaces?
  - ActionPoints >= 1?
Action: Move toward nearest enemy, attack if adjacent
```

## Check Types

**Resource checks**:
- `[ActionPoints] >= 1`
- `[Health] < 10`

**Position checks**:
- `Adjacent to enemy`
- `Enemy within X spaces`

**State checks**:
- `Target has Health > 0`
- `Path is clear`

## Writing Behaviors

**1. Define the condition**
What must be true for this behavior to execute?

**2. Specify the action**
What does the NPC do when condition is met?

**3. Consider priority**
Where does this fit in the strategy?

## Simple Behavior Examples

### Aggressive Melee

```
Behavior 1: Attack if Adjacent
Checks: Adjacent to enemy AND [ActionPoints] >= 1
Action: Use Basic Attack

Behavior 2: Approach Enemy
Checks: Enemy within 10 spaces AND [MovementPoints] >= 1
Action: Move toward nearest enemy

Behavior 3: Wait
Checks: None (always true)
Action: Do nothing
```

### Defensive Ranged

```
Behavior 1: Retreat if Threatened
Checks: Enemy adjacent AND [MovementPoints] >= 2
Action: Move away 2 spaces

Behavior 2: Ranged Attack
Checks: Enemy within 10 spaces AND [Arrows] >= 1
Action: Use Ranged Shot

Behavior 3: Melee if Cornered
Checks: Adjacent to enemy AND [ActionPoints] >= 1
Action: Use Basic Attack
```

### Healer Support

```
Behavior 1: Heal Ally
Checks: Ally has [Health] < 10 AND [Mana] >= 5
Action: Cast Heal on lowest Health ally

Behavior 2: Defend Self
Checks: [Health] < 5 AND [ActionPoints] >= 1
Action: Use Defend action

Behavior 3: Ranged Support
Checks: Enemy within 8 spaces AND [ActionPoints] >= 1
Action: Use Ranged Attack
```

## Strategies

A **Strategy** combines multiple behaviors in priority order.

```
Goblin Strategy
Priority 1: Flee if [Health] < 3
Priority 2: Attack if adjacent to player
Priority 3: Move toward nearest player
```

NPCs evaluate behaviors from highest to lowest priority. First behavior whose checks pass is executed.

## NPC Design Guidelines

### Keep It Simple

NPCs don't need complex decision trees. 3-4 behaviors cover most tactical patterns.

### Predictable but Not Trivial

Players should understand NPC behavior without it being exploitable.

Good: "Goblin always attacks if adjacent, otherwise moves closer"
Bad: "Goblin randomly chooses action each turn"

### Observable Triggers

Behavior triggers should be visible to players.

Good: "Flees when Health < 5" (players can see Health)
Bad: "Flees when scared" (players can't see internal state)

## Behavior Antipatterns

### Antipattern: Analysis Paralysis

```
Behavior 1: If [Condition1] AND [Condition2] AND [Condition3] AND [Condition4]...
```

Problem: Too many checks make behavior hard to understand and execute.

Fix: Simplify to 1-3 key checks per behavior.

### Antipattern: Impossible Conditions

```
Behavior: Attack if adjacent
Checks: Enemy within 10 spaces BUT NOT adjacent
Action: Use melee attack
```

Problem: Condition prevents action from ever succeeding.

Fix: Align checks with action requirements.

### Antipattern: No Fallback

```
Strategy:
  Behavior 1: Attack if [Health] > 50
  Behavior 2: Defend if [Health] < 20
```

Problem: NPC does nothing when Health is 21-49.

Fix: Always include catch-all final behavior.

## NPC Action Design

NPCs can use the same actions as players, or have unique actions.

### Unique NPC Actions

```
Boss Summon
if: [Phase] = 2 AND [Minions] = 0
do: Summon 3 Minions at positions X, Y, Z
then: [Phase] += 1
```

### Simplified NPC Actions

```
Goblin Stab
if: Adjacent to target
do: [Target Health] -= 1d6 + 3
then: [ActionPoints] -= 1
```

Note: Strength 3 baked into damage.

## Multi-Phase Bosses

Create dynamic encounters by changing behavior based on Health:

```
Dragon Strategy
Phase 1 ([Health] > 50): Aggressive melee
Phase 2 ([Health] 25-50): Mixed ranged and melee
Phase 3 ([Health] < 25): Defensive with powerful abilities
```

Each phase can have different behaviors.

## NPC Complexity Tiers

**Tier 1: Mindless**
Single behavior, no decision-making.
Example: "Always move toward nearest enemy and attack if adjacent"

**Tier 2: Basic Tactics**
2-3 behaviors with simple checks.
Example: "Attack if adjacent, otherwise move closer"

**Tier 3: Adaptive**
4-5 behaviors responding to game state.
Example: "Flee if low health, attack if adjacent, support allies if they're injured"

**Tier 4: Boss Mechanics**
Multi-phase with special abilities.
Example: "Different strategy each phase, summons minions, area attacks"

Match NPC complexity to:
- Player count (more players = simpler NPCs)
- Encounter length (longer = simpler NPCs)
- Campaign difficulty (experienced players = more complex)

## Testing NPC Behaviors

Playtest by observing:

**Decision Clarity**
Can players predict what NPC will do?

**Tactical Depth**
Do NPCs create interesting challenges?

**Balance**
Are NPCs too strong or too weak?

**Execution Speed**
Can NPCs' turns resolve quickly?

Red flags:
- NPC behavior is random or unclear
- NPC always wins or always loses
- NPC turns take too long to resolve
- Players can trivially exploit behavior
