# CraftStudio.Network API

----
##Network play in CraftStudio

Networking lets you make your games work over the Internet so that they can be played together by multiple players. Although made as simple as possible, networking will likely affect most aspects of your game so it's best to build it in along with your game rather than as an afterthought.

See also [the NetworkSync component documentation](NetworkSync.md).

----
##Technical details

Networking in CraftStudio uses the UDP protocol for communication.

----
##CraftStudio.Network.Server.Start
```lua
CS.Network.Server.Start( --[[ port (number, defaults to CS.Network.DefaultPort) ]] )
```

Starts accepting connections on the specified port number (defaults to ```CS.Network.DefaultPort``` which has a value of ```4233```).

You'll need to manually connect to your server locally with ```CS.Network.Connect``` (passing "127.0.0.1" as the hostname) if you want to treat your local game as just another network player.

This is a **server-side** function.

----
##CraftStudio.Network.Server.Stop
```lua
CS.Network.Server.Stop()
```

Disconnects all players and stops listening to incoming connections.

This is a **server-side** function.

----
## CraftStudio.Network.Connect
```lua
CS.Network.Connect( --[[ hostname (String) ]] , --[[ port (Number) (Default CS.Network.DefaultPort) ]], --[[ callback (Function) (Default nil) )
```

Opens a connection to the specified hostname (or IP) on the specified port number.

When the connection has been established, the specified callback function will be called.

This is a **client-side** function.

----
## CraftStudio.Network.Disconnect
```lua
CS.Network.Disconnect()
```

Closes any open connection.

This won't call your OnDisconnected handler.

This is a **client-side** function.

----
## CraftStudio.Network.OnDisconnected
```lua
CS.Network.OnDisconnected( --[[ callback (Function) ]] )
```

Defines which function to call (if any) when a disconnection happens. You can pass ```nil``` to disable it.

This is a **client-side** function.

----
## CraftStudio.Network.Server.OnPlayerJoined

```lua
CS.Network.Server.OnPlayerJoined( --[[ callback (function) ]] )
```

Defines which function to call (if any) when a player has joined. You can pass nil to disable it.

The callback will be passed a table containing player info with the following keys:

* ```id```: a unique ID attributed to this player

* ```name```: the player's name (alphanumeric). Currently always an empty string.

* ```authenticated```: a boolean stating whether the player is authenticated against the master server or not. Currently always false.

This is a **server-side** function.

### Example: **Printing the player's ID when they join**

```lua
function PlayerJoinHandler( player )
    print( "Player with ID " .. player.id .. " has joined!" )
end
```

----
## CraftStudio.Network.Server.OnPlayerLeft

```lua
CS.Network.Server.OnPlayerLeft( --[[ callback (function) ]] )
```

Defines which function to call (if any) when a player has left (or been disconnected). You can pass ```nil``` to disable it.

The callback will be passed the disconnected player's ID.

This is a **server-side** function.

### Example: **Printing the player's ID when they leave**

```lua
​function PlayerLeftHandler( playerId )
    print( "Player with ID " .. playerId .. " has left!" )
end
```

----
## CraftStudio.Network.Server.DisconnectPlayer

```lua
CS.Network.Server.DisconnectPlayer( --[[ playerId (Number) ]], --[[ reason (String) (Default "") ]] )
```

Disconnects the specified player, optionally specifying a reason as text that will be passed to the player's OnDisconnected handler.

This is a **server-side** function.

----
## CraftStudio.Network.RegisterMessageHandler

```lua
CS.Network.RegisterMessageHandler( --[[ handler (function) ]], --[[ side (CS.Network.MessageSide) ]] )
```

Registers a function as callable on the players (client-side) or the server (server-side). Message handler functions must be registered before they can be used to respond to messages.

Possible values for the second parameter are ```CS.Network.MessageSide.Server```, ```CS.Network.MessageSide.Players``` or ```CS.Network.MessageSide.Any```.

### Example: **Registering a server message handler**
```lua
​function Behavior:DoSomethingFun( data, playerId )
    print( "Got a DoSomethingFun message from player with ID " .. playerId )
end
CS.Network.RegisterMessageHandler( Behavior.DoSomethingFun, CS.Network.MessageSide.Players )
```