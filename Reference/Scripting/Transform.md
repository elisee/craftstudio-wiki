# Transform component API

----
## Transform:SetPosition, Transform:SetLocalPosition
```lua
Transform:SetPosition( --[[ position (Vector3) ]] )
Transform:SetLocalPosition( --[[ position (Vector3) ]] )
```

Sets the transform's (global or local) position.

### Example: **Set an object's position**
```lua
self.gameObject.transform:SetPosition( Vector3:New( 5, 0, 0 ) )
```

----
## Transform:SetOrientation, Transform:SetLocalOrientation
```lua
Transform:SetOrientation( --[[ orientation (Quaternion) ]] )
Transform:SetLocalOrientation( --[[ orientation (Quaternion) ]] )
```

Sets the transform's (global or local) orientation.

----
## Transform:SetEulerAngles, Transform:SetLocalEulerAngles
```lua
Transform:SetEulerAngles( --[[ angles (Vector3) ]] )
Transform:SetLocalEulerAngles( --[[ angles (Vector3) ]] )
```

Sets the transform's (global or local) orientation based on the specified euler angles in degrees.
Y is yaw, X is pitch, Z is roll, and they are applied in this order.

----
## Transform:SetLocalScale
```lua
Transform:SetLocalScale( --[[ scale (Vector3) ]] )
```

Sets the transform's local scale.

----
## Transform:GetPosition, Transform:GetLocalPosition
```lua
-- Returns a Vector3
Transform:GetPosition()
Transform:GetLocalPosition()
```
Returns the transform's (global or local) position as a ```Vector3```. ```GetLocalPosition``` returns the position relative to the game object's parent. If your game object is at the root of the scene then ```GetLocalPosition``` is equivalent to ```GetPosition```.

----
## Transform:GetOrientation, Transform:GetLocalOrientation
```lua
-- Returns a Quaternion
Transform:GetOrientation()
Transform:GetLocalOrientation()
```

Returns the transform's (global or local) orientation as a ```Quaternion```. ```GetLocalOrientation``` returns the orientation relative to the game object's parent. If your game object is at the root of the scene then ```GetLocalOrientation``` is equivalent to ```GetOrientation```.

----
## Transform:GetEulerAngles, Transform:GetLocalEulerAngles
```lua
-- Returns a Vector3
Transform:GetEulerAngles()
Transform:GetLocalEulerAngles()
```

Returns the transform's (global or local) orientation as Euler angles in degrees. The angles are packed in a ```Vector3```.

----
## Transform:GetLocalScale
```lua
-- Returns a Vector3
Transform:GetLocalScale()
```

Returns the transform's local scale as a ```Vector3```.

----
## Transform:Move, Transform:MoveLocal
```lua
Transform:Move( --[[ offset (Vector3) ]] )
Transform:MoveLocal( --[[ offset (Vector3) ]] )
```

Offsets the transform's (global or local) position by the specified value on each axis.

----
## Transform:MoveOriented
```lua
Transform:MoveOriented( --[[ offset (Vector3) ]] )
```

Moves the transform's position along the transform's oriented axes by the specified value on each axis.

----
## Transform:Rotate, Transform:RotateLocal
```lua
Transform:Rotate( --[[ rotation (Quaternion) ]] )
Transform:RotateLocal( --[[ rotation (Quaternion) ]] )
```

Rotates the transform's (global or local) orientation by the specified quaternion.

----
## Transform:RotateEulerAngles, Transform:RotateLocalEulerAngles
```lua
Transform:RotateEulerAngles( --[[ angles (Vector3) ]] )
Transform:RotateLocalEulerAngles( --[[ angles (Vector3) ]] )
```

Rotates the transform's (global or local) orientation by the specified euler angles (in degrees).
Y is yaw, X is pitch, Z is roll, and they are applied in this order.

----
## Transform:LookAt
```lua
Transform:LookAt( --[[ target (Vector3) ]] )
```

Orients the game object so that it looks at the specified target position.

### Example: **Looking at another game object**
```lua
local other = CS.FindGameObject( "some object" )
self.gameObject.transform:LookAt( other.transform:GetPosition() )
```