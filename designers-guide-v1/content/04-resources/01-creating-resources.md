# Creating Resources

## Resource Design Principles

Resources should be:
- **Meaningful**: Impact gameplay decisions
- **Measurable**: Positive integers only
- **Clear**: Unambiguous in purpose

## Common Resource Types

### Capability Resources
Define what actors can do:
- Strength, Dexterity, Intelligence
- Skills and proficiencies

### State Resources
Track current condition:
- Health, Energy, Stamina
- Status and conditions

### Currency Resources
Tradeable or spendable:
- Gold, Materials, Food
- Action Points, Movement Points

### Counter Resources
Track uses or quantities:
- Ammunition, Charges
- Inventory counts

## Initialization Patterns

See Chapter 13 for detailed initialization rules.

## Resource Interactions

Resources can:
- Modify expressions ([Strength] + 1d6)
- Trigger features (when [Health] < 5)
- Gate actions (if [ActionPoints] >= 2)
- Change through effects ([Health] -= [Damage])

---

## See Also
- Chapter 13: Initialization Patterns
- Chapter 14: Features
- Chapter 16: Actions
