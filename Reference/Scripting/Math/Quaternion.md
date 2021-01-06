# Quaternion

Quaternions are mathematical objects useful for representing and interpolating game object orientations & rotations. Most of the time, you'll come across quaternions when using functions like [```Transform:GetOrientation```](../Transform.md).

A quaternion is made of 4 components (X, Y, Z and W) but those components can't be made sense of easily and you shouldn't try to modify them directly. It's best to think of quaternions as "black boxes" like matrices rather than vectors.

You can compose ("chain") rotations by multiplying quaternions together.

----
## Quaternion:New

```lua
-- Returns a Quaternion
Quaternion:New( --[[ x (Number) ]], --[[ y (Number) ]], --[[ z (Number) ]], --[[ w (Number) ]] )
```
Creates a new quaternion. This function is rarely, if ever, useful. To create a quaternion, you'll often want to use ```Quaternion:FromAxisAngle``` instead.

----
## Quaternion:Identity
```lua
-- Returns a Quaternion
Quaternion:Identity()
```

Returns an identity quaternion (x=0, y=0, z=0, w=1). It's the default orientation value for new game objects (and when used to rotate, it doesn't do anything).

----
## Quaternion:FromAxisAngle

```lua
-- Returns Quaternion
Quaternion:FromAxisAngle( --[[ axis (Vector3) ]], --[[ angle (Number) ]] )
```

Returns a quaternion which rotates by the specified angle (in degrees) around the specified axis.

----
## Quaternion:Length, Quaternion:SqrLength

```lua
-- Returns length as Number
Quaternion:Length()

-- Returns SquareLength as Number
Quaternion:SqrLength()
```

Returns the magnitude (or the square of the magnitude) of the specified quaternion

----
##Quaternion * Quaternion

Returns a new quaternion, result of the composition of the two specified quaternions

Note that order matters, A * B isn't equivalent to B * A for quaternions.

----
##Quaternion.Slerp

```lua
​Quaternion.Slerp( --[[ a (Quaternion) ]], --[[ b (Quaternion) ]], amount (Number) )
```

Do a (spherical) linear interpolation between orientation a and orientation b, by the specified amount (between 0 and 1).

### Example: **Get the orientation half-way between two orientations**

```lua
  local a = Quaternion:FromAxisAngle( Vector3:Up(), 45 )
  local b = Quaternion:FromAxisAngle( Vector3:Left(), 20 )
  
  local halfwayOrientation = Quaternion.Slerp( a, b, 0.5 )
```