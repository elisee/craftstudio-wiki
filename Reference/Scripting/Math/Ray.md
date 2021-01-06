# Ray

----
The Ray class can be used to check for intersection of a ray with a particular model, map or plane.

----
## Ray:New

```lua
-- Returns the Ray
Ray:New( --[[ position (Vector3) ]], --[[ direction (Vector3) ]] )
```

Returns a new ray.

----
##Ray:IntersectsPlane

```lua
-- Returns number or nil
Ray:IntersectsPlane( --[[ plane (Plane) ]] )
```

Returns the distance of intersection of the ray with the specified [Plane](http://wiki.craftstud.io/Reference/Scripting/Math/Plane) (or ```nil``` if there is no intersection).

----
## Ray:IntersectsModelRenderer

```lua
-- Returns number or nil and Vector3 or nil
Ray:IntersectsModelRenderer( --[[ model renderer (ModelRenderer) ]] )
```

Returns the distance of intersection of the ray with the specified [ModelRenderer](http://wiki.craftstud.io/Reference/Scripting/ModelRenderer) (or ```nil``` if there is no intersection) and the normal of the hit face.

### Example: **Computing the hit position**

```lua
-- Setup a ray pointing forward
​local ray = Ray:New( self.gameObject.transform:GetPosition(), Vector3.Transform( Vector3:New( 0, 0, -1 ), self.gameObject.transform:GetOrientation() ) )

-- Assuming we have a model renderer component in "modelRndr", let's cast our ray
local distance = ray:IntersectsModelRenderer( modelRndr )

-- Check if we got a hit
if distance ~= nil then
    -- Compute the position of the hit using the distance and print it
    local hitPosition = ray.position + ray.direction * distance
    print( "Hit at " .. hitPosition )
end
```

----
## Ray:IntersectsMapRenderer

```lua
--returns distance, normal, hitBlockLocation and adjacentBlockLocation or all nil
Ray:IntersectsMapRenderer( --[[ map renderer (MapRenderer) ]])
```

Returns the distance of intersection of the ray with the specified [MapRenderer](http://wiki.craftstud.io/Reference/Scripting/MapRenderer) (or nil if there is no intersection). Additional return values are the normal of the hit face, and the locations in the map of the hit and adjacent map blocks.

**Warning**: If your ray is at the exact intersection of two map blocks, it will not reliably return the hit distance. As a workaround, you can try avoiding perfectly aligned rays or shooting precisely between two blocks. This should be fixed in a future update.

### Example: **Computing the hit position**

```lua
-- Setup a ray pointing forward
​local ray = Ray:New( self.gameObject.transform:GetPosition(), Vector3.Transform( Vector3:New( 0, 0, -1 ), self.gameObject.transform:GetOrientation() ) )

-- Assuming we have a map renderer component in "mapRndr", let's cast our ray
local distance, normal, blockPos, adjBlockPos = ray:IntersectsMapRenderer( mapRndr)

-- Check if we got a hit
if distance ~= nil then
    -- Compute the position of the hit using the distance and print it
    local hitPosition = ray.position + ray.direction * distance
    print( "Hit at ", hitPosition )
    print( "Hitted BlockPos ", blockPos)
end
```

----
## Ray:IntersectsTextRenderer

```lua
--returns number or nil and Vector3 or nil
Ray:IntersectsTextRenderer( --[[ text renderer (TextRenderer) ]])
```

Returns the distance of intersection of the ray with the specified [TextRenderer](http://wiki.craftstud.io/Reference/Scripting/TextRenderer) (or ```nil``` if there is no intersection) and the normal of the hit face.
