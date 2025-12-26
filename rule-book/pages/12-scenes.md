# Chapter 12: Scenes

## 12.1 Overview

Scenes are the narrative and decision-making phase of Methuen gameplay. They occur between encounters, providing story context, player choices, and non-tactical interactions. Scenes connect encounters into a coherent campaign experience.

## 12.2 Scene Definition

### 12.2.1 Formal Definition

A **Scene** is a game phase characterized by:
- Narrative or decision-driven content
- Non-spatial interaction (no map required)
- Linear or branching progression
- Transition to encounters or other scenes

### 12.2.2 Scene Properties

| Property | Description |
|----------|-------------|
| Type | Narrative, Choice, Check, or combination |
| Content | Text, options, or mechanics to resolve |
| Transitions | Next scene(s) or encounter(s) |
| Effects | Changes to game state |

## 12.3 Scene Types

### 12.3.1 Narrative Scenes

**Narrative** scenes present descriptive or story-driven text. They:
- Establish setting and atmosphere
- Provide context for upcoming encounters
- Advance the campaign story
- Introduce characters or situations

**Structure**:
```
Scene: The Dark Forest
Type: Narrative

The path narrows as ancient oaks crowd overhead, their branches
blocking the fading daylight. Strange sounds echo from the
shadows, and the air grows cold.

Ahead, the forest opens into a small clearing where a
crumbling stone structure waits.

Transition: Scene "The Ruined Shrine"
```

### 12.3.2 Choice Scenes

**Choice** scenes present multiple options for players to select. They:
- Allow player agency in story direction
- May affect resources or conditions
- Lead to different outcomes based on selection
- Can be random or player-determined

**Structure**:
```
Scene: The Merchant's Offer
Type: Choice

A traveling merchant approaches with a proposition:
"I have rare goods, but limited supply. Choose wisely."

Options:
A) Purchase the healing potion (Cost: 50 Gold)
   Effect: Gain 1 Healing Potion
   Transition: Scene "The Road Continues"

B) Purchase the map fragment (Cost: 30 Gold)
   Effect: Gain feature "Map Knowledge" for next encounter
   Transition: Scene "The Road Continues"

C) Decline and continue
   Effect: None
   Transition: Scene "The Road Continues"

D) Attempt to steal (Risk)
   Transition: Scene "Theft Attempt"
```

### 12.3.3 Check Scenes

**Check** scenes require dice rolls to determine outcomes. They:
- Introduce randomness to narrative progression
- Test character resources or capabilities
- Create tension and uncertainty
- Fork story based on success or failure

**Structure**:
```
Scene: Crossing the Chasm
Type: Check

A narrow bridge spans a deep chasm. The wooden planks
look weathered and unstable.

Check: 1d20 + [Dexterity] >= 12

Success:
  Text: You carefully cross, testing each plank before
        committing your weight. The bridge holds.
  Transition: Scene "The Other Side"

Failure:
  Text: A plank snaps beneath your foot. You catch yourself
        but take damage in the scramble.
  Effect: [Health] -= 1d6
  Transition: Scene "The Other Side"
```

### 12.3.4 Combined Scenes

Scenes may combine multiple types:

```
Scene: The Guardian's Test
Type: Narrative + Choice + Check

A spectral figure blocks the passage, speaking in an
ancient tongue that somehow you understand.

"Prove your worth, mortal. Choose your trial."

Options:
A) Trial of Strength
   Check: 1d20 + [Strength] >= 15
   Success: Gain feature "Guardian's Blessing"
   Failure: [Health] -= 2d6

B) Trial of Wisdom
   Check: 1d20 + [Intelligence] >= 15
   Success: Gain feature "Guardian's Blessing"
   Failure: [Wisdom] -= 2

C) Trial of Courage
   Check: 1d20 >= 18 (no modifier)
   Success: Gain feature "Guardian's Blessing"
   Failure: Gain condition "Shaken" for next encounter

All transitions lead to: Encounter "The Inner Sanctum"
```

## 12.4 Scene Mechanics

### 12.4.1 Player Participation

During scenes, players interact differently than in encounters:

**Discussion**: All players may discuss options, share opinions, and roleplay their characters' reactions. There is no turn order during scenes.

**Decision-Making**: The campaign may specify how choices are made:
- **Group consensus**: Players agree on a choice together
- **Lead character**: One player's character is the spokesperson
- **Vote**: Simple majority or unanimous agreement
- **Individual**: Each player makes their own choice (for checks that apply to specific actors)

**When Players Disagree**: If players cannot agree on a choice, common resolutions include:
- The Game Master decides
- The character with the highest relevant resource decides
- A die roll breaks the tie

**Character Resources**: Checks during scenes typically use one character's resources. The campaign should specify whose resources apply, or players may volunteer their character for the check.

### 12.4.2 Resource Changes

Scenes may modify resources:

**Costs**:
```
This option costs 50 Gold to select.
If insufficient Gold, the option is unavailable.
```

**Gains**:
```
Selecting this option grants 100 Experience to all party members.
```

**Losses**:
```
This choice results in [Health] -= 1d10 for the lead character.
```

### 12.4.3 Feature Acquisition

Scenes may grant or remove features:

```
Effect: Gain feature "Blessed by the Oracle"
This feature grants +2 to all checks until the next encounter.
```

### 12.4.4 Information Revelation

Scenes may reveal information:

```
Effect: Learn the true name of the villain.
This information unlocks additional dialogue options in future scenes.
```

## 12.5 Scene Flow

### 12.5.1 Scene Execution

1. **Present Content**: Display narrative text
2. **Offer Options**: Show available choices (if any)
3. **Resolve Checks**: Roll dice for check scenes (if any)
4. **Apply Effects**: Modify resources, grant features, etc.
5. **Determine Transition**: Identify next scene or encounter
6. **Proceed**: Move to the next phase

### 12.5.2 Branching

Scenes may branch based on:
- Player choices
- Check results
- Resource thresholds
- Previous scene outcomes
- Campaign state

```
Scene Branches:

If [Party Gold] >= 100:
  Option D becomes available: "Bribe the guard"

If feature "Known Criminal" is active:
  Guard becomes hostile, transition to Encounter "Jail Break"
```

### 12.5.3 Loops and Returns

Scenes may loop or return to previous scenes:

```
Scene: The Tavern
After any conversation, return to The Tavern until
"Leave the Tavern" is selected.
```

## 12.6 Scene Transitions

### 12.6.1 To Scenes

Scenes may transition to other scenes:
```
Transition: Scene "The Next Morning"
```

### 12.6.2 To Encounters

Scenes may transition to encounters:
```
Transition: Encounter "Ambush in the Alley"
```

### 12.6.3 Conditional Transitions

Transitions may be conditional:
```
If Check succeeded: Transition to Scene "Safe Passage"
If Check failed: Transition to Encounter "Trap Sprung"
```

### 12.6.4 Multiple Transitions

Some scenes offer multiple transition paths:
```
Options lead to:
A) Scene "The High Road"
B) Scene "The Low Road"
C) Scene "The Hidden Path" (requires [Perception] >= 15)
```

## 12.7 Scene Events

### 12.7.1 Triggered Scenes

Scenes may trigger during encounters:

```
Event: Reinforcement Warning
Trigger: Round 3 of any encounter in the Fortress
Effect: Interrupt to Scene "The Alarm Sounds"
Resume: Continue encounter with new actors deployed
```

### 12.7.2 Conditional Scenes

Some scenes only occur if conditions are met:

```
Scene: The Secret Door
Condition: Feature "Map Knowledge" is active
If condition not met: Skip to Scene "Dead End"
```

## 12.8 Random Scenes

### 12.8.1 Random Encounters

Campaigns may include random scene selection:

```
Scene: Travel Event
Roll 1d6:
1-2: Scene "Uneventful Journey"
3-4: Scene "Traveler Encounter"
5: Scene "Roadside Discovery"
6: Encounter "Bandit Ambush"
```

### 12.8.2 Random Outcomes

Choices may have random elements:

```
Option: Search the ruins
Roll 1d20:
1-5: Find nothing
6-15: Find 2d10 Gold
16-19: Find a Minor Artifact
20: Find a Major Artifact and trigger Encounter "Guardian Awakens"
```

## 12.9 Scene Records

### 12.9.1 Tracking Scene Outcomes

Track scene results that affect future content:
- Choices made
- Checks passed/failed
- Resources gained/lost
- Features acquired
- NPCs encountered

### 12.9.2 Campaign Flags

Scenes may set flags for future reference:

```
Effect: Set flag "Helped the Merchant"

Later Scene:
If flag "Helped the Merchant" is set:
  The merchant offers a discount on all goods.
```

## 12.10 Scene Writing Guidelines

### 12.10.1 Clarity

Scene text should:
- Be clear about available options
- Specify all costs and effects
- Indicate check difficulties when appropriate
- Make transitions explicit

### 12.10.2 Brevity

Scene text should:
- Convey necessary information efficiently
- Avoid excessive detail that slows play
- Balance narrative interest with gameplay pacing

### 12.10.3 Player Agency

Scenes should:
- Offer meaningful choices when possible
- Make check outcomes feel significant
- Connect player decisions to campaign consequences
- Avoid purely cosmetic choices disguised as meaningful ones

### 12.10.4 Scene Pacing

**For Players**:
- Do not rush scene decisions; they often have lasting consequences
- Roleplay character reactions if the group enjoys it
- Ask clarifying questions about options before committing

**For Game Masters**:
- Read scene text expressively but do not over-elaborate
- Give players time to discuss, but set a reasonable limit (2-3 minutes for most choices)
- If players are stuck, offer to clarify options or suggest in-character discussion
- Use scene length to control session pacing: longer narrative scenes after intense encounters

**For Campaign Designers**:
- Vary scene length: some should be quick transitions, others pivotal decisions
- Balance narrative scenes (world-building) with choice scenes (player agency)
- Avoid long sequences of scenes without encounters; players may feel passive
- Use check scenes sparingly; too many rolls can feel arbitrary

## 12.11 Scene Examples

### 12.11.1 Simple Narrative Scene

```
Scene: Dawn Breaks
Type: Narrative

The first light of dawn reveals the devastation of the
previous night's battle. Smoke rises from the village,
and survivors begin to emerge from hiding.

The village elder approaches, gratitude and sorrow
mixing in their weathered face.

"You saved us, but at great cost. The temple to the
north may hold the key to preventing this from
happening again."

Transition: Scene "Preparing for the Journey"
```

### 12.11.2 Complex Choice Scene

```
Scene: The Prisoner's Dilemma
Type: Choice

The captured spy offers information in exchange for freedom.
Their eyes dart nervously between you and the exit.

Options:

A) Accept the deal
   Effect: Gain feature "Spy's Information"
   Effect: Set flag "Released the Spy"
   Transition: Scene "The Information"

B) Refuse and imprison them
   Effect: Gain 50 Gold (bounty)
   Effect: Set flag "Imprisoned the Spy"
   Transition: Scene "To the Dungeon"

C) Execute them
   Effect: [Reputation with Thieves Guild] -= 10
   Effect: Set flag "Killed the Spy"
   Transition: Scene "A Message Sent"

D) [Requires Intimidation 15+] Threaten for information
   Check: 1d20 + [Intimidation] >= 18
   Success: Gain feature "Spy's Information", gain 50 Gold
   Failure: Spy attacks, Transition to Encounter "Cornered Spy"
```

### 12.11.3 Check Scene with Stakes

```
Scene: The Crumbling Tower
Type: Check

The ancient tower groans as you climb. Each step could
be your last as stones shift beneath your feet.

Check: 1d20 + [Dexterity] >= 14

Critical Success (Natural 20):
  Text: You navigate the hazards with supernatural grace,
        discovering a hidden cache along the way.
  Effect: Gain 100 Gold, 1 Potion of Healing
  Transition: Scene "The Tower Summit"

Success:
  Text: Careful steps bring you safely to the top.
  Transition: Scene "The Tower Summit"

Failure:
  Text: A stone gives way. You catch yourself but are
        battered by falling debris.
  Effect: [Health] -= 2d6
  Transition: Scene "The Tower Summit"

Critical Failure (Natural 1):
  Text: The floor collapses entirely.
  Effect: [Health] -= 4d6
  Check: [Health] > 0
    If true: Transition to Scene "Trapped in the Rubble"
    If false: Transition to Scene "Death in the Tower"
```
