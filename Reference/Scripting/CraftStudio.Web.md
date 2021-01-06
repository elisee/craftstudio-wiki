# CraftStudio.Web API

----
## CraftStudio.Web.Open, CraftStudio.Web.Redirect
```lua
-- Opens the specified URL in the player's default Web browser
CraftStudio.Web.Open( --[[ URL (string) ]] )
-- Opens the specified URL in the current browser window/tab
CraftStudio.Web.Redirect( --[[ URL (string) ]] )
```

Note that ```CraftStudio.Web.Redirect``` is only available in the Web player, not in the native runtime (since it only makes sense in the context of a browser).

### Example: **Open the CraftStudio website when the player clicks**

```lua
function Behavior:Update()
    if CS.Input.WasButtonJustPressed( "Fire" ) then
        CS.Web.Open( "http://craftstud.io/" )
    end
end
```

----
## CraftStudio.Web.Get, CraftStudio.Web.Post
```lua
-- Sends a GET request
CraftStudio.Web.Get( --[[ URL (string) ]], --[[ data (table or nil) ]], --[[ response type ]], --[[ callback ]] )
-- Sends a POST request
CraftStudio.Web.Post( --[[ URL (string) ]], --[[ data (table or nil) ]], --[[ response type ]], --[[ callback ]] )
```

Sends a GET or POST request to the specified URL with the specified data. The response type can be ```CS.Web.ResponseType.Text``` (aka. string) or ```CS.Web.ResponseType.JSON``` (aka. a Lua table).

The function you passed will be called back with a potential error as its first parameter (with a value of ```nil``` if everything went right) and the data (string or table) returned by the server as its second parameter.

### Example: **Get CraftStudio news**

```lua
function Behavior:Update()
    if CS.Input.WasButtonJustPressed( "Fire" ) then
        CS.Web.Get( "http://play.craftstud.io/News.json", nil, CS.Web.ResponseType.JSON, function( error, newsItems )
            if error ~= nil then
                print( "Couldn't get news!" )
                return
            end
            
            print( "There were " .. #newsItems .. " items returned" )
        end )
    end
end
```