# NPC Strategies

## What are Strategies?

A **Strategy** is the complete decision-making system for an NPC actor, composed of multiple **Behaviors** evaluated in priority order.

**Terminology Clarification**:
- **Strategy**: The full AI logic for an NPC (e.g., "Goblin Tactics", "Guardian Patrol")
- **Behavior**: A single conditional action rule within a strategy (e.g., "Flee if health < 3")
- **Relationship**: One Strategy contains multiple Behaviors

**Conceptual Hierarchy**:
```
Strategy: Goblin Tactics
├─ Behavior 1: Flee if health < 3
├─ Behavior 2: Attack if adjacent to enemy
├─ Behavior 3: Move toward nearest enemy
└─ Behavior 4: Move randomly (fallback)
```

When an NPC takes its turn, it evaluates its Strategy's Behaviors from highest to lowest priority, executing the first one whose conditions are met.

## Strategy Structure

A Strategy lists its component Behaviors in priority order (highest first):

```
Strategy: [Strategy Name]

Behavior 1: [Highest Priority Behavior Name]
Checks: [Conditions that must be met]
Action: [What to do if checks pass]

Behavior 2: [Medium Priority Behavior Name]
Checks: [Conditions that must be met]
Action: [What to do if checks pass]

Behavior 3: [Fallback Behavior Name]
Checks: [Usually minimal or none]
Action: [Default action]
```

**Complete Example**:
```
Strategy: Goblin Tactics

Behavior 1: Flee When Wounded
Checks: [Health] < 3
Action: Move away from nearest enemy at maximum speed

Behavior 2: Melee Attack
Checks: Adjacent to enemy AND [ActionPoints] >= 1
Action: Use #Melee Strike action on adjacent enemy

Behavior 3: Close Distance
Checks: Enemy within 10 spaces
Action: Move toward nearest enemy

Behavior 4: Wander
Checks: (none - always succeeds)
Action: Move in random direction
```

## Evaluation Order

Behaviors are evaluated in order until one succeeds:
1. Check first behavior conditions
2. If all checks pass, perform action
3. If checks fail, move to next behavior
4. Repeat until a behavior executes

## Balancing NPC Intelligence

**Simple Strategies**: 1-3 behaviors, straightforward logic
**Complex Strategies**: 5+ behaviors, tactical depth

## Common NPC Strategy Patterns

Here are reusable strategy templates for typical NPC archetypes. Customize behavior details for your campaign.

### 1. Basic Melee Aggressor

**Use For**: Bandits, warriors, melee fighters
**Complexity**: Simple (3 behaviors)

```
Strategy: Aggressive Melee

Behavior 1: Melee Attack
Checks: Adjacent to enemy AND [ActionPoints] >= 1
Action: Use melee attack action

Behavior 2: Close Distance
Checks: Enemy within 10 spaces
Action: Move toward nearest enemy

Behavior 3: Wander
Checks: (none)
Action: Move in random direction
```

**Design Notes**: Straightforward AI that rushes enemies and attacks. No self-preservation. Good for low-level cannon fodder.

### 2. Ranged Skirmisher

**Use For**: Archers, gunners, ranged attackers
**Complexity**: Medium (4 behaviors)

```
Strategy: Ranged Skirmisher

Behavior 1: Maintain Distance
Checks: Enemy within 3 spaces
Action: Move away from nearest enemy (maintain 8-12 space range)

Behavior 2: Ranged Attack
Checks: Enemy within 15 spaces AND [Arrows] >= 1 AND [ActionPoints] >= 1
Action: Use ranged attack action

Behavior 3: Approach Range
Checks: Enemy beyond 15 spaces
Action: Move toward enemy (stop at ~10 spaces)

Behavior 4: Defend Position
Checks: (none)
Action: Skip turn or move to cover
```

**Design Notes**: Maintains optimal range. Kites melee attackers. Stops when out of ammo.

### 3. Defensive Guardian

**Use For**: Guards, protectors, defensive NPCs
**Complexity**: Medium (4 behaviors)

```
Strategy: Guardian Defense

Behavior 1: Protect Zone
Checks: Enemy within protected zone (5 space radius of point)
Action: Attack nearest enemy in zone

Behavior 2: Return to Post
Checks: Self is >3 spaces from protected point
Action: Move toward protected point

Behavior 3: Defend
Checks: Enemy adjacent
Action: Use defensive action or counterattack

Behavior 4: Hold Position
Checks: (none)
Action: Skip turn (wait for threats)
```

**Design Notes**: Guards an area rather than pursuing. Won't chase beyond zone. Good for stationary encounters.

### 4. Glass Cannon (High Damage, Low Health)

**Use For**: Mages, snipers, fragile high-damage units
**Complexity**: Medium (4 behaviors)

```
Strategy: Glass Cannon

Behavior 1: Flee When Wounded
Checks: [Health] < 10
Action: Move away from all enemies at maximum speed

Behavior 2: High-Power Attack
Checks: Enemy within range AND [Magicka] >= 5 AND [ActionPoints] >= 2
Action: Use powerful spell/attack

Behavior 3: Basic Attack
Checks: Enemy within range AND [ActionPoints] >= 1
Action: Use standard attack

Behavior 4: Retreat to Safe Range
Checks: (none)
Action: Move to maintain 10+ space distance from enemies
```

**Design Notes**: Self-preservation prioritized. Uses resources for big hits. Runs when hurt.

### 5. Support/Healer

**Use For**: Clerics, medics, buff/debuff NPCs
**Complexity**: Complex (5 behaviors)

```
Strategy: Support Specialist

Behavior 1: Emergency Heal
Checks: Ally exists with [Health] < 5 AND [Magicka] >= 3
Action: Move adjacent to wounded ally, use heal

Behavior 2: Buff Strongest Ally
Checks: Ally within range AND [Magicka] >= 2
Action: Cast buff on highest-damage ally

Behavior 3: Debuff Enemy
Checks: Strongest enemy within range AND [Magicka] >= 2
Action: Cast debuff on highest-threat enemy

Behavior 4: Maintain Safe Distance
Checks: Enemy within 5 spaces
Action: Move away while staying near allies

Behavior 5: Conserve Resources
Checks: (none)
Action: Move to safe position, skip offensive actions
```

**Design Notes**: Prioritizes healing critical allies. Buffs/debuffs when safe. Avoids combat. Requires ally-tracking logic.

### 6. Berserker (Escalating Aggression)

**Use For**: Raging barbarians, wounded beasts, desperate foes
**Complexity**: Medium (4 behaviors)

```
Strategy: Berserker Rage

Behavior 1: Enraged Assault
Checks: [Health] < ([HealthMaximum] / 2) AND Adjacent to enemy
Action: Use powerful attack with bonus damage

Behavior 2: Reckless Charge
Checks: [Health] < ([HealthMaximum] / 2)
Action: Move toward nearest enemy at maximum speed, ignoring opportunity attacks

Behavior 3: Standard Attack
Checks: Adjacent to enemy
Action: Use normal melee attack

Behavior 4: Advance
Checks: (none)
Action: Move toward nearest enemy
```

**Design Notes**: Gets more dangerous when wounded. Uses health threshold to trigger different behaviors. No retreat.

### 7. Adaptive Tactical (Boss/Elite)

**Use For**: Boss encounters, elite enemies, intelligent foes
**Complexity**: Complex (6+ behaviors)

```
Strategy: Tactical Superiority

Behavior 1: Phase Transition
Checks: [Health] < specific threshold AND [PhaseChanged] = 0
Action: Trigger special ability, set [PhaseChanged] = 1

Behavior 2: Use Special Ability
Checks: [SpecialAbilityCooldown] = 0 AND [ActionPoints] >= 3
Action: Use signature move, set cooldown

Behavior 3: Exploit Weakness
Checks: Enemy has [Defense] < 3 AND within range
Action: Focus fire on weakest enemy

Behavior 4: Area Control
Checks: Multiple enemies within 5 spaces
Action: Use area-of-effect ability

Behavior 5: Single-Target Burst
Checks: Enemy within range AND [ActionPoints] >= 2
Action: Use high-damage single-target attack

Behavior 6: Reposition
Checks: [Health] < 30 OR surrounded
Action: Move to advantageous position (high ground, cover, near minions)

Behavior 7: Standard Attack
Checks: Enemy adjacent
Action: Basic attack

Behavior 8: Summon Reinforcements (fallback)
Checks: (none, once per encounter)
Action: Spawn additional NPCs if mechanic exists
```

**Design Notes**: Multi-phase design. Cooldown tracking. Target prioritization. Positional awareness. Requires more bookkeeping but creates memorable encounters.

### Customizing These Patterns

To adapt a pattern for your campaign:

1. **Replace Action References**: Change "Use melee attack action" to your specific action name (e.g., "#Sword Slash")
2. **Adjust Thresholds**: Modify health triggers, ranges, and resource costs to match your balance
3. **Add Campaign-Specific Checks**: Include terrain checks ("On fire tile"), status effects, or unique mechanics
4. **Combine Patterns**: Mix behaviors from multiple patterns (e.g., Ranged Skirmisher + Glass Cannon flee logic)

### Behavior Priority Best Practices

**High Priority** (Behaviors 1-2):
- Emergency responses (flee when dying, heal critical ally)
- Special abilities or signature moves
- Optimal-condition attacks

**Medium Priority** (Behaviors 3-4):
- Standard actions (basic attacks, movement toward enemies)
- Resource management

**Low Priority** (Behaviors 5+):
- Fallback actions (wander, defend, wait)
- Always-succeeds behaviors

**Critical Rule**: Always include at least one behavior with no checks (or checks that always succeed) as your final behavior. This prevents NPCs from freezing when all conditions fail.

---

## See Also
- Chapter 21: Behaviors
- Chapter 16: Actions Design
