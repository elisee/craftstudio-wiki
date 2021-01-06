# TextRenderer component API

----
## TextRenderer:GetFont, TextRenderer:SetFont
```lua
-- Returns a Font asset
TextRenderer:GetFont()
TextRenderer:SetFont( --[[ font asset to use ]] )
```

Gets or sets the font used by the text renderer to draw text.
You can get a font asset to use with ```CS.FindAsset( --[[ path to font asset ]], "Font" )```.

### Example: **Set the font displayed by a font renderer**

```lua
local fontToDisplay = CS.FindAsset( "A text asset", "Font" )

local textRndr = CS.FindGameObject( "An object with a text renderer" ).textRenderer
textRndr:SetFont( fontToDisplay )
```

----
## TextRenderer:GetText, TextRenderer:SetText
```lua
-- Returns a string
TextRenderer:GetText()
TextRenderer:SetText( --[[ text to display ]] )
```

Gets or sets the text to draw.

### Example: **Draw a counter**
```lua
-- Assuming we have a TextTenderer component on our object

function Behavior:Awake()
    self.counter = 0
end

​function Behavior:Update()
    self.counter = self.counter + 1
    self.gameObject.textRenderer:SetText( "Counter: " .. self.counter )
end
```

----
## TextRenderer:GetAlignment, TextRenderer:SetAlignment
```lua
-- Returns a number
TextRenderer:GetAlignment()
TextRenderer:SetAlignment( --[[ alignment ]] )
```

Gets or sets how the text should be aligned. Possible values are:

* ```TextRenderer.Alignment.Left```
* ```TextRenderer.Alignment.Center``` (default)
* ```TextRenderer.Alignment.Right```

### Example: **Change a text alignment**

```lua
local textRndr = CS.FindGameObject( "An object with a text renderer" ).textRenderer
textRndr:SetAlignment( TextRenderer.Alignment.Right )
```


----
## TextRenderer:GetTextWidth
```lua
-- Returns a number
TextRenderer:GetTextWidth( --[[ text to mesure (optional) ]] )
```

Returns the length (in scene units) of the specified text as it would be drawn by the text renderer. If you don't specify any text to measure, the current text currently displayed by the ```TextRenderer``` is used.

----
## TextRenderer:GetOpacity, TextRenderer:SetOpacity
```lua
-- Returns a number
TextRenderer:GetOpacity()
TextRenderer:SetOpacity( --[[ opacity ]] )
```

Gets or sets the text renderer's opacity (between 0.0 and 1.0) 