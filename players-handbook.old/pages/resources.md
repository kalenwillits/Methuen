## Resources

A **resource** is any value represented as a positive integer (0 or higher).

Resources measure:
- **Capabilities**: Strength, Dexterity, Intelligence
- **States**: Health, Energy, Focus
- **Currencies**: Gold, Materials, Ammunition
- **Counters**: Actions Remaining, Turns Survived

### Resource Rules

**Resources are always ≥ 0**
Cannot drop below zero. If an operation would make a resource negative, it becomes 0 instead.

**Resources are whole numbers**
No fractions. Division results are rounded down.

**Resources start at 0 by default**
Unless your campaign defines a feature that initializes the resource differently.

**All actors have access to all resources**
Your campaign defines what resources exist within the world. Every actor
implicitly has a value for every resource. But not all actors need to track
every resource if they don't use them. These untracked resources are `unkown`
until used. Then they are initialized and recorded for that actor. This is called *lazy initialization*.

**Lazy Initialization**
1. Check if your campaign defines an initialization rule for a given resource.
2. If yes, apply it (roll dice, calculate from other resources)
3. If no, the resource starts at 0
4. Record the value for the actor.

**Example**: An enemy deals damage to your Health, but you haven't initialized Health yet. Check your campaign book. It says "Health = 1d20 + Constitution". You roll 15, add your Constitution of 12, and record "Health: 27". Then subtract the damage.

### Resource Maximums

Some resources have maximum values. Campaigns define these using Features (special rules).

**Example Feature**:
```
Health Maximum
Health cannot exceed its initial rolled value
```

Common resources and features:
- Health (prevents infinite healing)
- Energy (limits resource regeneration)
- Action Points (Resets to 3 at the start of an actor's turn)

*Note that if there is a discrepancy between a campaign's feature and this text, this rule set be the superseding document.*
