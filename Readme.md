
--Add the lines below to your project's Engine.ini file:

[/Script/Engine.GameEngine]
### Add this line if using the steam net driver. ###
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/OnlineSubsystemSteam.SteamNetDriver",DriverClassNameFallback="/Script/OnlineSubsystemUtils.IpNetDriver")
### Add this line if using steam sockets. ###
!NetDriverDefinitions=ClearArray
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/SteamSockets.SteamSocketsNetDriver",
DriverClassNameFallback="OnlineSubsystemUtils.IpNetDriver")

[OnlineSubsystem]
DefaultPlatformService=steam

[OnlineSubsystemSteam]
bEnabled=true
SteamDevAppId=480 #Replace with your ID if you have one.
bInitServerOnClient=true
bAllowP2PPacketRelay=true
P2PConnectionTimeout=90

[/Script/OnlineSubsystemSteam.SteamNetDriver]
NetConnectionClassName="OnlineSubsystemSteam.SteamNetConnection"

[OnlineSubsystemUtils]
IpNetDriverClassName="/Script/OnlineSubsystemUtils.IpNetDriver"



--Add this line to your project's Game.ini file:

[/Script/Engine.GameSession]
MaxPlayers=100 #Set to desired value.

