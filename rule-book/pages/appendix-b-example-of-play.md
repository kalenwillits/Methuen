# Appendix B: Example of Play

This appendix provides a complete narrative walkthrough of a Methuen encounter, showing how the rules work in practice.

## B.1 Setup

**The Campaign**: "The Dark Citadel" - a fantasy adventure campaign.

**The Players**:
- Alex controls Sera, a Knight
- Beth controls Marcus, a Wizard

**The Encounter**: "Goblin Ambush" - the first combat encounter of the campaign.

## B.2 The Actors

### Player Actors

**Sera (Knight)** - controlled by Alex
```
Health: 20
Strength: 6
Defense: 14 (includes Heavy Armor feature)
Action Points: 3 per turn
Actions: Strike, Defend, Move, Shield Bash
Features: Heavy Armor (+2 Defense)
```

**Marcus (Wizard)** - controlled by Beth
```
Health: 12
Intelligence: 6
Defense: 10
Mana: 15
Action Points: 3 per turn
Actions: Magic Missile, Fire Bolt, Move
Features: None
```

### Enemy Actors

**Goblin Warrior (x2)** - Strategy: Aggressive
```
Health: 10
Strength: 3
Defense: 12
Action Points: 3 per turn
Actions: Strike, Move
```

**Goblin Archer (x1)** - Strategy: Ranged
```
Health: 8
Attack: 4
Defense: 11
Action Points: 3 per turn
Actions: Bow Shot (Range 6), Move
```

## B.3 The Encounter Begins

### Scene Introduction

*The Game Master reads the scene text:*

"After a day of travel through the Darkwood Forest, you make camp near a rocky outcropping. As night falls, Sera notices movement in the shadows. Before she can call out a warning, three goblins emerge from hiding positions."

*The scene transitions to the encounter.*

### The Map

```
  1 2 3 4 5 6 7 8
8 . . . . . . . .
7 . . . A . . . .     A = Goblin Archer
6 . . . . . . . .
5 . . G . . G . .     G = Goblin Warrior
4 . . . . . . . .
3 . . . . . . . .
2 . S . M . . . .     S = Sera, M = Marcus
1 . . . . . . . .
```

- Sera starts at 2N 2E, facing north
- Marcus starts at 2N 4E, facing north
- Goblin Warrior 1 at 5N 3E
- Goblin Warrior 2 at 5N 6E
- Goblin Archer at 7N 4E

### Deployment Phase

The players discuss positioning:

**Alex**: "I want Sera in front to protect Marcus."

**Beth**: "I'll stay back so I can use ranged spells."

Both players confirm their positions. The goblins are placed per the encounter definition.

### Initiative Phase

Each actor or cast rolls initiative (1d100, higher goes first):

- Sera: rolls 72
- Marcus: rolls 45
- Goblin Warrior 1: rolls 38
- Goblin Warrior 2: rolls 61
- Goblin Archer: rolls 55

**Initiative Order**:
1. Sera (72)
2. Goblin Warrior 2 (61)
3. Goblin Archer (55)
4. Marcus (45)
5. Goblin Warrior 1 (38)

## B.4 Round 1

### Turn 1: Sera (Alex)

**Start of Turn**: Action Points reset to 3.

**Alex**: "Sera draws her sword and moves toward the closest goblin."

**Action 1: Move** (Cost: 1 AP)
- Sera moves 3 tiles north: from 2N 2E to 5N 2E
- She is now adjacent to Goblin Warrior 1 (at 5N 3E)
- Action Points: 3 - 1 = 2

**Alex**: "She attacks the goblin."

**Action 2: Strike** (Cost: 1 AP)
- Target: Goblin Warrior 1
- Check: 1d20 + Attack (6) >= Target Defense (12)
- Alex rolls: 11. Total: 11 + 6 = 17. 17 >= 12? **Hit!**
- Damage: 1d8 + Strength (6)
- Alex rolls: 5. Total: 5 + 6 = 11 damage.
- Goblin Warrior 1 Health: 10 - 11 = 0 (clamped). **Defeated!**
- Action Points: 2 - 1 = 1

**Game Master**: "Sera's blade catches the goblin across the chest. It falls and does not rise."

*Goblin Warrior 1 is removed from the map and initiative order.*

**Alex**: "I still have 1 AP. I'll use Defend to brace for counterattack."

**Action 3: Defend** (Cost: 1 AP)
- Effect: +2 Defense until end of turn
- Sera's Defense: 14 + 2 = 16 (until end of turn)
- Action Points: 1 - 1 = 0

**End of Turn**: Sera has 0 AP. Turn ends. Defend bonus active until turn ends.

---

### Turn 2: Goblin Warrior 2 (Strategy-Controlled)

**Start of Turn**: Action Points reset to 3.

*The Game Master runs the Aggressive strategy:*

**Check Behavior 1**: "Adjacent to enemy?" - No. Sera is 4 tiles away (at 5N 2E; Goblin is at 5N 6E).

**Check Behavior 2**: "Move toward nearest enemy." - Yes.

**Action 1: Move** (Cost: 1 AP)
- Goblin moves 3 tiles toward Sera: from 5N 6E to 5N 3E
- Still not adjacent.
- Action Points: 3 - 1 = 2
- Strategy restarts from Behavior 1.

**Check Behavior 1**: "Adjacent to enemy?" - No. 1 tile away.

**Check Behavior 2**: "Move toward nearest enemy." - Yes.

**Action 2: Move** (Cost: 1 AP)
- Goblin moves 1 tile west: from 5N 3E to 5N 2E
- Sera occupies 5N 2E, so the goblin stops adjacent at 5N 3E
- Action Points: 2 - 1 = 1

**Check Behavior 1**: "Adjacent to enemy?" - Yes. Proceed to attack.

**Action 3: Strike** (Cost: 1 AP)
- Target: Sera
- Check: 1d20 + Attack (3) >= Target Defense (16, with Defend)
- GM rolls: 8. Total: 8 + 3 = 11. 11 >= 16? **Miss!**
- Action Points: 1 - 1 = 0

**End of Turn**: Goblin has 0 AP.

**Game Master**: "The goblin rushes Sera and swings wildly, but the blow glances off her raised shield."

---

### Turn 3: Goblin Archer (Strategy-Controlled)

**Start of Turn**: Action Points reset to 3.

*Running the Ranged strategy:*

**Check Behavior 1**: "Enemy adjacent?" - No.

**Check Behavior 2**: "Enemy in range?" - Range is 6. Sera is at 5N 2E, Archer at 7N 4E.
- Distance: 2 tiles north, 2 tiles west = 2 diagonal = 3 tiles (2 x 1.5 = 3). In range!

**Action 1: Bow Shot** (Cost: 1 AP)
- Target: Sera (closer, more threatening)
- Check: 1d20 + Attack (4) >= Target Defense (16)
- GM rolls: 6. Total: 6 + 4 = 10. 10 >= 16? **Miss!**
- Action Points: 3 - 1 = 2

**Action 2: Bow Shot** (Cost: 1 AP)
- Target: Sera
- GM rolls: 12. Total: 12 + 4 = 16. 16 >= 16? **Hit!**
- Damage: 1d6 = (rolls 3) = 3 damage
- Sera Health: 20 - 3 = 17
- Action Points: 2 - 1 = 1

**Action 3: Bow Shot** (Cost: 1 AP)
- Target: Sera
- GM rolls: 4. Total: 4 + 4 = 8. 8 >= 16? **Miss!**
- Action Points: 1 - 1 = 0

**End of Turn**: Goblin Archer has 0 AP.

**Game Master**: "Arrows whistle through the darkness. Most clatter off Sera's armor, but one strikes her shoulder."

---

### Turn 4: Marcus (Beth)

**Start of Turn**: Action Points reset to 3.

**Beth**: "Marcus sees Sera taking damage and needs to help. I'll target the archer since it's more dangerous at range."

**Game Master**: "The Goblin Archer is 5 tiles away from Marcus. What's your spell range?"

**Beth**: "Magic Missile has range 10, so that works."

**Action 1: Magic Missile** (Cost: 1 AP, 3 Mana)
- Target: Goblin Archer
- Check: Automatic hit (Magic Missile has no miss chance)
- Damage: 2d4 + Intelligence (6)
- Beth rolls: 3 + 2 = 5. Total: 5 + 6 = 11 damage
- Goblin Archer Health: 8 - 11 = 0 (clamped). **Defeated!**
- Mana: 15 - 3 = 12
- Action Points: 3 - 1 = 2

*Goblin Archer is removed from the map.*

**Game Master**: "Bolts of arcane energy streak from Marcus's fingertips, unerringly striking the goblin archer. It collapses without a sound."

**Beth**: "Nice! I'll save my remaining AP in case I need to react. I end my turn."

**End of Turn**: Marcus has 2 AP remaining (they will reset next turn anyway, but Beth is being cautious).

---

### Turn 5: Goblin Warrior 1

*This goblin was already defeated and removed from the initiative order.*

---

### End of Round 1

**Status Check**:
- Sera: Health 17/20, adjacent to Goblin Warrior 2
- Marcus: Health 12/12, Mana 12/15
- Goblin Warrior 2: Health 10/10
- Goblin Warrior 1: Defeated
- Goblin Archer: Defeated

**Round Counter**: Round 2 begins.

## B.5 Round 2

### Turn 1: Sera (Alex)

**Start of Turn**: Action Points reset to 3. Defend bonus from last turn expires.

**Alex**: "One goblin left. I attack it."

**Action 1: Strike** (Cost: 1 AP)
- Target: Goblin Warrior 2
- Check: 1d20 + 6 >= 12
- Alex rolls: 15. Total: 21. **Hit!**
- Damage: 1d8 + 6 = (rolls 7) = 13 damage
- Goblin Warrior 2 Health: 10 - 13 = 0 (clamped). **Defeated!**
- Action Points: 3 - 1 = 2

*Goblin Warrior 2 is removed from the map.*

**Game Master**: "Sera's sword swings in a decisive arc. The final goblin falls."

## B.6 Encounter Complete

**Victory Condition Met**: All enemies defeated.

**Game Master**: "The forest falls silent. The goblin ambush has been repelled. You take a moment to catch your breath."

**Final Status**:
- Sera: Health 17/20 (lightly wounded)
- Marcus: Health 12/12, Mana 12/15

**Scene Transition**: "After the Battle"

*The Game Master reads the victory scene text, and the campaign continues.*

## B.7 Key Rules Demonstrated

This example illustrated:

1. **Initiative Order**: Higher rolls act first (Section 10.3)
2. **Action Resolution**: The if/do/then structure (Chapter 6)
3. **Resource Tracking**: Health, AP, and Mana changes (Chapter 4)
4. **Strategy Execution**: Enemies following behavior priorities (Chapter 13)
5. **Defeat Condition**: Actors at 0 Health are removed (Section 4.10.2)
6. **Temporary Effects**: Defend bonus lasting until end of turn (Chapter 6)
7. **Range Calculation**: Diagonal distance (Section 8.6.2)
8. **Victory Condition**: Encounter ends when all enemies defeated (Section 11.7)

## B.8 What Would Happen If...

**...Sera had been reduced to 0 Health?**
She would be defeated and removed from the encounter. The encounter would continue with Marcus alone. If Marcus were also defeated, the encounter would end in player defeat.

**...the players wanted to retreat?**
If the campaign defined retreat rules (typically a Feature), they could attempt to escape. Otherwise, the encounter continues until a completion condition is met.

**...Marcus ran out of Mana?**
He could not cast spells requiring Mana. He would need to use the Move action to reposition or end his turn without acting offensively.
