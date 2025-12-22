# Setup and Play

## Reading Your Campaign Book

Campaign books vary in structure, but look for these sections:

**Getting Started / Character Creation**
How to create your actor: name, starting resources, initial position.

**Resources**
List of all resources and their initialization rules.

**Actions**
Operations your actor can perform.

**Features**
Special rules that modify core mechanics: initiative, movement, turn structure, victory conditions.

**Maps and Encounters**
Scenarios, enemy placements, terrain.

**Victory Conditions**
How to win.

## Creating Your Actor

Follow your campaign's character creation process:

**1. Choose or Generate Name**
Some campaigns provide names, others let you choose.

**2. Initialize Starting Resources**
Your campaign specifies which resources to initialize at creation. Common patterns:

```
Health: 1d20 + Constitution
Energy: 1d10 + Endurance
ActionPoints: 3 (fixed)
Gold: 0 (default)
```

Roll dice as instructed and record values.

**3. Record Position and Heading**
Note your starting location on the map and which direction you face.

**4. Note Available Actions**
Write down or reference which actions your actor can perform.

**5. Record Features**
Note any special rules that apply to your actor.

## Setup Phase

**1. Read Victory Condition**
Understand how to win before you start.

**2. Set Up Map**
Place terrain, markers, and actor positions as specified.

**3. Determine Initiative**
Roll or calculate initiative for all actors.

**4. Prepare Materials**
Have dice, character sheet, and campaign book ready.

## Playing the Game

### Round Structure

A **round** is one full cycle where all actors take their turns.

1. Highest initiative acts first
2. Next highest initiative acts
3. Continue until all actors have acted
4. Start new round

### Your Turn

Use the turn structure from Chapter 3:

**CHECK** → **ACT** → **MOVE** → **END**

### Between Turns

Track changes to the game state:
- Actor positions
- Resource values
- Status effects
- Round count (if relevant)

### Resolving Conflicts

When rules are unclear:
1. Check the campaign book's Features
2. Check this handbook's core rules
3. Apply most literal interpretation
4. Record the decision for consistency

## Common Scenarios

### Taking Damage

When you take damage:
1. Check if Health is initialized. If not, initialize it now.
2. Subtract damage amount from Health.
3. If Health reaches 0, apply your campaign's defeat condition.

**Example**: Goblin deals 5 damage. Your Health is 27. New Health: 22.

### Running Out of Resources

If an effect requires a resource you don't have:
- The (if) condition fails
- The (do) effect doesn't execute
- The (else) effect executes (if defined)
- The (then) effect still executes

**Example**: Basic Attack requires 1 ActionPoint. You have 0.
- Condition fails (0 >= 1 is false)
- No damage dealt (do doesn't execute)
- ActionPoint cost still applied (then always executes, reduces to 0)

### Initializing Resources Mid-Game

When a resource is first referenced:
1. Look up initialization rule in campaign book
2. Apply the rule (roll dice, calculate)
3. Record the value
4. Continue with the current operation

### Actor Defeat

When Health (or campaign-specified resource) reaches 0:
1. Apply campaign's defeat rules
2. Common outcomes:
   - Actor removed from map
   - Actor becomes inactive
   - Game ends (if player actor)

Check your campaign for specific defeat consequences.

## Tips for New Players

**Keep the Quick Reference handy** (Chapter 6)
Use it to look up action structure, dice notation, and turn sequence.

**Track resources carefully**
Update your sheet immediately after each change.

**Declare actions clearly**
State the action name and target before resolving.

**Ask "What happens if..."**
Test your understanding by walking through action steps.

**Start with simple actions**
Master basic resource checks before attempting complex combinations.

## Example: First Turn Walkthrough

**Scenario**:
- Campaign: "Dungeon Raid"
- Your actor: Raven (Strength 4, Dexterity 3, Health 27, ActionPoints 3)
- Position: 0N 0E, facing North
- Enemy: Goblin at 1N 0E (Health 12)
- Initiative: You 15, Goblin 10 (you go first)

**Your First Turn**:

**CHECK**
- Start-of-turn effects: None
- Available actions: Basic Attack, Defend, Move
- Resources available: ActionPoints 3

**ACT**
- Choose: Basic Attack
- Declare: "I use Basic Attack on the Goblin at 1N 0E"
- Check condition: Adjacent? Yes. ActionPoints >= 1? Yes.
- Execute (do): Roll 1d6, result 4. Deal 4 damage. Goblin Health: 12 → 8
- Execute (then): ActionPoints: 3 → 2

**MOVE**
- Campaign allows 6 spaces movement per turn
- Choose: Stay in position
- Movement: None

**END**
- End-of-turn effects: None
- Announce: "Turn complete"

**Goblin's Turn**:
(Goblin acts according to campaign's behavior rules)

## Multi-Turn Strategy

Plan across multiple turns:

**Resource Management**
- Don't spend all ActionPoints at once
- Save resources for reactions (if available)
- Plan for resource regeneration

**Positioning**
- Move toward objectives
- Maintain advantageous positions
- Stay in range of allies

**Risk Assessment**
- Estimate enemy capabilities
- Calculate odds before attacking
- Prepare defensive actions

## Ending the Game

The game ends when victory conditions are met:

**Common victory conditions**:
- All enemies defeated
- Objective reached
- Resource threshold achieved
- Survival duration met

**Common defeat conditions**:
- All player actors defeated
- Time limit expired
- Critical resource depleted

Check your campaign book for specific end-game rules.
