## Actors

An **actor** is any named entity in the game—your character, enemies, objects,
or environmental elements.

Every actor has:

**Name**
Unique identifier

**Location**
Grid coordinates showing during an encounter(e.g., 3N 2E means 3 spaces North, 2 spaces East from origin)

**Heading**
Direction the actor is facing: N, NE, E, SE, S, SW, W, NW

**Radial**
Clockwise direction relative to the actor's heading. (12, [1, 2], 3, [4, 5], 6) there are only 8 directions so the diagonal directions are lumped together. Only used in campaigns where entities reference radials.

**Resources**
Numerical values tracking qualities for an actor.

**Actions**
Operations the actor can perform.

**Feature**
Features are special rules that apply to any type of entity.

