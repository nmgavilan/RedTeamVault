Sliver C2 is a powerful post-exploitation framework that can be used to establish a firm foothold on a device with an extensible interface that reminds the user of Meterpreter. It is detected out of the box by most AV solutions, as it is very popular, but it can be obfuscated and otherwise made to evade detection. 

Wiki: https://github.com/BishopFox/sliver/wiki

# Server
```shell
sliver-server # start the server
```

The server functions as a fully featured point of interaction, and it is not required to use the client at all if no multiplayer is going to be used. However, if multiple operators will need to interact with compromised hosts, multiplayer mode will need to be enabled, and configuration files will need to be generated. 

# Multiplayer
TODO: Flesh out multiplayer enable and configuration generation

# Implant Generation
TODO: Go over implants. Callback types, beacon vs session, etc

# Armory
TODO: Give more details on loading armory modules and how to use them effectively.