Man braucht ja öfters mal den Hash-Wert von Dateien – am bekanntesten bestimmt der MD5 Hash bei Downloads zum Vergleichen ob die Datei auch wirklich genau die Datei ist die man geladen hat.

Das geht direkt in Powershell - super einfach:

```console
Get-FileHash Datei.dat -Algorithm MD5
```
Hier wird der MD5-Hash generiert – es können aber auch neben Hashs mit **MD5** auch mit **SHA1, SHA256, SHA384, SHA512m MACTripleDES** und **RIPEMD160** generiert werden.

Ohne den Parameter **-Algorithm MD5** generiert der Befehl übrigens **SHA256**-Hash-Werte. Den Befehl mit **| Format-List** dahinter gibt noch eine übersichtlichere Ausgabe…

![Powershell MD5-Hash](https://github.com/friedlandreas/Guides/blob/eef45bacf61a8b4189dc8ce38bc0a379deb5ed3f/images/PowershellMD5Hash.png)
