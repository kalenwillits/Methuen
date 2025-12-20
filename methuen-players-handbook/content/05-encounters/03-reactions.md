# Reactions

## What are Reactions?

**Definition**: A **reaction** is a special type of action that can be performed outside your normal turn, triggered by specific events during another actor's turn.

## How Reactions Work

### Trigger Events

Reactions specify exact triggers:

**Movement Triggers**:
- "When an adjacent actor moves away from you"
- "When an actor enters a tile within 3 spaces"

**Action Triggers**:
- "When you are targeted by an action"
- "When an adjacent actor performs an action"

**Resource Triggers**:
- "When your health drops below 5"
- "When an actor within range gains resources"

**Turn Triggers**:
- "At the start of any actor's turn"
- "At the end of any actor's turn"

### Reaction Structure

Reactions follow the same if/do/then/else structure as normal actions, plus a **trigger** component:

```
Reaction: Opportunity Strike
Trigger: Adjacent actor moves away
if: [ActionPoints] >= 1
do: [Target Health] -= (1d4 + [Strength])
then: [ActionPoints] -= 1
```

**Execution**: When triggered → Check condition → If true: deal damage → Always: pay cost

### Performing Reactions

When a trigger event occurs:

1. **Check if trigger applies**: Does the event match your reaction's trigger?
2. **Declare reaction**: Announce you're using the reaction
3. **Evaluate condition (if)**: Check if the condition is true or false
4. **Execute conditional effect**:
   - If TRUE: Execute (do)
   - If FALSE: Execute (else) if defined
5. **Execute always-effect (then)**: Apply effects that always execute
6. **Resume original action**: The triggering actor continues their turn

## Reaction Timing

Reactions interrupt the normal flow of the turn:

**Example Sequence**:
1. Opponent begins moving away from you
2. Movement triggers your Opportunity Strike reaction
3. You declare reaction and pay costs
4. Resolve reaction (deal damage)
5. Opponent continues their movement

Some reactions specify **when** they occur:

- **Before**: Reaction resolves before the triggering event
- **After**: Reaction resolves after the triggering event
- **Instead**: Reaction replaces the triggering event (if successful)

**Check your campaign** for timing details on each reaction.

## Reaction Limits

Campaigns define limits on reactions:

### Per Turn Limit

"You may use one reaction per turn (any actor's turn)"

- Tracks across all actors' turns
- Resets at the start of your turn

### Per Round Limit

"You may use up to three reactions per round"

- Tracks across entire round
- Resets at start of new round

### Resource Cost Limit

"Reactions cost ActionPoints like normal actions"

- Limited by available resources
- Must have resources to react

### No Limit

Some campaigns allow unlimited reactions (if you can pay costs)

## Common Reaction Types

### Defensive Reactions

Reduce or avoid incoming harm:

```
Reaction: Dodge
Trigger: You are targeted by a ranged action
if: [ActionPoints] >= 1
do: [ActionPoints] -= 1
then: Reduce damage by [Dexterity]
```

### Counter Reactions

Respond to actions with your own action:

```
Reaction: Counter-Spell
Trigger: An actor within 10 spaces performs a spell action
if: [Mana] >= 3
do: [Mana] -= 3
then: Cancel the triggering spell
```

### Opportunity Reactions

Exploit enemy mistakes:

```
Reaction: Opportunity Strike
Trigger: Adjacent actor moves away
if: [ActionPoints] >= 1
do: [ActionPoints] -= 1
then: Perform basic attack
```

### Triggered Benefits

Gain advantages from events:

```
Reaction: Vindictive
Trigger: You take damage
then: Gain +2 to your next action's expression
```

## Reaction Chains

Can reactions trigger other reactions?

**Campaign-Specific**: Some allow chaining, others prohibit it

**Example Chain** (if allowed):
1. Actor A moves, triggering Actor B's reaction
2. Actor B attacks Actor C with the reaction
3. Actor C's "When Attacked" reaction triggers
4. Actor C responds to Actor B
5. All reactions resolve, then Actor A continues moving

**Anti-Chain Rule** (common restriction):
"Reactions cannot trigger other reactions"

## Canceling Actions with Reactions

Some reactions can prevent actions:

```
Reaction: Interrupt
Trigger: An actor within 5 spaces begins an action
if: (1d20+[Speed]) > [Target Speed]
do: [ActionPoints] -= 2
then: Target's action is canceled
else: Target's action proceeds normally
```

**Note**: These examples use the "cost in do" pattern, meaning you only pay the reaction cost if the condition succeeds. This prevents wasting resources on failed reactions.

## Tracking Reactions

On your character sheet, track:

- **Available Reactions**: Which reactions you have
- **Reaction Uses**: How many reactions you've used this turn/round
- **Trigger Conditions**: What events trigger each reaction

## Passive vs Active Reactions

### Active Reactions

Require player decision:
- Player chooses whether to use when triggered
- Can be saved for better opportunities

### Passive Reactions

Automatic when triggered:
- No player choice
- Always occur if conditions met
- Treated as features with triggered effects

**Check your campaign** for which reactions are which.

---

## See Also

- **Chapter 7**: Taking Actions - Action structure
- **Chapter 6**: Turn Structure - Understanding turn flow
- **Chapter 12**: Reactions Design - For campaign designers
