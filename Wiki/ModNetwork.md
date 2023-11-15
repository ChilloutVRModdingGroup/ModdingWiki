## Mod Network

The mod network allows you to send info through the CVR Servers to the other users in the same instance as you. The
messages are only relayed by the server to game clients that subscribed to the mod Identifier you're sending the message
with.

For more details on implementation, see `ABI_RC.Systems.ModNetwork` class.

### Subscribing and Receiving Messages

You can use the `OnInitializeMelon()` to subscribe to the mod network. It needs and Identifier, and a handler function
that will be called when receiving messages on the chosen Identifier.

- The identifier needs to be a unique for your mod. And can be set with the types `Guid` or `string`.
- The function needs to return void and take a argument of the type `ModNetworkMessage`, which will be the message
  received.

In the following snippet we're listening a message that we know only has `1` parameter, and it is a `string`:

```cs
using ABI_RC.Systems.ModNetwork;

private static readonly Guid ModGuid = Guid.Parse("5affbc06-d288-f39b-6fd0-b54a51b86613");

private static void OnMessage(ModNetworkMessage msg) {
    msg.Read(out string readString);
    MelonLogger.Msg($"data [str]: {readString}");
}

public override void OnInitializeMelon() {
    ModNetworkManager.Subscribe(ModGuid, OnMessage);
}
```


### Sending a Message to Everyone in the Instance

In the following snippet we're sending a message (to the previously created Identifier), to everyone in the Instance.
Note we're sending a `string` here as the only parameter of the message. This needs to match with the Receiving handler.

```cs
private static void SendMsgToAll(string msg) {
    using var modMsg = new ModNetworkMessage(ModGuid);
    modMsg.Write(msg);
    modMsg.Send();
}
```

### Sending a Message to a Specific Player

We can can also target specific players in the Instance to send the message to, it takes an array of player ids in
string format. You can retrieve the players in the Instance using the class `CVRPlayerManager.Instance`

```cs
private static void SendMsgToNAK() {
    using var modMsg = new ModNetworkMessage(ModGuid, ["b3005d19-e487-bafc-70ac-76d2190d5a29"]);
    modMsg.Write("SHAKE");
    modMsg.Send();
}
```

### Multiple Message Types

The example above was made for a single type of message. Which takes a single `string` parameters. But you can also have
more complex messages, that send a bunch of arguments of different types.

You can play smart with the messages (if you need more than 1 type of message). For example you could instead have the
first parameter of the message to be the message type (an integer for example). So you'd start by calling:

```cs
msg.Read(out int msgType);
```

and now you could make some logic to handle each type of messages. For example if I had 2 different message types:

**1st type**
```cs
modMsg.Write(1);
modMsg.Write("Message of type 1");
```

**2nd type**
```cs
modMsg.Write(2);
modMsg.Write(true);
```

I would need to ensure my OnMessage could handle those two types, for example:

```cs
private static void OnMessage(ModNetworkMessage msg) {
    // All my messages have integers as first arg, so I know how to handle them
    msg.Read(out int msgType);

    if (msgType == 1) {
        // I know the second arg of the type 1 is a string
        msg.Read(out string secondArgumentForType1);
    }
    else if (msgType == 2) {
        // I know the second argument of the type 2 is a bool
        msg.Read(out bool secondArgumentForType2);
    }
}
```
