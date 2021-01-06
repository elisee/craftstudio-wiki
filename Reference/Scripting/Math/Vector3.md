# Vector3

---
A Vector3 is an object holding a math vector (which can represent a position, a direction or an offset for instance).

Vector3s contain 3 properties x, y, z.

### Example: **Printing the Y component of a vector in the runtime report**

```lua
​local position = self.gameObject.transform:GetPosition()
print( "Y is: " .. position.y )
```

----
## Vector3:New
```lua
-- Returns Vector3
Vector3:New( --[[ x (number) ]], --[[ y (number) ]], --[[ z (number) ]] )

-- Returns Vector3
Vector3:New( --[[ xyz (number) ]] )
```

Returns a new Vector3.

----
## Vector3:Length, Vector3:SqrLength
```lua
-- Returns length as number
Vector3:Length()

-- Returns sqrLength as number
Vector3:SqrLength()
```

Returns the vector's (actual or squared) magnitude / length.

### Example: **Trimming a vector to a specific length**
```lua
local someVector = Vector3:New( 50, 20, 30 )
local maxLength = 10
 
if someVector:Length() > maxLength then
    someVector = someVector:Normalized() * maxLength
end
```

----
## Vector3:Normalize
```lua
Vector3:Normalize()
```

Normalizes the vector in place.

### Example: **Normalize a Vector**
```lua
local someVector = Vector3:New( 50, 20, 30 )
someVector:Normalize()
```

----
## Vector3:Normalized
```lua
-- Returns a new Vector3
Vector3:Normalized()
```

Returns a copy of the vector, normalized.

----
## Vector3:Add
```lua
Vector3:Add( --[[ Vector3 ]] )
```

Adds the specified vector in place.

----
## Vector3:Subtract
```lua
Vector3:Subtract( --[[ Vector3 ]] )
```

Subtracts the specified vector.

----
## Vector3.Lerp

```lua
-- Returns a new Vector3
Vector3.Lerp( --[ a (Vector3) ]], --[[ b (Vector3) ]], --[[ amount (number) ]] )
```

Return the vector resulting from the linear interpolation between vectors a and b by the specified amount.

----
## Vector3.Slerp

```lua
-- Returns a new Vector3
​Vector3.Slerp( --[ a (Vector3) ]], --[[ b (Vector3) ]], --[[ amount (number) ]] )
```

Return the vector resulting from the spherical linear interpolation between vector a and b by the specified amount.

## Vector3.Dot
```lua
-- Returns a number
Vector3.Dot( --[[ a (Vector3) ]], --[[ b (Vector3) ]] )
```

Returns the dot product of vectors a and b.

----
## Vector3.Cross
```lua
-- Returns a new Vector3
Vector3.Cross( --[[ a (Vector3) ]], --[[ b (Vector3) ]] )
```

Returns the cross product of vectors a and b.

----
##Vector3.Angle
```lua
-- Returns the angle as number
Vector3.Angle( --[[ a (Vector3) ]], --[[ b (Vector3) ]] )
```

Returns the angle in radians between the two vectors a and b.

----
##Vector3.Distance

```lua
-- Returns the distance as number
Vector3.Distance( --[[ a (Vector3) ]], --[[ b(Vector3) ]] )
```

Returns the distance between vectors a and b.

----
## Vector3.Rotate

```lua
-- Returns a new Vector3
Vector3.Rotate( --[[ vector (Vector3) ]], --[[ rotation (Quaternion) ]] )
```

Returns a new vector, result of the transformation of the specified vector by the specified rotation.

This function was previously called ```Vector3.Transform```.

----
## Vector3 * number
Returns a new vector with all components scaled by the specified number.

----
## Vector3 * Vector3
Returns a new vector whose components are equal to each component of the first vector multiplied by each component of the second vector.

----
## Vector3 / Vector3
Returns a new vector whose components are equal to each component of the first vector divided by each component of the second vector.

----
## Vector3 + Vector3
Returns a new vector whose components are equal to each component of the second vector added to those of the first vector.

----
##Vector3 - Vector3
Returns a new vector whose components are equal to each component of the second vector subtracted from those of the first vector.

----
## Vector3:Left, Vector3:Up, Vector3:Forward
```lua
-- Returns a new Vector3
Vector3:Left()

-- Returns a new Vector3
Vector3:Up()

-- Returns a new Vector3
Vector3:Forward()
```

Returns a unit vector pointing left (X=-1, Y=0, Z=0), up (X=0, Y=1, Z=0) or forward (X=0, Y=0, Z=-1).

### Example: **Getting a vector pointing forward for a particular game object**
```lua
-- Start with the absolute forward direction
local direction = Vector3:Forward()​
 
-- Rotate it to match the object's current orientation
direction = Vector3.Rotate( direction, self.gameObject.transform:GetOrientation() ) -- relative forward direction
```

----
## Vector3:UnitX, Vector3:UnitY, Vector3:UnitZ
```lua
-- Returns a new Vector3
Vector3:UnitX()

-- Returns a new Vector3
Vector3:UnitY()

-- Returns a new Vector3
Vector3:UnitZ()
```

Returns a unit vector pointing on the X, Y or Z axis.