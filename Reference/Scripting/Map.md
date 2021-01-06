# Map asset API

----
## Map:GetBlockIDAt
**Returns** A block ID between 0-254 if a block exists at the given location (all valid block IDs are in the range 0-254), otherwise If there is no block at the given location then it will return ```Map.EmptyBlockID``` (which has a value of 255).

```lua
-- Returns number
Map:GetBlockIDAt( --[[ x (Number) ]], --[[ y (Number) ]], --[[ z (Number) ]] )
```

----
## Map:GetBlockOrientationAt
**Returns** The block orientation of the block at the specified location, otherwise if there is no block at the given location it will return ```Map.BlockOrientation.North```.

```lua
-- Returns BlockOrientation
Map:GetBlockOrientationAt( --[[ x (Number) ]], --[[ y (Number) ]], --[[ z (Number) ]] )
```

----
## Map.BlockOrientation Enumeration
This enumeration is used to define the direction a block is facing. When creating a block, each "face" of the block is assigned to a specific direction.

Possible values:

* ```Map.BlockOrientation.North```

* ```Map.BlockOrientation.East```

* ```Map.BlockOrientation.South```

* ```Map.BlockOrientation.West```

----
## Map:SetBlockAt
Sets a block's ID and block orientation at the given position on the map.

```lua
 Map:SetBlockAt( --[[ x (Number) ]], --[[ y (Number) ]], --[[ z (Number) ]], --[[ block id (Number) ]], --[[ orientation (BlockOrientation) ]] )
```

### Example: **Setting and Getting a block ID**
```lua
function Behavior:Awake()
    local map = self.gameObject:GetComponent ("MapRenderer"):GetMap()
 
    -- We set the block at 5, 5, 5 to block ID 0
    map:SetBlockAt (5, 5, 5, 0, Map.BlockOrientation.East)
 
    -- We get the block ID at 5, 5, 5 which is 0
    local blockID = map:GetBlockIDAt (5, 5, 5)
    print (blockID)
    -- Outputs: 0
end
```

----
## Map:GetPathInPackage
```GetPathInPackage``` returns the full path of a map in the form of "Folder/Sub-folder/Asset name". For an example, see ```Map.LoadFromPackage```.

```lua
-- Returns path of map
Map:GetPathInPackage()
```

----
## Map.LoadFromPackage
```LoadFromPackage``` loads a new copy of the map asset at the specified path. It's useful if you want to load a map from its original, saved state. You can destroy the new map later on by calling [CraftStudio.Destroy](CraftStudio) on it.

Loading data from the game package might involve downloading or disk access so it is an asynchronous operation: once the asset is ready, the specified function will be called back with the new asset as its only parameter.

```lua
-- Loads a map asynchronously
Map.LoadFromPackage( --[[ path of map in game package (string) ]], --[[ callback function ]] )
```

### Example: **Replacing a map with the original version in a map renderer**
```lua
function Behavior:Awake()
    -- Get the currently displayed map
    local mapRndr = self.gameObject:GetComponent( "MapRenderer" )
    local mapPath = mapRndr:GetMap():GetPathInPackage()
   
    -- Load a copy of the original version from the game package
    Map.LoadFromPackage( mapPath, function( newMap )
        -- Display the newly loaded version of the map
        mapRndr:SetMap( newMap )
    end )
end
```