# GameObject API

----
## GameObject.transform & co
```lua
GameObject.transform
GameObject.modelRenderer
GameObject.mapRenderer
GameObject.camera
GameObject.physics
GameObject.textRenderer
```

Those aren't functions (so you don't need to call them with parentheses), they are properties that contain the object's first component for a particular type.

As such, ```self.gameObject.modelRenderer``` is a shorthand for ```self.gameObject:GetComponent( "ModelRenderer" )```

### Example: **Printing an object's position**
```lua
function Behavior:Update()
    local pos = self.gameObject.transform:GetPosition()
    print( pos )
end
```

----
## GameObject:GetComponent
```lua
-- Returns a table
GameObject:GetComponent( --[[ component type ]] )
```

Returns the game object's (first) component of the specified type (or nil if none were found).

Valid component type strings are: "Transform", "Camera", "ModelRenderer", "MapRenderer", "ScriptedBehavior" and "Physics".

----
## GameObject:CreateComponent
```lua
-- Returns a Component
GameObject:CreateComponent( --[[ component type ]] )
```

Creates a new component. The component type can be any of: "ModelRenderer", "MapRenderer", "Camera" or "Physics".

To create scripted behaviors, use ```GameObject:CreateScriptedBehavior```

---
## GameObject:GetScriptedBehavior
```lua
-- Returns a ScriptedBehavior
GameObject:GetScriptedBehavior( --[[ Script asset ]] )
```

Returns the scripted behavior component (aka. script instance) with the specified script.

To find scripts, you can use ```CraftStudio.FindAsset```.

----
## GameObject:CreateScriptedBehavior
```lua
-- Returns a ScriptedBehavior component
GameObject:CreateScriptedBehavior( --[[ Script asset to use ]], --[[ table of property default values (optional) ]] )
```

Creates a new ScriptedBehavior component. To find scripts, you can use ```CraftStudio.FindAsset```.

You can optionally pass a table of properties to add to the newly created scripted behavior. The properties will be added to the scripted behavior's ```self``` object before Awake is called on it so it's useful for customizing a scripted behavior's initialization.

### Example: **Create a new scripted behavior on an existing object**
```lua
​local obj = CS.FindGameObject( "Some object" )
local scriptToUse = CS.FindAsset( "Some script" )

obj:CreateScriptedBehavior( scriptToUse, { Health=10, Ammo=3 } )
```

----
## GameObject:GetName, GameObject:SetName
```lua
-- Returns a string
GameObject:GetName()
GameObject:SetName( --[[ new game object's name ]] )
```

Gets or sets the game object's name.

----
## GameObject:GetParent, GameObject:SetParent
```lua
-- Returns a GameObject
GameObject:GetParent()

GameObject:SetParent( --[[ new parent GameObject ]], --[[ keep local transform (true or false) (optional) ]] )
```

Gets or sets the game object's parent. ```GetParent``` returns ```nil``` if the game object has no parent.

```SetParent``` can optionally carry over the game object's local transform instead of the global one if ```true``` is passed as the second parameter.

----
## GameObject:FindChild
```lua
GameObject:FindChild( --[[ GameObject name ]], --[[ recursive (true or false) (optional) ]] )
```

Look for a child game object with the specified name, optionally looking for all descendants instead of just immediate children.

----
## GameObject:GetChildren
```lua
-- Returns a numerically-indexed table
GameObject:GetChildren()
```

Returns the list of all direct children for the game object.

### Example: **Count direct children**
```lua
local children = self.gameObject:GetChildren()
print( self.gameObject:GetName() .. " has " .. #children .. " children" )
```

----
## GameObject:SendMessage
```lua
​GameObject:SendMessage( --[[ method name ]], --[[ data table (optional) ]] )
```

Tries to call a method with the specified name on all the scripted behaviors attached to the game object.

The data argument can be ```nil``` or a table you want the method to receive as its first (and only) argument.
If none of the scripted behaviors attached to the game object have a method matching the specified name, nothing happens.

### Example: **Sending a basic message**

Receiver script:
```lua
function Behavior:SayHi( data )
    print( "Hi " .. data.name .. "!" )
end
```

Sender script:
```lua
CS.FindGameObject( "some object" ):SendMessage( "SayHi", { name="CraftStudio" } )
```