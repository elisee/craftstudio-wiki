# CraftStudio.Physics API

----
##CraftStudio.Physics.SetGravity
```lua
CS.Physics.SetGravity( --[[ gravity direction/Strength (Vector3) ]] )
```

Sets the global gravity for all dynamic physics bodies.

The default gravity is ```Y = -10```.
### Example: **Setting the gravity**
```lua
-- Let's make everything heavier!
​CS.Physics.SetGravity( Vector3:New( 0, -50, 0 ) )
```

----
##CraftStudio.Physics.GetGravity
```lua
-- Returns the gravity as a Vector3
CS.Physics.GetGravity()
```
