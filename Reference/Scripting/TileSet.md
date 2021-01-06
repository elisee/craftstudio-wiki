# TileSet asset API

----
## TileSet:GetTileSize
**Returns** the tile size of the tile set.

```lua
-- Returns number
TileSet:GetTileSize()
```

### Example: **Getting the tile size of a map renderer's map**

```lua
function Behavior:Awake()
    -- Get the map renderer component from the object
    local mapRndr = self.gameObject:GetComponent( "MapRenderer" )
    -- Get the map from the map renderer component
    local map = mapRndr:GetMap()
    -- Get the tile set associated with the map (we're getting there!)
    local tileSet = map:GetTileSet()
    -- Get and print the tile size
    print( tileSet:GetTileSize() )
end
```

----
## TileSet:GetBlockTypeShape
**Returns** a ```TileSet.BlockShape``` for the specified block type ID in the tile set.

```lua
-- Returns BlockShape
TileSet:GetBlockTypeShape( blocktile ID (Number) )
```

----
## TileSet.BlockShape Enumeration
This enumeration is used to describe the shape of a block. The values along with a thumbnail of what they look like is below.

Possible values:

* ```TileSet.BlockShape.Cube```

* ```TileSet.BlockShape.Pane```

* ```TileSet.BlockShape.Stairs```

* ```TileSet.BlockShape.Slope```

* ```TileSet.BlockShape.InvertedSlope```

* ```TileSet.BlockShape.HorizontalSlab```

* ```TileSet.BlockShape.VerticalSlab```

* ```TileSet.BlockShape.Post```

* ```TileSet.BlockShape.InvertedStairs```

* ```TileSet.BlockShape.StairsCorner```

* ```TileSet.BlockShape.SlopeCorner```

* ```TileSet.BlockShape.PaneCorner```