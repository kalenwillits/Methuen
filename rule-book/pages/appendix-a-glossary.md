# Appendix A: Glossary

This appendix provides formal definitions for all terminology used within the Methuen framework. Terms are listed alphabetically for reference.

## A.1 Action

An **Action** is an operation that an actor performs during their turn to interact with other actors, the environment, or themselves. Actions follow a structured format with conditional logic (see Chapter 6).

## A.2 Actor

An **Actor** is any named entity that can participate in encounters. Actors possess spatial information (location, heading), resources, actions, and features. Examples include player characters, enemies, objects, and environmental elements. See Chapter 5.

## A.3 Behavior

A **Behavior** is an action that has been ranked within a strategy to deterministically produce choices for non-player actors. Behaviors include a `when` condition that determines when the behavior is satisfied and control passes to the next behavior. See Chapter 13.

## A.4 Campaign

A **Campaign** is a complete game content package that defines actors, maps, encounters, scenes, resources, and features. Campaigns use the Methuen rule set as their governing framework. See Chapter 15.

## A.5 Cast

A **Cast** is a group of actors controlled by the same player or strategy that share a single initiative value. All actors in a cast take their turns consecutively before play passes to the next cast or actor in the initiative order. See Chapter 7.

## A.6 Check

A **Check** is a boolean expression that resolves to either true or false. Checks drive deterministic two-way outcomes based on their resolution. The term "dice-check" is sometimes used interchangeably with Check. See Chapter 3.

## A.7 Choice

A **Choice** is a multiple-option selection point that may be resolved randomly or by player decision. Choices drive deterministic effects based on the selected option. See Chapter 12.

## A.8 Effect

An **Effect** is any change to the game state, including modifications to:
- Game phase
- Actor properties
- Resource values
- Map state

## A.9 Encounter

An **Encounter** is a turn-based challenge phase where actors occupy positions on a map and take sequential turns performing actions. Encounters have three phases: deployment, initiative, and turns. See Chapter 11.

## A.10 Expression

An **Expression** is a mathematical notation that combines dice rolls, resource values, and arithmetic operators to produce a non-negative integer result. The term "dice-expression" is sometimes used interchangeably with Expression. See Chapter 3 for complete notation rules.

## A.11 Feature

A **Feature** is a clearly written, unambiguous special rule that modifies how any part of a campaign operates. Features may be attached to actors, actions, tiles, regions, encounters, or the campaign as a whole. See Chapter 14.

## A.12 Global

**Global** is a scope modifier for features. A global feature applies to all applicable situations throughout the entire campaign, rather than being limited to a specific actor, encounter, or location.

## A.13 Heading

A **Heading** is the cardinal or ordinal direction an actor is facing. Valid headings are: N, NE, E, SE, S, SW, W, NW.

## A.14 Initiative

**Initiative** is a numerical measurement that determines turn order during encounters. Higher initiative values act before lower initiative values. See Chapter 10.

## A.15 Location

A **Location** is a coordinate pair that identifies the position of an actor or point on a map, relative to the map's origin. Locations are expressed using cardinal directions (e.g., `3N 2E` indicates 3 spaces north and 2 spaces east of the origin).

## A.16 Map

A **Map** is a grid-based graph that defines the spatial layout for an encounter. Maps consist of tiles, regions, and associated features and events. See Chapter 8.

## A.17 Narrative

A **Narrative** is a scene type consisting of descriptive or story-driven text that establishes context for upcoming encounters or advances the campaign story. See Chapter 12.

## A.18 Phase

A **Phase** is a distinct state of the game with its own governing rules. The primary phases are the scene phase and the encounter phase.

## A.19 Radial

A **Radial** is a directional indicator relative to an actor's current heading, using clock-face notation. Radial values are:
- 12: directly ahead (same as heading)
- 3: directly right (90 degrees clockwise)
- 6: directly behind (opposite heading)
- 9: directly left (90 degrees counter-clockwise)

Intermediate values (1-2, 4-5, 7-8, 10-11) represent diagonal directions. Radials are only used in campaigns that explicitly reference them. See Chapter 5.

## A.20 Reaction

A **Reaction** is an action that triggers during another actor's turn, interrupting the normal flow of play to resolve before continuing. See Chapter 6.

## A.21 Region

A **Region** is a named collection of tiles that share common features and/or events. Regions simplify map design by allowing features to be applied to multiple tiles simultaneously. See Chapter 8.

## A.22 Resource

A **Resource** is a named integer value that must always be zero or positive. Resources track actor capabilities, states, currencies, and counters. All actors have implicit access to all resources defined in the campaign. See Chapter 4.

## A.23 Round

A **Round** is a complete cycle through the initiative order, during which every actor takes one turn. See Chapter 11.

## A.24 Scene

A **Scene** is a game phase that occurs between encounters. Scenes may be narrative, choice-based, check-based, or any combination thereof. See Chapter 12.

## A.25 Strategy

A **Strategy** is a ranked set of behaviors that controls non-player actor decision-making. Strategies enable deterministic, automated actor control. See Chapter 13.

## A.26 Tile

A **Tile** is a single square unit of a map's grid. Each tile has a location and may have associated features and events. See Chapter 8.

## A.27 Turn

A **Turn** is the period during which a single actor (or cast) is the active participant and may perform actions. Turns consist of a start phase, action phase, and end phase. See Chapter 2 and Chapter 11.

---

## Notation Conventions

### Resource References

Resources are referenced by name in square brackets:
- `[Health]` - the Health resource of the acting actor
- `[Target Health]` - the Health resource of the target actor
- `[Strength]` - the Strength resource of the acting actor

### Dice Notation

Dice are notated as `XdY` where X is the number of dice and Y is the number of sides:
- `1d6` - roll one six-sided die
- `2d10` - roll two ten-sided dice and sum the results
- `d20` - shorthand for `1d20`

### Location Notation

Locations are expressed as distances from the origin along cardinal directions:
- `3N` - 3 spaces north of the origin
- `2E` - 2 spaces east of the origin
- `3N 2E` - 3 spaces north and 2 spaces east of the origin
- `0N 0E` or simply `origin` - the origin point

### Direction Notation

Directions use standard compass notation:
- Cardinals: N, E, S, W
- Ordinals: NE, SE, SW, NW

---

## Scope Definitions

### Campaign Scope

Elements at campaign scope persist throughout the entire campaign and affect all encounters and scenes.

### Encounter Scope

Elements at encounter scope exist only for the duration of a single encounter and are discarded when the encounter ends.

### Turn Scope

Elements at turn scope exist only for the duration of a single actor's turn and are discarded when the turn ends.

### Action Scope

Elements at action scope exist only for the duration of a single action's execution and are discarded when the action completes.
