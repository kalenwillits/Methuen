
# Strategies to Control Non-Player Actors

Strategies are ranked lists of behaviors determining what a non-player actor
does on their turn. Behaviors are written out as actions, except with a new
`when` condition check. If the `when` condition is true on a behavior, the
behavior is satisfied and the next behavior begins to run. The final behavior
in a strategy does not need a when condition because it always runs when
reached. The entire strategy from lowest priority to the last runs until there
is no way to perform the `do` part of the behavior any longer on any behavior
in the non-player actor's strategy.

