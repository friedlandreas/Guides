Manchmal kommt beim Upgraden mittels winget die Fehlermeldung:

 > **Eine andere Version dieser Anwendung ist bereits installiert.**

Man kann die alte Version beim Upgrade gleich deinstallieren :-)

```console
 winget upgrade --id Packet.Name --uninstall-previous
```
Also z.B.

```console
 winget upgrade --id cisco.webexteams --uninstall-previous
```

Alterntaiv geht auch erst deinstallieren und danach installieren:

```console
winget remove Packet.Name ; winget install Packet.Name
```

Also z.B.

```console
winget remove Cisco.WebexTeams ; winget install Cisco.WebexTeams
```
