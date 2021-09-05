Verbindet man Outlook für Mac von extern mit einem Exchange wird über den AutoDiscover-Mechanismus der Servername automatisch konfiguriert – bzw. geändert.

Problematisch ist es aber wenn hier der lokale Name des Exchange-Servers eingetragen wird – und somit keine Verbindung mehr zustande kommt.

Dieses Verhalten von Outlook kann man aber deaktiveren:

**1) Outlook öffnen**

**2) AppleScript Editor öffnen (Script Editor.app in Programme/Dienstprogramme)**

**3) folgendes Script ausführen**

```console
tell application "Microsoft Outlook"

	set background autodiscover of every exchange account to false

end tell
```

![Outlook-Script](https://github.com/friedlandreas/Guides/blob/4d21458d82fd04cf52f4df61c062bd684079604a/images/OutlookMacAutoDiscoverDisable.png)

Danach den Servernamen im Outlook nochmal auf den externen Namen setzten – jetzt sollte der Servername nicht mehr geändert werden und die Verbindung funktionieren!
