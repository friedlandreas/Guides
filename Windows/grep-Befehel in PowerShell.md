Will man unter Widnows ählich wie mit **grep** unter Linux in Dateien einen String suchen kann man das in der PowerShell mittels

```console
Select-String -Pattern "Suchstring" -path *.*
```

machen.

Dabei wird bei -path die Filetypen zum durchsuchen angeben - und optional auch der Pfad. Ohne Pfadangabe wird im aktuellen Pfad gesucht :-)

Wietere Infos: https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.2
