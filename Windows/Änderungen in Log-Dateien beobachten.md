Unter Linux/macOs/BSD verwende ich ja immer **tail** um Änderungen in Log-Dateien live zu verfolgen.

Unter Windows kann man das mit der Powershell tun:

```console
Get-Content logfile.log –Wait
```

![Tail Windows Powershell](https://github.com/friedlandreas/Guides/blob/3eb1288b88aac10bb37d957851f236ea34823d0c/images/TailWindowsPowershell1.png)

Man kann aber auch nach einen String darin filtern

```console
Get-Content logfile.log –Wait | where { $_ -match “Success” }
```

![Tail Windows Powershell](https://github.com/friedlandreas/Guides/blob/3eb1288b88aac10bb37d957851f236ea34823d0c/images/TailWindowsPowershell2.png)

Zwar nicht so mächtig wie **tail** – aber auch nicht schlecht 😉
