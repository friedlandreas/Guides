Will man Dateien über Netzwerke (VPN, Internet) kopieren nimmt man am besten Start-BitsTransfer.

Geht super einfach:

```console
Start-BitsTransfer -Source c:\quelle\datei.xyz -Destination x:\ziel\ -Asynchronous
```

Durch -asynchronous kann man mehrer Jobs gleichzeit starten :-)
