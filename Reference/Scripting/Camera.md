# Camera component API

----
## Camera:SetProjectionMode, Camera:GetProjectionMode

```lua
Camera:SetProjectionMode( --[[ projection mode (ProjectionMode) ]])

-- Returns the ProjectionMode
Camera:GetProjectionMode()
```

Sets or returns the camera projection mode. Possible values are: ```Camera.ProjectionMode.Perspective``` and ```Camera.ProjectionMode.Orthographic```.

### Example: **Change the camera projection mode**

```lua
local cameraRndr = CS.FindGameObject( "An object with a camera renderer" ).camera
cameraRndr:SetProjectionMode( Camera.ProjectionMode.Orthographic )
```

----
## Camera:SetFOV, Camera:GetFOV
```lua
​Camera:SetFOV( --[[ FOV (number) ]] )

-- Returns the Camera FOV as number
​Camera:GetFOV()
```

Sets or returns the camera's vertical angle of view (also called Field of view), in degrees. Valid values are 1° to 179°.

Only used when the camera's projection mode is ```perspective```.

----
## Camera:SetOrthographicScale, Camera:GetOrthographicScale
```lua
​Camera:SetOrthographicScale( --[[ scale (number)]] )
-- Return Scale number
Camera:GetOrthographicScale()
```

Sets or returns the camera's orthographic scale. The bigger the scale, the bigger the camera's viewing area will be.

Only used when the camera's projection mode is ```orthographic```.

----
## Camera:SetRenderViewportPosition / Camera:SetRenderViewportSize, Camera:GetRenderViewportPosition / Camera:GetRenderViewportSize
```lua
Camera:SetRenderViewportPosition( --[[ position x (number) ]], --[[ position y (number) ]] )
Camera:SetRenderViewportSize( --[[ width (number) ]], --[[ height (number) ]] )

-- Returns a table with Viewport Position 
Camera:GetRenderViewportPosition()

-- Returns a table with Viewport Size 
 Camera:GetRenderViewportSize()
```

Sets or returns the camera's render viewport position and size. This can be used to setup split-screen multiplayer.

The values are normalized, that means they should be within the 0.0 (left / top) to 1.0 (bottom / right) range.

For instance, you could have two cameras with size (1.0, 0.5). One at the top located at (0, 0) and the other one at the bottom located at (0, 0.5).

The returned tables for the getters contain two numbers stored as the ```.x``` and ```.y``` properties.

----
## Camera:CreateRay
```lua
-- Returns a Ray
Camera:CreateRay( --[[ a table with screen coordinates x,y (table) ]] )
```
Creates a Ray starting from the camera at the specified (x, y) screen coordinates and going forward.

It can be used to implement mouse picking and other similar actions. See this [raycast demo video](http://www.youtube.com/watch?v=V1nz1xnEDKY) for instance.

----
## Camera:Project
```lua
-- Returns a table
Camera:Project( --[[ position (Vector3) ]] )
```

Projects a 3D space position to a 2D screen position.

The returned table contains the projected screen coordinates stored as the ```.x``` and ```.y``` properties.

This function could be used to get the 2D screen position of a character or object with the main perspective camera and then create a ray with that screen position to render some 2D interface elements on top with a secondary orthographic camera.