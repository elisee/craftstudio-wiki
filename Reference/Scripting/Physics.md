# Physics component API

----
## Setting the gravity

The gravity force isn't a property of each body, it's global, so you can set it using [CraftStudio.Physics.SetGravity](CraftStudio.Physics).

----
## Physics:SetBodyType
```lua
Physics:SetBodyType( --[[ body type (BodyType) ]] )
```

Sets up the body's type. Possible values:

* ```Physics.BodyType.Dynamic``` - Dynamic bodies are affected by forces (including gravity) and can be moved around

* ```Physics.BodyType.Static``` - Static bodies can't be moved and aren't affected by gravity, useful for scenery

* ```Physics.BodyType.Kinematic``` - Kinematic bodies can be moved programmatically but aren't affected by forces (useful for moving obstacles)

----
## Physics:SetupAsBox, Physics:SetupAsSphere, Physics:SetupAsCapsule, Physics:SetupAsMap
```lua
Physics:SetupAsBox( --[[ size (Vector3) ]] )
Physics:SetupAsSphere( --[[ radius (number) ]] )
Physics:SetupAsCapsule( --[[ radius (number) ]], --[[ height (number) ]] )
Physics:SetupAsMap( --[[ Map asset (MapAsset) ]], --[[ TileSet to use (optional) (TileSetAsset) ]] )
```

Sets up the body's shape.

----
## Physics:GetMass, Physics:SetMass
```lua
-- Returns the mass as a number
Physics:GetMass()
Physics:SetMass( --[[ mass (number) ]] )
```

Gets or sets the body's mass.

Only makes sense on ```Dynamic``` bodies.

----
## Physics:ApplyForce, Physics:ApplyImpulse
```lua
Physics:ApplyForce( --[[ force (Vector3) ]], --[[ relative position (Vector3) (optional) ]] )
Physics:ApplyImpulse( --[[ impulse (Vector3) ]], --[[ relative position (Vector3) (optional) ]] )
```

Applies the specified force or impulse on the body. If ''relative position'' is nil, then a central force / impulse is applied by default.

A force modifies the body's acceleration (which in turns affects the object's velocity over time).

An impulse modifies the body's velocity directly.

Only works on ```Dynamic``` bodies.

----
## Physics:ApplyTorque, Physics:ApplyTorqueImpulse
```lua
Physics:ApplyTorque( --[[ torque (Vector3) ]] )
Physics:ApplyTorqueImpulse( --[[ impulse (Vector3) ]] )
```
Applies the specified torque or torque impulse on the body. If relative position is nil, then a central force / impulse is applied by default.

A torque modifies the body's angular acceleration (which in turns affects the object's angular velocity over time).

An impulse modifies the body's angular velocity directly.

Only works on ```Dynamic``` bodies.

----
## Physics:WarpPosition, Physics:OffsetPosition
```lua
Physics:WarpPosition( --[[ position (Vector3) ]] )
Physics:OffsetPosition(  --[[ offset (Vector3) ]] )
```

Teleports or offsets the body to/by the specified position/offset. Especially useful for moving around kinematic bodies (moving platforms in a platformer, opening doors & so on)

Works on ```Dynamic``` and ```Kinematic``` bodies.

(```Physics:WarpPosition``` was previously called ```Physics:Teleport``` but has been renamed for consistency)

----
## Physics:WarpEulerAngles / Physics:WarpOrientation / Physics:OffsetEulerAngles / Physics:OffsetOrientation
```lua
Physics:WarpEulerAngles( --[[ euler Angles (Vector3) ]] )
Physics:WarpOrientation( --[[ orientation (Quaternion) ]] )
 
Physics:OffsetEulerAngles( --[[ euler Angles offset (Vector3) ]] )
Physics:OffsetOrientation( --[[ orientation offset (Quaternion) ]] )
```

```WarpEulerAngles``` / ```WarpOrientation``` sets the object's orientation.

```OffsetEulerAngles``` / ```OffsetOrientation``` applies the specified Euler angles / orientation as an offset to its current orientation.

Works on ```Dynamic``` and ```Kinematic``` bodies.

----
## Physics:GetLinearVelocity, Physics:SetLinearVelocity
```lua
-- Returns a Vector3
Physics:GetLinearVelocity()
Physics:SetLinearVelocity( --[[ velocity (Vector3) ]] )
```
Returns or sets the body's linear velocity.

Only makes sense on ```Dynamic``` bodies.

----
## Physics:GetAngularVelocity, Physics:SetAngularVelocity
```lua
-- Returns a Vector3
Physics:GetAngularVelocity()
Physics:SetAngularVelocity( --[[ velocity (Vector3) ]] )
```
Returns or sets the body's angular velocity.

Only makes sense on ```Dynamic``` bodies.

----
## Physics:SetFreezePosition, Physics:SetFreezeRotation
```lua
Physics:SetFreezePosition( --[[ x (Boolean) ]], --[[ y (Boolean) ]], --[[ z (Boolean) ]] )
Physics:SetFreezeRotation( --[[ x (Boolean) ]], --[[ y (Boolean) ]], --[[ z (Boolean) ]] )
```
Sets whether object's position / orientation is fixed around each axis.

Only makes sense on ```Dynamic``` bodies.
### Example: **Freezing an object's rotation entirely**
```lua
​self.gameObject.physics:SetFreezeRotation( true, true, true )
```

----
##Physics:GetFriction, Physics:SetFriction
```lua
-- Returns number
Physics:GetFriction()
Physics:SetFriction( --[[ friction (number) ]] )
```
Returns or sets the body's friction as a number, 0 being no friction (very slippery) and 1 being high friction (very sticky). Default friction value for newly-created bodies is 1.

----
##Physics:GetAnisotropicFriction, Physics:SetAnisotropicFriction
```lua
-- Returns Vector3
Physics:GetAnisotropicFriction()
Physics:SetAnisotropicFriction( --[[ friction (Vector3) ]] )
```
Returns or sets the body's anisotropic friction.

Anisotropic basically means "not the same on all axes". By default, anisotropic friction is disabled (friction is the same on all axes).
### Example: **No vertical friction**
```lua
-- Sets the overall friction coefficient
self.gameObject.physics:SetFriction( 0.5 )
 
 -- Disable friction on the Y axis (vertically)
self.gameObject.physics:SetAnisotropicFriction( Vector3:New( 1, 0, 1 ) )
```