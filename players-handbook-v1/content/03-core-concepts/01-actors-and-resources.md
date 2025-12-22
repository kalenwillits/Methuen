# Actors and Resources

## Actors

**Definition**: An **actor** is a named entity that exists within the game world, holds resources, and can perform actions.

### Core Properties

Every actor has:

1. **Name**: A unique identifier
2. **Location**: Position on a map (expressed as coordinates)
3. **Heading**: The direction the actor faces (N, NE, E, SE, S, SW, W, NW)
4. **Resources**: Named values that define the actor's capabilities and state. (ALL resources are available to ALL actors, resources are unknown until Initialized)
5. **Features**: Rules about that effect how the actor can be used or interacted with.
6. **Actions**: A set of actions that the actor can perform. i.e. Some categories for actions are: (Reposition, Exchange, Transform, Create, Destroy), more on that later
7. **Reactions**: Trap-like actions that can be played during other actor's turns via triggers set with features.

### Types of Actors

**Player Actors**: Controlled by human players
- Players make all decisions for their actors

**Non-Player Actors**: Controlled by predefined strategies
- Follow behavior patterns defined in the campaign
- Act according to decision trees and triggers
- Provide encounters, challenges, or environmental elements

## Resources

**Definition**: A **resource** is a named value represented as a positive integer (zero or higher).

### How Resources Work

Resources are an abstraction to measure and track anything of importance between actors. This is the key concept how how actors are measured.

It's important to understand that all actors have access to all resources within a world. However, they have lazy initialization.
So, if the world defines 100 actions, and your new character has only health  and mana written on their character sheet (initialized), they still have the other 98 resources, however their value is unknown until initialized.
Resources become Initialized when there is an attempt to use them in an expression, or when otherwise directed by the campaign.
Resources by default, are Initialized with the value of 0. But it's a well-supported pattern to initialize a resource with a dice notation expression.


Some examples of resources:
- **Capabilities**: Strength, speed, accuracy
- **States**: Health, energy, focus
- **Currencies**: Gold, materials, food
- **Counters**: Actions remaining, ammunition, uses

### Resource Rules

1. **Always Non-Negative**: Resources cannot drop below zero. Any operation that would result in a negative value sets the resource to zero instead.

2. **Integer Values Only**: Resources are whole numbers. Fractional results from calculations are floor-divided (rounded down).

3. **Initialized State**: Resources start at zero unless a campaign feature specifies an initialization rule.

4. **Universal Availability**: All actors have access to all resources defined in a campaign, though values are unique to each actor.

### Resource Maximums

Some resources have maximum values they cannot exceed. Campaigns define maximums using **Features**.

**How Maximums Work:**

Maximums are not separate resources—they're rules defined as Features that reference the resource:

```
Health Maximum (Feature)
Health cannot exceed its initial rolled value
If an effect would increase Health above this value, Health remains at maximum
```

```
Stamina Maximum (Feature)
Stamina cannot exceed its initial value of (1d10 + Endurance + racial bonus)
Regeneration stops when Stamina reaches this maximum
```

**Common Resources with Maximums:**
- **Health**: Usually capped at initial roll to prevent infinite scaling
- **Stamina**: Caps prevent endless resource regeneration
- **Magicka**: Limits magical resource pools
- **Action Points**: Often has a fixed maximum (e.g., always 3)

**Resources WITHOUT Maximums:**
- **Gold**: Can accumulate indefinitely
- **Counters**: Track totals without upper bounds (AttacksMade, DamageTaken, etc.)
- **Temporary Buffs**: Often no maximum (Defense bonuses, etc.)

**Example Maximum Feature:**
```
Stamina Maximum (Feature)
Stamina cannot exceed initial Stamina roll
Initial value: 1d10 + Endurance + racial bonus
If Stamina would increase above maximum (via rest, potion, etc.), it stays at maximum
```

**Exceeding Maximums via Items:**

Some equipment can increase a resource's maximum:

```
Before finding Enchanted Ring:
  Magicka: 14
  Magicka Maximum: 14 (from initial 1d10 roll)

After equipping Enchanted Ring of Magicka (Feature):
  Enchanted Ring of Magicka: Magicka Maximum +10
  Magicka: 14
  Magicka Maximum: 24 (14 base + 10 from ring)
```

The ring doesn't give you 10 Magicka immediately—it raises your maximum. You still need to regenerate or drink a potion to fill the new capacity.

**How to Find Maximums:**

Look in your campaign's Features section for rules about resource caps. If no maximum is defined, the resource has no upper limit.

### Lazy Initialization

Resources don't need to be recorded on a character sheet until they're first referenced. When a resource appears in gameplay:

1. Check if the campaign defines an initialization rule for that resource
2. If yes, apply the initialization (roll dice, calculate from other resources, etc.)
3. If no, the resource starts at zero
4. Record the value on the character sheet

**Example**: A player's actor hasn't tracked "Health" yet. An opponent deals damage. The player looks up Health in the campaign glossary, finds it initializes as "1d20+Constitution", rolls 15, adds their Constitution value of 12 for a total of 27, then subtracts the damage dealt.

## Campaigns and Content

**Definition**: A **campaign** is the collection of content definitions that adhere to the Methuen framework.

Campaigns define:

- Which resources exist and how they initialize
- What actions actors can perform
- How movement and initiative function
- Maps, encounters, and scenarios
- Victory and completion conditions

### Framework vs Campaign

**The Framework** (this handbook) provides:
- Core rules and mechanics
- How to structure actions, features, and effects
- Guidelines for campaign design

**The Campaign** (campaign book) provides:
- Specific resources, actions, and actors
- Maps and scenarios
- Theme and setting
- Win/loss conditions

