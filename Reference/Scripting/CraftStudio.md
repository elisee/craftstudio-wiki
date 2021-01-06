# CraftStudio API

----
## CS shorthand for CraftStudio

Rather than typing ```CraftStudio.Something``` all the time, you can simply use ```CS.Something```, which saves on typing!

----
## CraftStudio.FindAsset
```lua
-- Returns a table
CraftStudio.FindAsset( --[[ asset path ]], --[[ asset type (optional) ]] )
```

Returns the specified asset (a sprite, model, model animation, map, tile set, scene, script or document).

The asset path of an asset looks like this: **Characters/Enemies/Gobelin**. It's the path from the root of the hierarchy to the asset, with folders separated by slashes.

You can specify the asset type if needed, to disambiguate between several assets with the same name but of different types.

### Example: **Getting an animation**
```lua
local walkAnim = CS.FindAsset( "Characters/Walk", "ModelAnimation" )
self.gameObject.modelRenderer:SetAnimation( walkAnim )
```

----
## CraftStudio.LoadScene
```lua
CraftStudio.LoadScene( --[[ Scene asset to load ]] )
```

Schedules loading the specified scene after the current tick (1/60th of a second) has completed.

When the new scene is loaded, all of the current scene's game objects will be removed.

Calling this function doesn't immediately stops the calling function. As such, you might want to add a return statement afterwards.

You can use ```CraftStudio.FindAsset``` to get a scene asset to pass to ```CraftStudio.LoadScene```.

----
## CraftStudio.AppendScene
```lua
-- Returns a GameObject or nil
CraftStudio.AppendScene( --[[ Scene asset to append ]], --[[ parent GameObject to attach to (optional) ]] )
```

Appends the specified scene to the game by instantiating all of its game objects. Contrary to ```CraftStudio.LoadScene```, this doesn't unload the current scene nor waits for the next tick: it happens right away.

You can optionally specify a parent game object which will be used as a root for adding all game objects.

You can use ```CraftStudio.FindAsset``` to get a scene asset to pass to ```CraftStudio.AppendScene```. If there is a single root object in the specified scene, then this object is returned, otherwise the return value is ```nil```.

### Example: **Appending a bullet**

```lua
local bulletPrefab = CS.FindAsset( "Prefabs/Bullet", "Scene" )

-- Assuming the bullet prefab scene contains a single root game object, it is returned for us to use
local bulletGameObject = CS.AppendScene( bulletPrefab )

-- Place the bullet on our character with some offset
bulletGameObject.transform:SetPosition( self.gameObject.transform:GetPosition() + Vector3:New(1,0,1) )
```

----
## CraftStudio.Instantiate
```lua
CraftStudio.Instantiate( --[[ New GameObject name ]], --[[ Scene to instantiate ]], --[[ parent GameObject to attach to (optional) ]] )
```

Creates a new game object with the specified name and containing a copy of the specified scene inside. You can optionally specify a parent game object for the newly-created game object.

This is useful for inserting a "preset" object / prefab into the world at runtime. For instance you could define a character made of multiple game objects and components in a separate scene and insert it into your level by calling ```CraftStudio.Instantiate```.

If you don't want a wrapper game object to be created, you can use ```CraftStudio.AppendScene``` instead.

----
## CraftStudio.FindGameObject
```lua
-- Returns the GameObject or nil if not found
CraftStudio.FindGameObject( --[[ GameObject name ]] )
```

Returns the first game object with the specified name, or ```nil``` if none is found.

----
## CraftStudio.CreateGameObject
```lua
-- Returns the newly created GameObject
CraftStudio.CreateGameObject( --[[ name ]], --[[ parent GameObject to attach to ]] )
```

Creates a new empty game object with the specified name and returns it. You can optionally specify a parent for the newly-created game object.

Once your game object is created, you can add components to it with ```GameObject:CreateComponent``` and ```GameObject:CreateScriptedBehavior```.

----
## CraftStudio.GetRootGameObjects
```lua
-- Returns a list of root game objects
CraftStudio.GetRootGameObjects()
```

Returns a list of all parentless game objects currently in the world. Combined with GameObject:GetChildren(), this can be used to recursively visit the whole game object tree.

### Example: **Displaying the name and number of children of all root game objects**

```lua
for i, rootGameObject in ipairs( CS.GetRootGameObjects() ) do
    print( rootGameObject:GetName() .. " has " .. #rootGameObject:GetChildren() .. " children" )
end
```

----
## CraftStudio.Destroy
```lua
CraftStudio.Destroy( --[[ game object, component or dynamically-loaded asset ]] )
```

Based on the type of the object passed, this function:

  * Destroys the specified game object (and all of its descendants), or
  * Removes the specified component from its game object, or
  * Unloads a dynamically-loaded asset (see ```Map.LoadFromPackage```)

----
## CraftStudio.Exit
```lua
CraftStudio.Exit()
```

Quits the game at the end of the current frame.