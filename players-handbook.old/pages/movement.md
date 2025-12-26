### Actor Movement 
*Movement* is not directly defined in the Methuen framework and requires an
action to be defined by the campaign for actors to move at all. Some common
patterns are:
- A fixed movement system:
```
Fixed Movement
do: Move an actor 3 spaces
then: [Moves Per Turn] -= 1
```
- Resource based movement system:
```
Agile Movement
do: Move an actor [Agility] spaces
then: [Moves Per Turn] -= 1
```


*Note that diagonal distance measuring applies to movement.*
