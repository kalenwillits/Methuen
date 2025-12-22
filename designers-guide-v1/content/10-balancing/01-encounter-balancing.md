# Encounter Balancing

## Introduction to Balance

Balancing Methuen encounters requires understanding that you're designing **tactical puzzles** with deterministic outcomes. Unlike traditional RPGs with randomness smoothing imbalances, Methuen's precision means balance issues are immediately apparent.

### What "Balanced" Means in Methuen

A balanced encounter:
- Provides meaningful player choices
- Has victory achievable through skillful play
- Punishes poor tactics but allows recovery
- Creates tension without being trivial or impossible
- Rewards resource management

**Balance is NOT:**
- 50/50 win rate (players should win ~70-80% with good tactics)
- Equal power between player and enemies (asymmetric is fine)
- Removing all randomness (dice create variety)
- Making every choice equally viable (some tactics should be better)

## Difficulty Calibration

### Difficulty Spectrum

**Trivial** (Auto-Win):
- Player resources >> Enemy threat
- Victory possible with random actions
- No meaningful decisions required
- **When to use**: Tutorial encounters, story moments

**Easy** (Comfortable Win):
- Player advantage clear
- Mistakes forgiven
- Victory with average tactics
- **When to use**: Encounter 1, confidence building

**Medium** (Tactical Challenge):
- Resources roughly balanced
- Requires good tactics
- 1-2 mistakes acceptable
- **When to use**: Encounters 2-3, standard difficulty

**Hard** (Demanding):
- Enemy advantage or complex mechanics
- Requires optimal tactics
- Mistakes punished
- **When to use**: Encounter 4+, experienced players

**Brutal** (Near-Impossible):
- Significant enemy advantage
- Requires perfect execution
- 1 mistake = failure
- **When to use**: Optional challenges, hardcore mode

### Testing Difficulty

Playtest with these tactics:

**Optimal Play**: Smart positioning, resource efficiency, target prioritization
- Should win Hard encounters
- Should crush Easy/Medium encounters

**Average Play**: Some mistakes, suboptimal but reasonable choices
- Should win Easy encounters comfortably
- Should win Medium encounters with tension
- May lose Hard encounters

**Poor Play**: Ignoring mechanics, wasting resources, bad positioning
- Should lose all but Trivial encounters

## Resource Balance Guidelines

### Action Point Economy

**Standard**: 3 AP per turn per actor

**Baseline Damage**:
- 1 AP = ~1d6 damage (3.5 avg)
- 2 AP = ~2d6 or 1d6+attribute (7-10 avg)
- 3 AP = ~3d6 or 2d6+attribute (10-14 avg)

**Healing Costs More**:
- 1 AP = ~1d6-1 healing (2.5 avg)
- 2 AP = ~1d8 healing (4.5 avg)
- Reason: Healing is defensive, should be less efficient than damage

**Buffing/Debuffing**:
- +2 to single stat for 1 turn = 1 AP
- +3 to single stat for 2 turns = 2 AP
- Area buff = +1 AP cost

### Health Pools

**Players (Starting)**:
- Tank/Warrior: 2d10+Endurance+racial (avg 20-30)
- Standard: 1d20+Endurance+racial (avg 15-25)
- Glass Cannon: 1d12+Endurance+racial (avg 12-20)

**NPCs (by tier)**:
- Minion: 15-30 HP (dies in 1-2 hits)
- Standard: 30-50 HP (dies in 3-4 hits)
- Elite: 60-90 HP (requires focus fire)
- Boss: 100-150 HP (multi-phase fight)

**Rule of Thumb**: Player HP should survive 3-4 average hits. NPC HP should require 2-5 player attacks to defeat depending on tier.

### Defense Values

**Defense = Flat damage reduction**

Common values:
- No armor: Defense 0
- Light armor: Defense 1-2
- Medium armor: Defense 3-4
- Heavy armor: Defense 5-6
- Boss/Elite: Defense 6-8

**Balance Consideration**: Defense effectiveness scales with incoming damage. Against 1d6 attacks (avg 3.5), Defense 3 is ~85% reduction. Against 2d6 attacks (avg 7), Defense 3 is ~43% reduction.

**Recommendation**: Keep Defense < average incoming damage. Defense 6 vs 1d6 damage creates negative damage (problematic).

### Damage Variance

**Low Variance** (1d6, 1d8):
- Predictable outcomes
- Easier to balance
- Less dramatic moments
- Good for: Standard encounters

**Medium Variance** (2d6, 1d10):
- Balanced randomness
- Occasional high/low rolls
- Good tension
- Good for: Most encounters

**High Variance** (3d6, 1d12, 1d20):
- Swingy outcomes
- Memorable moments
- Harder to balance
- Good for: Boss abilities, critical effects

**Attribute Scaling** (+Strength, +Intellect):
- Reduces variance
- Rewards character building
- Increases power creep
- Use when: Long campaigns with progression

## Enemy Composition

### Action Economy Advantage

**Golden Rule**: Players should have slight action economy advantage.

**Example**: 1 player (3 AP) vs 2 enemies (2 AP each) = 3 vs 4 AP
- Enemy has AP advantage but players have better coordination
- Balanced if player has higher damage or HP

**Recommended Ratios** (Player AP : Enemy AP):
- Easy: 1.5 : 1 (player advantage)
- Medium: 1 : 1 (equal)
- Hard: 1 : 1.5 (enemy advantage)

### Enemy Types

Mix enemy archetypes for interesting encounters:

**All Melee Enemies**:
- Easy for ranged players
- Hard for melee players
- Becomes trivial with kiting

**All Ranged Enemies**:
- Easy for high-mobility
- Hard for slow tanks
- Becomes camping contest

**Mixed Composition** (Recommended):
- 60% melee, 40% ranged
- Forces positioning decisions
- Multiple viable strategies
- Interesting for all playstyles

**Example - Balanced 3-Enemy Composition**:
- 2× Melee Bandits (pressure close combat)
- 1× Archer Bandit (punishes static positioning)

### Elite vs Minion Enemies

**Minion Swarm** (Many weak):
- 5-8 enemies, 20-30 HP each
- Dies in 1-2 hits
- Tests area damage and target priority
- Risk: Overwhelming action economy

**Elite Force** (Few strong):
- 2-3 enemies, 60-90 HP each
- Requires sustained focus
- Tests resource management
- Risk: Grindy if too tanky

**Hybrid** (Recommended):
- 1 Elite + 3-4 Minions
- Elite is threat, minions are pressure
- Clear target priority decisions
- Best balance of challenge types

## Encounter Design Checklist

### Pre-Encounter Planning

- [ ] Define encounter goal (teach mechanic, test mastery, climax)
- [ ] Choose difficulty tier (Easy/Medium/Hard)
- [ ] Calculate total player AP available per round
- [ ] Calculate total enemy AP available per round
- [ ] Verify AP ratio matches intended difficulty

### Enemy Design

- [ ] Each enemy has clear role (damage dealer, tank, support)
- [ ] Enemy HP totals require 6-12 player attacks to clear
- [ ] Enemy damage can reduce player HP by 30-60% over encounter
- [ ] At least one enemy forces player movement
- [ ] Enemy strategies are distinct and meaningful

### Map Design

- [ ] Map size allows ~3-5 turns to close distance
- [ ] Cover/obstacles create positioning decisions
- [ ] Chokepoints exist but aren't mandatory
- [ ] Hazards/features affect tactics but aren't instant-win
- [ ] Player starting positions aren't immediately disadvantageous

### Victory Conditions

- [ ] Victory is achievable with good tactics
- [ ] Defeat is possible with poor tactics
- [ ] Multiple viable strategies exist
- [ ] Optimal strategy is discoverable but not obvious
- [ ] Time investment matches difficulty (15-60 min)

## Playtesting and Iteration

### Initial Playtest

Play both sides yourself:

**Test 1 - Optimal Player Tactics**:
- Use best positioning, target priority, resource management
- Should win Medium encounters
- Should have 40-60% resources remaining

**Test 2 - Average Player Tactics**:
- Make 1-2 suboptimal choices per round
- Should win Easy encounters
- May lose Medium+ encounters

**Test 3 - Poor Player Tactics**:
- Ignore cover, waste resources, bad positioning
- Should lose most encounters
- Verifies encounter punishes bad play

### Balance Red Flags

**If players auto-win:**
- Reduce enemy HP by 20%
- Add 1 enemy
- Improve enemy tactics
- Add environmental hazard

**If players always lose:**
- Reduce enemy damage by 15%
- Remove 1 enemy
- Increase player starting resources
- Simplify enemy tactics

**If encounter is boring (no tension):**
- Add environmental hazard
- Make enemies more aggressive
- Introduce elite enemy
- Add timer/pressure mechanic

**If encounter is frustrating (feels unfair):**
- Add more cover
- Reduce enemy advantage
- Make victory condition clearer
- Reduce punishing mechanics

### Iteration Formula

After each playtest:

1. **Identify Problem**: Why did balance feel off?
2. **Hypothesize Fix**: What's the smallest change to address it?
3. **Make ONE Change**: Resist changing multiple variables
4. **Retest**: Did it improve? Create new problems?
5. **Repeat**: Until 3 playtests feel balanced

**Example Iteration**:
- Test 1: Players stomped enemies (too easy)
- Hypothesis: Need more enemy HP
- Change: Increased enemy HP from 25 to 35
- Retest: Now balanced, but encounter takes too long
- Hypothesis: Too much HP created grind
- Change: Reduced HP to 30, added 1 more enemy
- Retest: Perfect balance, good tension

## Advanced Balance Techniques

### Damage Breakpoints

Design HP pools around breakpoint thresholds:

**Example**: Player deals 1d6+4 damage (avg 7.5, range 5-10)
- Enemy HP 10: Dies in 1-2 hits (feels fragile)
- Enemy HP 15: Dies in 2 hits usually, sometimes 3 (ideal minion)
- Enemy HP 20: Dies in 2-3 hits (durable minion)
- Enemy HP 30: Dies in 3-4 hits (standard enemy)

**Design Tip**: Set NPC HP at multiples of average player damage ± 2. This creates predictable but slightly variable kill times.

### Action Economy Compression

**Problem**: Players optimize to "nova" (burst damage) one enemy per round, reducing enemy action economy quickly.

**Solutions**:
1. **High HP Enemies**: Require multiple rounds to kill (forces sustained combat)
2. **Reinforcements**: New enemies enter mid-combat (maintains action economy)
3. **Resurrection**: Defeated enemies return (punishes focusing wrong targets)
4. **Split Objectives**: Must divide attention (can't focus fire)

**Example - Boss with Minions**:
```
Harkan (Boss): 120 HP
2× Cultists: 70 HP each

Player Strategy: Kill Cultists first (easier targets)
Counter: Cultists can sacrifice (heal boss)
Result: Players must choose between threats
```

### Rubber-Banding (Use Sparingly)

**Definition**: Mechanics that adjust difficulty based on performance.

**Acceptable**:
```
Boss Phase 2 Trigger
If Boss HP < 60 AND Ritual Power > 50: Transform (harder)
If Boss HP < 60 AND Ritual Power < 50: Summon minions (easier)
```

**Unacceptable**:
```
Dynamic Scaling (Feature)
Enemy damage = Player MaxHP / 4
```
(This removes player agency and trivializes tactics)

**Guideline**: Rubber-banding can provide different experiences based on choices, but shouldn't negate skillful play.

### Damage Mitigation Stacking

**Problem**: Multiple defense sources stack multiplicatively, becoming overpowered.

**Example**:
- Heavy Armor: +5 Defense
- Shield: +2 Defense
- Buff: +3 Defense
- Total: +10 Defense vs 2d6 damage (avg 7) = near invulnerable

**Solutions**:
1. **Cap Defense**: Maximum Defense = 6 or 8
2. **Diminishing Returns**: Defense effectiveness halves above threshold
3. **Percentage Reduction**: Defense reduces by %, not flat amount
4. **Exclusive Bonuses**: Can't stack multiple armor pieces

**Recommended**: Cap Defense at 6-8 to prevent invulnerability.

## Balance by Encounter Type

### Encounter 1 (Tutorial)

**Goal**: Teach mechanics, build confidence

**Balance Guidelines**:
- Player HP should survive entire encounter without healing
- Enemy damage: ~30% of player max HP total
- Enemy HP: 2-3 hits to defeat
- 3 enemies maximum
- No complex mechanics
- Victory: 95%+ success rate with basic tactics

**Test**: Can a brand-new player win on first attempt?

### Encounter 2-3 (Standard Challenge)

**Goal**: Apply learned skills, introduce complexity

**Balance Guidelines**:
- Player HP should need 1 heal during encounter
- Enemy damage: ~50-60% of player max HP total
- Enemy HP: 3-4 hits to defeat
- 3-4 enemies
- 1-2 new mechanics
- Victory: 70-80% success rate with good tactics

**Test**: Does optimal play feel rewarding? Does poor play lose?

### Final Encounter (Boss)

**Goal**: Test mastery, provide climax

**Balance Guidelines**:
- Player should use all resources (potions, abilities, etc.)
- Boss HP: 100-150 (requires sustained damage)
- Boss damage: Can kill player in 4-6 hits
- Minions or multi-phase design
- All previous mechanics relevant
- Victory: 60-70% success rate with excellent tactics

**Test**: Does victory feel earned? Is defeat clear and fair?

## Quick Reference: Balance Formulas

**Total Encounter Damage** (how much damage enemies will deal):
```
Enemy Count × Enemy AP per Turn × Avg Damage per AP × Expected Rounds
Example: 3 enemies × 2 AP × 4 damage × 5 rounds = 120 total damage
```

**Player Survivability** (can players survive?):
```
(Player HP + Expected Healing) should exceed Total Encounter Damage × 0.7
Example: (25 HP + 15 healing) = 40 > 120 × 0.7 = 84 ❌ Too deadly!
```

**Time to Kill Enemy**:
```
Enemy HP ÷ (Player Damage per Round)
Example: 30 HP ÷ 7.5 damage = 4 rounds to kill
```

**Encounter Length Estimate**:
```
(Total Enemy HP ÷ Total Player Damage per Round) × 1.5
Example: (90 total HP ÷ 15 player damage per round) × 1.5 = 9 rounds
```

**Sweet Spot**: 5-8 rounds for standard encounters, 10-15 rounds for bosses.

---

## See Also

- **Chapter 2**: Campaign Design Guide - Progressive complexity
- **Chapter 3**: Action Design - Balancing actions
- **Chapter 5**: NPC Strategies - Enemy behavior design
- **Chapter 7**: Map Design - Environmental balance
