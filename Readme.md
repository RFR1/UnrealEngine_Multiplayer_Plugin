# Multiplayer Plugin Setup for Unreal Engine

This plugin uses the Steam Online Subsystem for multiplayer functionality, and works with UE4.27-UE5+. 

**Note:** This plugin is offered in two version: **Steam Sockets** which is the modern and preffered option, and the legacy **Steam Net Driver** option. Use the Steam Sockets version unless you have a reason to use the old legacy option.

## Setup

First you'll need to make sure your project has these plugins enabled:
- Online Subsystem
- Online Subsystem Steam

To enable them, in your editor window click on "Edit" on the top left corner and "Plugins" in the drop down menu. 

![Screenshot](Images/Plugin_Window.png)

A plugins window should appear, search "Online Subsystem" and "Online Subsystem Steam" and ensure those plugins are enbaled. You may be prompted to restart your editor after enabling them.

![Screenshot](Images/Plugin_Enable1.png)

![Screenshot](Images/Plugin_Enable2.png)

After enabling those plugins and restarting the editor, you'll need to modify some '.ini' files in your project. Navigate to the Config folder in your project's main directory and find the 'DefaultEngine.ini' and 'DefaultGame.ini' files. 'test.ini'

Example path: [Project]/Config/DefaultEngine.ini and DefaultGame.ini'

Add the following lines to your project’s `DefaultEngine.ini` file. Note the lines specific to the plugin version you're using.

```ini
[/Script/Engine.GameEngine]

; Include these lines if using Steam Sockets, otherwise delete.
!NetDriverDefinitions=ClearArray
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/SteamSockets.SteamSocketsNetDriver",DriverClassNameFallback="OnlineSubsystemUtils.IpNetDriver")

; Include this line if using the Steam Net Driver, otherwise delete.
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/OnlineSubsystemSteam.SteamNetDriver",DriverClassNameFallback="/Script/OnlineSubsystemUtils.IpNetDriver")

[OnlineSubsystem]
DefaultPlatformService=Steam

[OnlineSubsystemSteam]
bEnabled=true
SteamDevAppId=480
bInitServerOnClient=true
bAllowP2PPacketRelay=true
P2PConnectionTimeout=90

[/Script/OnlineSubsystemSteam.SteamNetDriver]
NetConnectionClassName="OnlineSubsystemSteam.SteamNetConnection"

[OnlineSubsystemUtils]
IpNetDriverClassName="/Script/OnlineSubsystemUtils.IpNetDriver"
```

> `SteamDevAppId=480` is Steam’s test App ID. Replace it with your own Steam App ID if you have one.



Now add the following lines to your project’s `DefaultGame.ini` file.

```ini
[/Script/Engine.GameSession]
MaxPlayers=100
```

> The value for 'MaxPlayers' is set as an example, you can change it to whatever your project needs.
