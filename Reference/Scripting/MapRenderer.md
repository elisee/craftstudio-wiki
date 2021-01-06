# MapRenderer component API

----
## MapRenderer:GetMap, MapRenderer:SetMap
```lua
-- Returns a Map
MapRenderer:GetMap()
MapRenderer:SetMap( --[[ map asset ]], --[[ replace tile set (optional, defaults to true) ]] )
```

Gets or sets the map to display. You can find a map to display with ```CraftStudio.FindAsset```.

### Example: **Set the map displayed by a map renderer**

```lua
local mapToDisplay = CS.FindAsset( "A map asset", "Map" )

local mapRndr = CS.FindGameObject( "An object with a map renderer" ).mapRenderer
mapRndr:SetMap( mapToDisplay )
```

----
## MapRenderer:GetTileSet, MapRenderer:SetTileSet
```lua
-- Returns a TileSet
MapRenderer:GetTileSet()
MapRenderer:SetTileSet( --[[ tile set asset ]] )
```

Gets or sets the tile set to use for map rendering. You can find a tile set to display with ```CraftStudio.FindAsset```.

----
## MapRenderer:GetOpacity, MapRenderer:SetOpacity
```lua
-- Returns a number
MapRenderer:GetOpacity()
MapRenderer:SetOpacity( --[[ opacity ]] )
```

Gets or sets the map renderer's opacity (between 0.0 and 1.0)

### Example: **Print a map renderer's current opacity**

```lua
local opacity = self.gameObject.mapRenderer:GetOpacity()

print( "The map renderer's opacity is: " .. opacity )
```
----
## MapRenderer:GetChunkRenderDistance, MapRenderer:SetChunkRenderDistance
```lua
-- Returns an integer
MapRenderer:GetChunkRenderDistance()
MapRenderer:SetChunkRenderDistance( --[[ number (positive integer) ]] )
```

Gets or sets the chunk render distance. The default is 4.

Increasing the render distance can use a lot of memory and decrease performance, be careful.