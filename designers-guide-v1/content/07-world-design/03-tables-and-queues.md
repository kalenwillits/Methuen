# Tables and Queues

## Tables

Random selection tables map dice results to outcomes.

### Table Format

```
Starting Position Table (1d10)
1-2: 5N 10W
3-4: 10N 5E
5-6: 15S 3W
7-8: 8S 12E
9-10: 20N 20N
```

### Using Tables

Reference in features or actions:
```
Feature: Random Start
At setup, roll 1d10 on Starting Position table
```

## Queues

Ordered selection (like card decks).

### Queue Format

```
Event Queue (shuffle at start)
- Goblin Ambush
- Treasure Found
- Peaceful Day
- Storm
```

### Using Queues

```
Feature: Daily Event
At start of each day, draw from Event Queue
If queue empty, reshuffle
```

---

## See Also
- Chapter 2: Dice Notation
