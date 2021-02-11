# NetworkSync component API

----
## Message delivery methods & channels

When sending a message, you can optionally specify the delivery method and channel. This might help reduce network load and make your game feel more reactive.

There are 3 possible delivery methods (prefixed by ```CS.Network.DeliveryMethod```):

* ```CS.Network.DeliveryMethod.ReliableOrdered``` : your message will be sent over and over again until its delivery is acknowledged by the other end. Any further reliable ordered messages sent on the same channel will be delayed until this one arrives first.

* ```CS.Network.DeliveryMethod.ReliableSequenced``` : your message will be sent over and over again until it, or a newer reliable sequenced message sent on the same channel, is acknowledged by the other end.

* ```CS.Network.DeliveryMethod.UnreliableSequenced``` : your message will be sent once (fire and forget) but might or might not ever arrive to some or all of its recipients. When the other end receives a message, it will ignore any older messages that might arrive later (due to network congestion). This is useful for ever-changing data like player position, which is sent all the time anyway.

There are currently at most 32 channels available for each delivery method (numbered 0 to 31).

### **Use cases**
Reliable ordered messages (the default) are useful for delivering important game info like long-duration state changes, level info, score & so on.

Reliable sequenced messages can be used when sending data that is updated often and it's okay if some of the intermediate messages are dropped.

Unreliable sequenced messages can be used for sending data that is updated often but doesn't absolutely need to arrive at all.

----
## NetworkSync.Setup

```lua
NetworkSync.Setup( --[[ id (number) ]] )
```

Sets up the network sync component's unique ID.
Must be called to be able to send or receive any messages.

### Example: **Set up a network sync ID based on a script property**
```lua
-- We'll start at 10 for instance
-- (let's imagine 1-9 are used for something else)
local FirstCharacterNetworkSyncId = 10
 
​function Behavior:Awake()
    -- Assuming the script has a property named PlayerIndex
    self.gameObject.networkSync:Setup( FirstCharacterNetworkSyncId + self.PlayerIndex )
end
```

----
## NetworkSync.SendMessageToServer

```lua
NetworkSync.SendMessageToServer( --[[ name (string) ]], --[[ data table (defaults to nil) ]], --[[ delivery method (CS.Network.DeliveryMethod, defaults to CS.Network.DeliveryMethod.ReliableOrdered) ]] , --[[ delivery channel (number, defaults to 0) ]] )
```

Sends a message to the server with the specified data.

See at the top of the page for info about delivery methods & channels.

In order to be able to receive a message, the corresponding [message handler must have been registered first](CraftStudio.Network.md).

This is a **client-side** function.

----
## NetworkSync.SendMessageToPlayers
```lua
NetworkSync.SendMessageToPlayers( --[[ name (string) ]], --[[ data table (defaults to nil) ]], --[[ recipient player ids (table, defaults to nil) ]], --[[ delivery method (CS.Network.DeliveryMethod, defaults to CS.Network.DeliveryMethod.ReliableOrdered) ]], --[[ delivery channel (number, defaults to 0) ]] )
```

Sends a message to the specified players (or all of them if no list is specified).

See at the top of the page for info about delivery methods & channels.

In order to be able to receive a message, the corresponding 
[message handler must have been registered first](CraftStudio.Network.md).

This is a **server-side** function.
