Manchmal kommt beim Upgraden mittels winget die Fehlermeldung:

 > **Eine andere Version dieser Anwendung ist bereits installiert.**

Das kann man fixen indem man das Packet erst deinstalliert und gleich wieder installiert :-)

```console
winget uninstall Packet.Name ; winget install Packet.Name
```
Also z.B.

```console
winget uninstall Cisco.WebexTeams ; winget install Cisco.WebexTeams
```
![winget uninstall - install - one command](https://github.com/friedlandreas/Guides/blob/34a7dcebdffac6200f61f0b781d11a9f8d9dea3f/images/winget-uninstall-install-one-command.PNG)
