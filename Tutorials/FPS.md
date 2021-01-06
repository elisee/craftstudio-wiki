# Building a first-person shooter game

----
## What's in this tutorial

This tutorial assumes you already know how CraftStudio works overall. If this is your first game, consider [checking out the introduction](Introduction.md  ) and [starting with a more beginner-oriented tutorial](Space_shooter.md).

If you're not familiar with Lua, the textual scripting language used in CraftStudio, the [Scripting Reference](../Reference/Scripting.md) has a couple links to good starting tutorials!

We'll be building a generic single-player first-person shooter, mostly focusing on writing the player control script.

----
## Locking the mouse inside the game window

To allow the player to look around with the mouse, we'll first want to hide and lock the mouse pointer with [```CS.Input.LockMouse()```](../Reference/Scripting/CraftStudio.Input.md). We can unlock it when the player presses the escape key using ```CS.Input.UnlockMouse()``` coupled with a chcek on ```CS.Input.WasButtonJustPressed()```.

```lua
-- Script version 1: Locking & unlocking the mouse

function Behavior:Awake()
    CS.Input.LockMouse()
end

function Behavior:Update()
    -- NOTE: Make sure to define an "Escape" game button in your project's Administration tab
    if CS.Input.WasButtonJustPressed( "Escape" ) then
        CS.Input.UnlockMouse()
    end
end
```

This script should be placed on your main camera game object.

----
## Looking around

We can use the values returned by [```CS.Input.GetMouseDelta()```](../Reference/Scripting/CraftStudio.Input.md) to adjust the camera's rotation.

We'll want to lock the rotation around the X axis (for looking up/down) to a reasonable range to prevent the camera from making a full turn. This can be achieved by clamping the value with ```math.clamp( value, min, max )```.

Here's our updated camera script:

```lua
-- Script version 2: Looking around with the mouse

function Behavior:Awake()
    CS.Input.LockMouse()
    
    self.angleX = 0
    self.angleY = 0
    
    self.rotationSpeed = 0.2
end

function Behavior:Update()
    -- Allow unlocking the mouse with Escape
    if CS.Input.WasButtonJustPressed( "Escape" ) then
        CS.Input.UnlockMouse()
    end
    
    -- Rotate the camera when the mouse moves around
    local mouseDelta = CS.Input.GetMouseDelta()
    
    -- Horizontal mouse delta corresponds to a rotation around the Y axis (left / right)
    self.angleY = self.angleY - self.rotationSpeed * mouseDelta.x
    -- Vertical mouse delta corresponds to a rotation around the X axis (up / down)
    self.angleX = self.angleX - self.rotationSpeed * mouseDelta.y
    
    -- Clamp X rotation to the -45° / 45° range
    self.angleX = math.clamp( self.angleX, -45, 45 )

    self.gameObject.transform:SetLocalEulerAngles( Vector3:New( self.angleX, self.angleY, 0 ) )
end
```

----
## Moving forward / backward

In order to move around with collisions (using the physics engine), we'll need to separate the character from the camera. This will allow us to have a physics component on the character itself while the camera can look wherever it wants.

Here's what your scene setup might look like:

![Character and camera scene setup](../public/images/FPS/CharacterCameraSetup.png)

Notice that the script was moved from the camera to the character and the character's capsule body had its rotation frozen on all 3 axes.

Instead of directly modifying the character's orientation, we'll be setting the child camera game object's orientation:

```lua
-- Script version 3: Using a separate camera game object

function Behavior:Awake()
    CS.Input.LockMouse()
    
    -- ADDED: Store a reference to the camera game object
    self.cameraGO = self.gameObject:FindChild( "Camera" )
    
    self.angleX = 0
    self.angleY = 0
    
    self.rotationSpeed = 0.2
end

function Behavior:Update()
    -- Allow unlocking the mouse with Escape
    if CS.Input.WasButtonJustPressed( "Escape" ) then
        CS.Input.UnlockMouse()
    end
    
    -- Rotate the camera when the mouse moves around
    local mouseDelta = CS.Input.GetMouseDelta()
    
    self.angleY = self.angleY - self.rotationSpeed * mouseDelta.x
    self.angleX = self.angleX - self.rotationSpeed * mouseDelta.y
    self.angleX = math.clamp( self.angleX, -45, 45 )
    
    -- CHANGED: Set the camera's transform
    self.cameraGO.transform:SetLocalEulerAngles( Vector3:New( self.angleX, self.angleY, 0 ) )
end
```

Feel free to add a map with a static body component as well as various obstacles.

In order to move our character around, we'll be setting its linear velocity.

```lua
-- Script version 4: Moving forward / backward

function Behavior:Awake()
    CS.Input.LockMouse()
    
    self.cameraGO = self.gameObject:FindChild( "Camera" )
    
    self.angleX = 0
    self.angleY = 0
    
    self.rotationSpeed = 0.2
    self.walkSpeed = 2.0
end

function Behavior:Update()
    -- Allow unlocking the mouse with Escape
    if CS.Input.WasButtonJustPressed( "Escape" ) then
        CS.Input.UnlockMouse()
    end
    
    -- Rotate the camera when the mouse moves around
    local mouseDelta = CS.Input.GetMouseDelta()
    
    self.angleY = self.angleY - self.rotationSpeed * mouseDelta.x
    self.angleX = self.angleX - self.rotationSpeed * mouseDelta.y
    self.angleX = math.clamp( self.angleX, -45, 45 )
    
    self.cameraGO.transform:SetLocalEulerAngles( Vector3:New( self.angleX, self.angleY, 0 ) )
    
    -- Moving around
    
    -- Compute our new velocity based on the Vertical game control axis
    local vertical = CS.Input.GetAxisValue( "Vertical" )
    local newVelocity = Vector3:Forward() * vertical * self.walkSpeed
    
    -- We need to transform the velocity from character space to global space before applying it
    local characterOrientation = Quaternion:FromAxisAngle( Vector3:Up(), self.angleY )
    newVelocity = Vector3.Transform( newVelocity, characterOrientation )
    
    -- Keep the current Y velocity value so as to not mess with gravity
    newVelocity.y = self.gameObject.physics:GetLinearVelocity().y
    
    self.gameObject.physics:SetLinearVelocity( newVelocity )
end
```

----
## Strafing

No FPS movement is complete without the ability to move left or right, also known as [strafing](http://en.wikipedia.org/wiki/Strafing_%28gaming%29).

```lua
-- Script version 5: Moving around (now with strafing)

function Behavior:Awake()
    CS.Input.LockMouse()
    
    self.cameraGO = self.gameObject:FindChild( "Camera" )
    
    self.angleX = 0
    self.angleY = 0
    
    self.rotationSpeed = 0.2
    self.walkSpeed = 2.0
end

function Behavior:Update()
    -- Allow unlocking the mouse with Escape
    if CS.Input.WasButtonJustPressed( "Escape" ) then
        CS.Input.UnlockMouse()
    end
    
    -- Rotate the camera when the mouse moves around
    local mouseDelta = CS.Input.GetMouseDelta()
    
    self.angleY = self.angleY - self.rotationSpeed * mouseDelta.x
    self.angleX = self.angleX - self.rotationSpeed * mouseDelta.y
    self.angleX = math.clamp( self.angleX, -45, 45 )
    
    self.cameraGO.transform:SetLocalEulerAngles( Vector3:New( self.angleX, self.angleY, 0 ) )
    
    -- Moving around
    local vertical = CS.Input.GetAxisValue( "Vertical" )
    local horizontal = CS.Input.GetAxisValue( "Horizontal" )
    
    -- Walking forward / backward
    local newVelocity = Vector3:Forward() * vertical * self.walkSpeed
    -- Strafing
    newVelocity = newVelocity - Vector3:Left() * horizontal * self.walkSpeed
    
    local characterOrientation = Quaternion:FromAxisAngle( Vector3:Up(), self.angleY )
    newVelocity = Vector3.Transform( newVelocity, characterOrientation )
    newVelocity.y = self.gameObject.physics:GetLinearVelocity().y
    
    self.gameObject.physics:SetLinearVelocity( newVelocity )
end
```

----
## Jumping

(to be done)

----
## Shooting

(to be done)