# Glossary

## A

**Action**: A structured operation with four components: (if) condition check, (do) effects when true, (then) effects that always execute, (else) effects when false. Execution order: (if) → [true: (do), false: (else)] → (then)

**Actor**: A named entity with location, heading, and resources that can perform actions

## B

**Behavior**: A decision rule for non-player actors (checks + action)

## C

**Campaign**: Collection of content definitions adhering to Methuen framework

**Cast**: Group of actors sharing initiative and turn

**Check**: A boolean condition/expression that evaluates to true or false. Can be inline or defined as a reusable component referenced with # notation

**Component**: A reusable Check or Effect that can be referenced by name using # notation (e.g., #Has ActionPoints)

## D

## E

**Effect**: An active change to game state, such as resource modification, position change, or state change. Can be inline or defined as a reusable component referenced with # notation

**Expression**: Mathematical formula combining dice, resources, and operators

## F

**Feature**: A passive rule describing how actors interact

## G

## H

**Heading**: Direction an actor is facing (N, NE, E, SE, S, SW, W, NW)

## I

**Initiative**: Turn order value determined by rolling/calculating

## L

**Location**: Actor's position on map (coordinate notation)

## M

**Map**: Grid of tiles containing spatial information

## Q

**Queue**: Ordered list for sequential selection

## R

**Radial**: Cardinal direction relative to actor's heading

**Reaction**: Action performed outside normal turn, triggered by event

**Region**: Collection of similar/related tiles

**Resource**: Named value (positive integer) tracked for actors

## S

**Strategy**: Collection of behaviors defining non-player actor decision-making

## T

**Table**: Numbered list mapping dice rolls to outcomes

**Tile**: Single grid coordinate with properties

## W

**World**: Collection of maps
