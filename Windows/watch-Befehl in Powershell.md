Unter Linux gibt es ja den **watch**-Befehl mit dem man einen Befehl alle x Sekunden wiederholen kann. Unter der Windows PowerShell gibts sowas leider standardmäßig nicht – aber man kann den Befehl mit Boardmitteln nachbauen:

```console
while ($true) {Clear-Host; gci; sleep 15}
```

![Powershell watch](https://github.com/friedlandreas/Guides/blob/7299b27c78cc9d2b73f96a3e7a64bffe1af33c54/images/powershell-watch-gci-befehl.png)

In diesem Beispiel wird zuerst mit Clear-Host die aktuelle Anezige der PowerShell gelöscht, dann gci ausgeführt und zum Schluss 15 Sekunden gewartet. Danach wiederholt sich das ganze bis man es mit **STRG-C** abbricht.

![Powershell watch](https://github.com/friedlandreas/Guides/blob/7299b27c78cc9d2b73f96a3e7a64bffe1af33c54/images/powershell-watch-gci-1.png)

der Befehl lässt sich natürlich durch fast jeden anderen Befehl ersetzten 😉

Das ganze lässt sich gut für z.B. anzeigen von Verschiebeanforderungen bei Exchange benutzen:

```console
while ($true) {Clear-Host; get-moverequest; sleep 15}
```

man kann auch Befehle kombinieren – z.B. das Datum anzeigen und etwas pingen

```console
while ($true) {Clear-Host; date; ping 9.9.9.9; sleep 15}
```

![Powershell watch](https://github.com/friedlandreas/Guides/blob/7299b27c78cc9d2b73f96a3e7a64bffe1af33c54/images/powershell-watch-ping.png)
