# Engine Overview

----
## Game loop

The game loop is the repeating chain of events that runs your game.

A few things to consider:

  * Currently, the game loop walks through the game object tree depth-first and updates each component of each object in the order they were created. It might make more sense to update all components and scripts of the same type together, both for performance (better cache coherence) and consistency reasons.
  * The ```Behavior:Update()``` function is called 60 times a second and the game loop will try to catch up by skipping rendering and doing updates several times in a row if the game is laggy. It might make sense to add a ```Behavior:LazyUpdate()``` called as often as possible with the elapsed time as an argument.

----
## Asset loading

Currently, all of your game package's assets will be loaded in memory when the game starts. It would probably make sense to support lazily loading some / most assets.