# Glossary

Definitions for various words used throughout CraftStudio

----

## Server, projects and assets

The CraftStudio **server** is a piece of software that you can run on a computer to serve projects. When you start CraftStudio, a server for your own projects will automatically start on your local machine (unless you disable the auto-start in the Settings).

When you want to make a new game, [you create a new project on a server](../Tutorials/Introduction.md). A **project** has, among other things, a name, description, type (game or movie), whiteboard, members and assets.

**Assets** are models (characters / objects made of blocks), animations, maps, block sets, scenes, scripts, sounds or fonts.

----

## Scenes, game objects and components

A **scene** is a type of asset that contains a tree of game objects. Each **game object** has one or more components:

The Transform component is found on all game objects and cannot be removed. It allows them to be located in space through position, orientation and scale.

Various other game object **components** are available: Camera (for defining a view point from which the game will render something), Model / Map / Text Renderers, Scripted Behaviors, Physics and Network Sync.

----

## Variables, local, global and properties

A **variable** is a jar (containing a value) with a label (the variable's name). The variable's name can be made of any letters of the alphabet or digit but can't contain any spaces.

A **global variable** is a variable initialized at the root of a script (that is to say, outside any function or block) like so: ```variableName = value```. Such a variable is shared and can be accessed by all scripts.

A **local variable** is a variable initialized with ```local variableName = value```. Its lifetime is limited to the inside of the enclosing block (function, condition, loop, etc.) and it ceases to exist as soon as the block ends. You can define a variable as local at the root of a script, in which case it will be only accessible to this particular script.

A **property** can be added to an object of type ```table```:

```lua
myTable = {}
myTable.someProperty = value
```

In script functions whose name is prefixed by ```Behavior:```, the Scripted Behavior component currently being executed is made accessible to you as a variable named ```self``` and it's possible to add properties on it. Since each Scripted Behavior component is unique, this allows you to make reusable scripts for multiple objects.

For instance, one could add a property ```self.health``` to a scripted behavior used by all enemies in a game, and each of the enemies would then have their own independent health value.