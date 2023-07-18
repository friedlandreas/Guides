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
