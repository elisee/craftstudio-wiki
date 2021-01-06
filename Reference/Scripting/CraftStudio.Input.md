# CraftStudio.Input API

----
## CraftStudio.Input.GetAxisValue
```lua
-- Returns a number
CS.Input.GetAxisValue( --[[ axis name ]] )
```

Returns the specified axis' numerical value.

The value will be in the (-1, 1) range unless it's a mouse move value, in which case its the mouse's delta in pixels since the last frame.

Game controls can be defined in the project's Administration tab.

----
## CraftStudio.Input.IsButtonDown
```lua
-- Returns a boolean
CS.Input.IsButtonDown( --[[ button name ]] )
```

Returns true if the specified button is currently pressed, false otherwise.

Game controls can be defined in the project's Administration tab.

----
## CraftStudio.Input.WasButtonJustPressed, CraftStudio.Input.WasButtonJustReleased
```lua
-- Returns a boolean
CS.Input.WasButtonJustPressed( --[[ button name ]] )
-- Returns a boolean
CS.Input.WasButtonJustReleased( --[[ button name ]] )
```

Returns true if the specified button was pressed (or released) during the last tick (1/60th of a second), false otherwise.

----
## CraftStudio.Input.SetMouseVisible
```lua
CraftStudio.Input.SetMouseVisible( --[[ true or false ]] )
```

Defines whether the mouse cursor should be visible or not while in the game's window.

Calls to this function while the mouse is locked will be ignored.

----
## CraftStudio.Input.LockMouse
```lua
CS.Input.LockMouse()
```

Hides the mouse cursor and locks it inside the game's window. Useful for games that use the mouse for looking around like first-person shooters.

----
## CraftStudio.Input.UnlockMouse
```lua
CS.Input.UnlockMouse()
```

Unlocks the mouse after it has been locked with CraftStudio.Input.LockMouse.

----
## CraftStudio.Input.GetMousePosition
```lua
-- Returns a table
CS.Input.GetMousePosition()
```

Returns a table with properties ```.x``` and ```.y``` containing the mouse position in pixels. ```x=0``` is left, ```y=0``` is top.

You probably don't want to call this function after the mouse has been locked with ```CraftStudio.Input.LockMouse``` as the hidden mouse will be kept in the center of the window. See ```CraftStudio.Input.GetMouseDelta``` instead.


----
## CraftStudio.Input.GetMouseDelta
```lua
-- Returns a table
CS.Input.GetMouseDelta()
```

Returns a table with properties ```.x``` and ```.y``` containing the mouse offset since last frame in pixels. ```x=0``` is left, ```y=0``` is top. Positive x is right, positive y is bottom.

This function is particularly useful for implementing mouse look after calling ```CraftStudio.Input.LockMouse```.

### Example: **Basic first-person mouse look**

```lua
-- Camera script
function Behavior:Awake()
    CS.Input.LockMouse()
    self.angleX = 0
    self.angleY = 0
end

function Behavior:Update()
    local mouseDelta = CS.Input.GetMouseDelta()
    
    -- Horizontal mouse delta corresponds to a rotation around the Y axis (left / right)
    self.angleY = self.angleY - 0.2 * mouseDelta.x
    -- Vertical mouse delta corresponds to a rotation around the X axis (up / down)
    self.angleX = self.angleX - 0.2 * mouseDelta.y

    -- Prevent rotating too far up or down
    self.angleX = math.clamp( self.angleX, -45, 45 )

    self.gameObject.transform:SetLocalEulerAngles( Vector3:New( self.angleX, self.angleY, 0 ) )
end
```

----
## CraftStudio.Input.OnTextEntered
```lua
CS.Input.OnTextEntered( --[[ function to call when text is entered ]] )
```

Sets up the function to be called whenever the player enters a character through the keyboard.

Once you don't want your function to be called anymore, call ```CS.Input.OnTextEntered( nil )``` to reset the handler.

You can use ```string.byte``` to convert the character into its ASCII numerical value. This is useful for special characters like the Return key (13) or the Backspace key (8).

### Example: **Printing each character typed by the player**

```lua
CS.Input.OnTextEntered( function( character )
  local charNumber = string.byte(char)

  -- Characters from 0 to 31 are control / non-printable characters
  if charNumber >= 32 then
      print( character )
  elseif charNumber == 13 then
      print( "The Return key was pressed" )
  elseif charNumber == 8 then
      print( "The Backspace key was pressed" )
  end
end )
```