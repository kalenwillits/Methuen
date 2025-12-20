# Turn Structure

## Game Loop

After setup, Methuen campaigns follow a **game loop**: players take turns in initiative order, acting with their actors until completion conditions are met.

## The Turn

**Definition**: A **turn** is one player's opportunity to act with their actor (or cast of actors).

### Turn Order

Turns proceed according to **initiative**—the result of an initiative check that determines sequence. The actor (or cast) with the highest initiative acts first, followed by the next highest, and so on.

### Re-Rolling Initiative

Some campaigns require initiative to be re-rolled under specific conditions:

- At the start of each round
- When an actor doesn't use movement or actions
- When new actors join the encounter
- As specified by campaign Features (see Chapter 3: Features)

Check your campaign's initiative system for details.

## Turn Phases

Campaigns define turn structure in one of two ways:

### Flexible Turn Structure

**Definition**: Actions and movement can be performed in any order during your turn.

- Move, then act
- Act, then move
- Split movement (move, act, move again)
- Take multiple actions in any sequence

**Limitation**: Total actions and movement still limited by features and resources

**Example**: An actor with "Single Action Per Turn" and "Move up to 5 spaces" could:
- Move 2 spaces, perform action, move 3 spaces
- Perform action, then move 5 spaces
- Move 5 spaces, perform action

### Phased Turn Structure

**Definition**: Turns follow a strict sequence of phases.

**Common Phase Order**:

1. **Start Phase**: Resolve "start of turn" triggers
2. **Movement Phase**: All movement must occur now
3. **Action Phase**: Perform actions
4. **End Phase**: Resolve "end of turn" triggers

**Note**: Once you proceed to the next phase, you cannot return to a previous phase.

## Action Economy

**Definition**: **Action economy** refers to how many actions an actor can perform per turn.

### Determining Action Limits

Campaigns define action limits through Features:

```
Single Action Per Turn (Feature)
Each actor may perform exactly 1 action per turn
```

```
Action Point Economy (Feature)
Actors spend 1 [ActionPoint] per action performed
```

> See **Chapter 3: Features** for more action economy examples.

### Free Actions

Some campaigns define **free actions**—operations that don't count against action limits:

- Speaking or signaling
- Dropping an item
- Looking up information

Check your campaign for which actions are free.

## Movement Economy

Similarly, campaigns define movement through Features (see Movement Features in Chapter 3):

### Resource-Based Movement
```
Dexterous Movement (Feature)
Move up to [Dexterity] spaces per turn
```

### Fixed Movement
```
Standard Movement (Feature)
All actors move 6 spaces per turn
```

### Action-Point Movement
"Spend 1 ActionPoint per space moved" - movement competes with actions

## Passing and Waiting

### Passing Your Turn

You may choose to pass your turn, performing no actions or movement. Depending on campaign rules, this may:

- Preserve initiative for next round
- Trigger initiative re-roll
- Grant bonuses to next turn

### Delayed Actions

Some campaigns allow holding actions to trigger later. Check your campaign for whether this is permitted.

## End of Round

**Definition**: A **round** is complete when all actors have taken their turns.

At the end of a round:

1. Resolve any "end of round" effects
2. Re-roll initiative (if required by campaign)
3. Begin the next round with the highest initiative

## Reactions During Others' Turns

**Reactions** are special actions that can be performed outside your turn, triggered by specific events during another actor's turn.

**Example**: "When an adjacent actor moves away, you may spend 1 ActionPoint to perform a basic attack"

See **Chapter 8: Reactions** for details on how reactions work.

## Cast Turns

If multiple actors form a **cast** (share initiative), they act together during a single turn:

- All cast members share the same turn
- Actions and movement can be coordinated
- Order of cast member actions is flexible

See **Chapter 20: Casts and Groups** for details.

## Turn Summary

A typical turn consists of: start-of-turn triggers → perform actions → execute movement → end-of-turn triggers → announce complete.

> For the complete turn checklist, see **Quick Reference** (Appendix).

---

## See Also

- **Chapter 7**: Taking Actions - How to execute actions
- **Chapter 8**: Reactions - Acting outside your turn
- **Chapter 13**: Turn Structure Design - For campaign designers
