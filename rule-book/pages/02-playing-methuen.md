# Chapter 2: Playing Methuen

## 2.1 Overview

This chapter explains how to actually play a Methuen game. It walks through what happens in a session, how turns work, and what you need to know to get started. Technical details appear in later chapters; this chapter focuses on the experience of play.

## 2.2 What Happens in a Session

A Methuen session alternates between two types of gameplay: **scenes** and **encounters**.

### 2.2.1 Scenes

During scenes, the game presents narrative content: descriptions of locations, dialogue with characters, and situations requiring decisions. Scenes may ask you to:

- Choose between options that affect the story
- Make Checks (dice rolls) to determine outcomes
- Spend or receive resources
- Learn information that matters later

Scenes do not use maps or tactical positioning. They advance the story and set up encounters.

**Example Scene**:
> The village elder approaches your party. "Bandits have taken the eastern road. You can confront them directly, or take the forest path and flank them."
>
> Choose:
> - A) Take the eastern road (leads to Encounter: Road Ambush)
> - B) Take the forest path (leads to Encounter: Forest Approach)

### 2.2.2 Encounters

During encounters, play becomes tactical. Actors occupy positions on a grid map and take turns performing actions. This is where combat happens, where positioning matters, and where resource management becomes critical.

Encounters have three phases:
1. **Deployment**: Place actors on the map
2. **Initiative**: Determine turn order
3. **Turns**: Take turns until completion conditions are met

### 2.2.3 The Session Flow

A typical session looks like this:

```
Scene: "The Quest Begins"
  - Read narrative text
  - Make a choice
    |
    v
Encounter: "First Battle"
  - Deploy actors
  - Roll initiative
  - Take turns until enemies defeated
    |
    v
Scene: "Aftermath"
  - See results of battle
  - Gain rewards
  - Learn next objective
    |
    v
[Continue alternating...]
```

## 2.3 Your First Encounter

This section walks through a complete encounter from start to finish.

### 2.3.1 Setup

Before the encounter begins:

1. **Lay out the map**: Use the grid provided by the campaign, either physical or digital
2. **Identify deployment zones**: The campaign specifies where each side places actors
3. **Gather your actors**: Know which actors you control and their capabilities
4. **Prepare dice**: Have the dice types your campaign uses ready

### 2.3.2 Deployment Phase

During deployment, actors are placed on the map.

**Example**:
> The map shows a forest clearing. Player deployment zone is the southern edge (rows 1-2). Enemy deployment zone is the northern edge (rows 7-8).
>
> Player places Knight at 1N 3E facing north, Archer at 2N 5E facing north.
> Campaign places Goblin Warrior at 7N 3E, Goblin Archer at 8N 4E.

All actors should have:
- A location on the map
- A heading (direction they face)
- Their starting resource values recorded

### 2.3.3 Initiative Phase

Roll to determine who acts first. The default is 1d100 for each actor or cast, acting in descending order (highest first).

**Example**:
> Knight rolls 72, Goblin Warrior rolls 45, Archer rolls 38, Goblin Archer rolls 61.
>
> Turn order: Knight (72), Goblin Archer (61), Goblin Warrior (45), Archer (38).

Record this order. It remains fixed for the encounter unless modified by special effects.

### 2.3.4 Taking Turns

Each turn follows this structure:

```
START OF TURN
  - Resources refresh (Action Points reset to 3)
  - Start-of-turn effects trigger
       |
       v
ACTION PHASE
  - Spend Action Points to perform actions
  - Continue until out of actions or choose to stop
       |
       v
END OF TURN
  - End-of-turn effects trigger
  - Pass to next actor in initiative order
```

**Example Turn**:
> It is the Knight's turn.
>
> **Start of Turn**: Action Points set to 3.
>
> **Action Phase**:
> - Knight uses Move action (cost: 1 AP) to advance 3 tiles north. Now at 4N 3E.
> - Knight uses Move action again (cost: 1 AP) to advance 3 more tiles. Now at 7N 3E, adjacent to Goblin Warrior.
> - Knight uses Strike action (cost: 1 AP) targeting Goblin Warrior.
>   - Roll: 1d20 + Attack (5) = 14 vs Goblin Defense (12). Hit!
>   - Damage: 1d8 + Strength (4) = 7 damage.
>   - Goblin Health: 10 - 7 = 3.
> - Knight has 0 Action Points remaining.
>
> **End of Turn**: No end-of-turn effects. Pass to Goblin Archer.

### 2.3.5 Resolving Actions

When an actor performs an action, follow these steps:

1. **Declare** the action and target
2. **Verify** the action is valid (actor has it, target is in range, costs can be paid)
3. **Roll** if the action has a condition (the "if" component)
4. **Apply effects** based on success or failure
5. **Pay costs** (the "then" component, which always executes)

See Chapter 6 for complete action rules.

### 2.3.6 Tracking the Encounter

During the encounter, track:

| What | How |
|------|-----|
| Turn order | List actors in initiative order, mark current actor |
| Round number | Increment after all actors have acted once |
| Actor positions | Tokens on map or coordinate records |
| Resources | Health, Action Points, and other values per actor |
| Active effects | Conditions, buffs, and their remaining durations |

### 2.3.7 Completing the Encounter

The encounter ends when completion conditions are met. Common conditions include:

- **All enemies defeated**: Every opposing actor reaches 0 Health
- **Objective achieved**: A player actor reaches the exit tile, activates a mechanism, etc.
- **Survival**: A certain number of rounds pass with at least one player actor active
- **Retreat**: All player actors exit via designated tiles

The campaign specifies what happens after each outcome (victory, defeat, or other).

## 2.4 The Turn in Detail

### 2.4.1 Start of Turn

At the start of each turn:

1. **Resource Refresh**: By default, Action Points reset to 3 (see Chapter 4, Section 4.10)
2. **Start-of-Turn Effects**: Features and conditions that trigger "at the start of your turn" resolve now
3. **Duration Checks**: Effects that expire "at the start of your turn" end now

This happens automatically before the actor can take any actions.

### 2.4.2 Action Phase

During the action phase, the active actor may:

- Perform any action they have access to
- Perform actions in any order
- Perform the same action multiple times (if resources allow)
- Choose to take no actions

There is no inherent limit on how many actions an actor can take. The limiting factor is typically Action Points: most actions cost 1 AP, and actors start with 3 AP by default.

The action phase ends when:
- The actor declares their turn complete, OR
- The actor cannot perform any more actions (no resources, no valid targets, etc.)

### 2.4.3 End of Turn

At the end of each turn:

1. **End-of-Turn Effects**: Features and conditions that trigger "at the end of your turn" resolve now
2. **Duration Countdown**: Effects with duration "until end of turn" expire now
3. **Pass Control**: The next actor in initiative order becomes the active actor

### 2.4.4 Rounds

A **round** is complete when every actor in the initiative order has taken one turn. After the last actor's turn:

1. **End-of-Round Effects**: Triggers that activate "at the end of each round" resolve
2. **Round Counter**: Increment the round number
3. **Start-of-Round Effects**: Triggers that activate "at the start of each round" resolve
4. **New Round Begins**: Return to the first actor in initiative order

Round count matters for:
- Time-limited objectives ("survive 5 rounds")
- Scheduled events ("reinforcements arrive at round 3")
- Effect durations ("lasts 2 rounds")

## 2.5 Common Questions

### 2.5.1 What happens when an actor reaches 0 Health?

By default, an actor reaching 0 Health is **defeated** and removed from the encounter. They no longer take turns, cannot be targeted, and do not occupy space on the map.

Campaigns may override this with Features that provide alternate defeat conditions (unconscious and can be revived, for example).

### 2.5.2 How many actions can I take per turn?

As many as you have resources for. By default, actors have 3 Action Points and most actions cost 1 AP, so a typical turn includes 3 actions. But some actions cost 0 AP (free actions), some cost 2+ AP, and Features may grant additional Action Points.

### 2.5.3 Can I move and attack in the same turn?

Yes, if you have the Action Points for both. A common turn is: Move (1 AP), Move (1 AP), Attack (1 AP). Or: Attack (1 AP), Move (1 AP), Attack (1 AP).

Note that Methuen does not provide inherent movement. You must have a Move action (or similar) defined by your campaign.

### 2.5.4 What if I do not want to use all my Action Points?

You may end your turn with unused Action Points. By default, unspent Action Points do not carry over; they reset at the start of your next turn. Some campaigns may provide Features that allow banking or other behaviors.

### 2.5.5 When do I roll dice?

Roll dice when:
- An action has a condition to evaluate (the "if" component)
- A scene presents a Check
- An Expression in any context includes dice notation (like `1d8 + 3`)

The campaign and action definitions tell you when rolls are needed.

### 2.5.6 How do I know what my actor can do?

Your actor has:
- **Actions**: Listed in their definition or granted by the campaign
- **Features**: Special rules that modify capabilities
- **Resources**: Values that enable or constrain actions

Check your actor's definition and any campaign-wide actions available to all actors.

## 2.6 Putting It Together: A Sample Round

Here is a complete round of play in narrative form:

---

**Round 1, Initiative Order**: Sera (Knight, 18), Goblin Chief (15), Marcus (Wizard, 12), Goblin Warrior (8)

---

**Sera's Turn** (Player)

Sera begins with 3 Action Points. The Goblin Chief is 5 tiles away.

- **Action 1**: Move. Sera advances 3 tiles toward the Goblin Chief. (2 AP remaining)
- **Action 2**: Move. Sera advances 2 more tiles. She is now adjacent to the Goblin Chief. (1 AP remaining)
- **Action 3**: Strike, targeting Goblin Chief.
  - Roll 1d20 + 6 (Attack) = 17 vs Defense 14. Hit!
  - Roll 1d8 + 4 (damage) = 9 damage.
  - Goblin Chief Health: 20 - 9 = 11.
  - (0 AP remaining)

Sera ends her turn.

---

**Goblin Chief's Turn** (Strategy-controlled)

The Goblin Chief follows the Aggressive strategy. It has 3 Action Points.

- **Behavior check**: Adjacent enemy? Yes (Sera). Attack.
- **Action 1**: Strike, targeting Sera.
  - Roll 1d20 + 5 = 11 vs Defense 16. Miss!
  - (2 AP remaining)
- **Behavior check**: Adjacent enemy? Yes. Attack.
- **Action 2**: Strike, targeting Sera.
  - Roll 1d20 + 5 = 19 vs Defense 16. Hit!
  - Roll 1d10 + 3 = 8 damage.
  - Sera Health: 25 - 8 = 17.
  - (1 AP remaining)
- **Behavior check**: Adjacent enemy? Yes. Attack.
- **Action 3**: Strike, targeting Sera.
  - Roll 1d20 + 5 = 7 vs Defense 16. Miss!
  - (0 AP remaining)

Goblin Chief ends its turn.

---

**Marcus's Turn** (Player)

Marcus begins with 3 Action Points. He is 4 tiles from the combat.

- **Action 1**: Cast Fireball, targeting a tile adjacent to Goblin Chief.
  - Cost: 2 AP and 5 Mana.
  - The Goblin Chief is in the area of effect.
  - Roll 1d20 + 7 (Spellcasting) = 22 vs Defense 14. Hit!
  - Roll 3d6 = 11 fire damage.
  - Goblin Chief Health: 11 - 11 = 0. Defeated!
  - (1 AP remaining, Mana reduced)

The Goblin Chief is removed from play.

- **Action 2**: Marcus saves his last AP. (He could act but chooses not to.)

Marcus ends his turn.

---

**Goblin Warrior's Turn** (Strategy-controlled)

The Goblin Warrior follows the Aggressive strategy. Its leader is defeated.

- **Behavior check**: Adjacent enemy? No.
- **Behavior check**: Move toward enemy? Yes.
- **Action 1**: Move toward Sera. (2 AP remaining)
- **Behavior check**: Adjacent enemy? No (still 2 tiles away).
- **Action 2**: Move toward Sera. Now adjacent. (1 AP remaining)
- **Behavior check**: Adjacent enemy? Yes. Attack.
- **Action 3**: Strike, targeting Sera.
  - Roll 1d20 + 3 = 14 vs Defense 16. Miss!
  - (0 AP remaining)

Goblin Warrior ends its turn.

---

**End of Round 1**

All actors have taken their turns. Round counter advances to 2.
Victory condition (all enemies defeated) not yet met; one Goblin Warrior remains.

---

This cycle continues until completion conditions are met.

## 2.7 Next Steps

Now that you understand the flow of play:

- **Chapter 3** explains dice notation and mathematical expressions
- **Chapter 4** covers resources in detail, including default mechanics
- **Chapter 6** provides complete rules for actions
- **Chapter 11** gives the full encounter procedure
- **Appendix B** provides a longer example of play
- **Appendix C** offers a quick reference for play
