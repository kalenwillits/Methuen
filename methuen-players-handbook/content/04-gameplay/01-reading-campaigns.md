# Reading Campaign Books

## What is a Campaign Book?

A **campaign book** contains all the specific content for an Methuen game. While this handbook provides the core framework rules, the campaign book defines what you'll actually do within those rules.

### What Campaigns Define

Every campaign book specifies:

1. **Resources**: Which resources exist and how they initialize
2. **Actions**: What operations actors can perform
3. **Features**: Passive rules that modify gameplay
4. **Effects**: Active changes that alter game state
5. **Movement System**: How actors move across the map
6. **Initiative System**: How turn order is determined
7. **Maps and Scenarios**: Where gameplay takes place
8. **Completion Conditions**: How to win or complete the campaign

### Campaign Structure

Most campaign books follow this organization:

**Setup Section**:
- Required materials
- Number of players
- Actor creation instructions
- Starting scenario

**Resource Glossary**:
- Alphabetical list of all resources
- Initialization rules for each
- Special properties or triggers

**Action Reference**:
- All available actions for actors
- Action structures (if/do/then/else)
- Costs and effects

**Map and Scenario Guide**:
- Map layouts and tile properties
- Encounter descriptions
- Objective details

## Reading Resource Definitions

Resources in campaign books typically include:

### Resource Name
The identifier used in expressions and on character sheets

### Initialization Rule
How the resource's starting value is determined:

- **Fixed Value**: "Starts at 10"
- **Dice Roll**: "Roll 1d20"
- **Modified Roll**: "Roll 1d20+5"
- **Derived**: "Equal to Strength×2"
- **Conditional**: "Roll 2d6 if Noble background, else 1d6"

### Description
What the resource represents and how it's used

### Triggers or Features
Special rules activated when the resource changes

**Example Resource Entry**:

```
Health
Initialization: 1d20+Constitution
Description: Represents physical wellness. When Health reaches 0,
the actor is removed from the map.
Feature: Wounded - When Health drops below 5, movement costs double.
```

## Reading Action Definitions

Actions define what actors can do. Campaign books present actions with:

### Action Name
How the action is referenced ("Swing Axe", "Harvest Crop", "Build Wall")

### Action Structure
The if/do/then/else components:

- **if**: Condition check (boolean expression)
- **do**: Effects executed when condition is TRUE
- **then**: Effects that ALWAYS execute
- **else**: Effects executed when condition is FALSE (optional)

Actions may use **inline** components or **reference** named components with `#` notation.

### Range and Target
Who or what the action can affect

**Example Action Entry (Inline)**:

```
Harvest Crop
Range: Adjacent tile
if: Target tile is "Farmland" type AND [CropGrowth] > 5
do: Gain [Gold] equal to [CropGrowth], set tile's [CropGrowth] to 0
then: [ActionPoints] -= 1
else: (None)
```

**Example Action Entry (Referenced)**:

```
Can Harvest (Check)
Target tile is "Farmland" type AND [CropGrowth] > 5

Collect Crop (Effect)
Gain [Gold] equal to [CropGrowth], set tile's [CropGrowth] to 0

Pay Action Cost (Effect)
[ActionPoints] -= 1

Harvest Crop (Action)
Range: Adjacent tile
if: #Can Harvest
do: #Collect Crop
then: #Pay Action Cost
```

## Understanding Features vs Effects

### Features (Passive)
Rules that are always active or trigger automatically:

- "Move up to Dexterity spaces per turn"
- "Immune to fire damage"
- "Cannot enter water tiles"

### Effects (Active)
Changes that happen when triggered:

- "Deal 1d6 damage to target"
- "Move target 3 spaces North"
- "Gain 5 Gold"

**Key Difference**: Features describe ongoing rules; Effects describe specific changes.

## Using the Glossary

Most campaign books include a glossary of all terms. When you encounter an unfamiliar:

- **Resource**: Look it up to find initialization and special rules
- **Action**: Find the full if/do/then/else structure
- **Tile Type**: Learn properties and movement costs
- **Keyword**: Understand campaign-specific mechanics

## Campaign Genres

Methuen campaigns can support various genres:

### Tactical Scenarios
Focus on positioning, resource management in encounters

### Resource Management
Emphasize gathering, spending, and optimizing resources

### City Building
Construct and develop structures, manage populations

### Farming Simulators
Plant, harvest, and manage agricultural resources

**The framework remains the same—only the content changes.**

---

## See Also

- **Chapter 1**: Actors and Resources - Core framework concepts
- **Chapter 5**: Setup Phase - Creating your actor
- **Chapter 8**: Campaign Design Guide - For campaign creators
