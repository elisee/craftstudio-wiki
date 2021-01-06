# CraftStudio.Screen API

----
##CraftStudio.Screen.GetSize

```lua
-- Returns table
CraftStudio.Screen.GetSize()
```

Returns the screen / window current size in pixels as a table with x and y as the keys.

### Example: **Print the window width and height**
```lua
local windowSize = CraftStudio.Screen.GetSize()
print( "Width: " .. windowSize.x )
print( "Height: " .. windowSize.y )
```

----
## CraftStudio.Screen.SetSize
```lua
CraftStudio.Screen.SetSize( -- [[width (number) ]], --[[ height (number) ]] )
```

Sets the screen / window size in pixels.

----
##CraftStudio.Screen.SetResizable
```lua
CraftStudio.Screen.SetResizable( --[[ resizable (true or false) ]] )
```

Sets whether the window is resizable by the user when the game is running.
