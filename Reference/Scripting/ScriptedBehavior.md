# ScriptedBehavior component API

A scripted behavior is a component you can add to your game objects that allows adding custom behavior to it. A scripted behavior component lets you choose which script to use.

Scripts can expose a few functions that will be called by CraftStudio at various times during the game loop . Those functions aren't meant to be called by you, but rather serve as hooks for you to make your game objects do stuff through code.

A single script can be used on many different game objects at once. Each of the Behavior functions you expose will be passed a variable named self when called, referencing the scripted behavior component.

----
## Game object properties

The scripted behavior component, passed as ```self``` to your script's Behavior functions, holds a property named ```gameObject```, which is a reference to the game object the scripted behavior is attached to. You can access it like so: ```​self.gameObject```.

The game object itself holds various properties & functions to access other components and manipulate them.
You can attach your own properties to ```self``` or ```self.gameObject``` so keep around object state (health, current status, damage, etc.) between calls to your script functions.

### Example: **Keeping track of time alive**
```lua
​function Behavior:Awake()
    self.aliveTicks = 0
end

function Behavior:Update()
    self.aliveTicks = self.aliveTicks + 1
    print( "I've been alive for " .. self.aliveTicks .. " game ticks" )
    print( "That's " .. ( self.aliveTicks / 60 ) .. " in seconds" )
end
```

----
## Behavior functions

```Behavior:Awake``` should be used to do your one-time setup (if any) and ```Behavior:Update``` will contain your script's logic as time passes by. A third function called ```Behavior:Start``` can also be added to your script. If it exists, it will be executed after all ```Awake``` functions have been executed but before the first ```Update``` of any object happens. It might come in handy when you need to initialize stuff in a specific order.

### Behavior:Awake()
```lua
function Behavior:Awake()
    -- Your initialization code
end
```

The Behavior function named ```Awake``` will be called when a game object featuring this script comes to live. Game objects can be created when a scene is loaded or on demand while the game is running.

### Behavior:Start()
```lua
function Behavior:Start()
    -- Your late initialization code
end
```

Executed once for all newly-added behaviors just before all the ```Update``` calls start.

### Behavior:Update()
```lua
function Behavior:Update()
    -- Your code which will be run 60 times a second
end
```

The function named ```Update``` will be called 60 times a second for each game object featuring this script.
