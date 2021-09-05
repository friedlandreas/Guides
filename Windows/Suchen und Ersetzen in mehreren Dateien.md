Wenn man einen String in mehreren Dateien suchen und ersetzen will, kann man hierfür auch die Powershell verwenden 🙂

```console
get-ChildItem *.txt | Foreach-Object {Get-Content $_ | Out-String | Foreach-Object {$_.Replace(„Alter Text“,“Neuer Text“)} | Set-Content $_}
```

Hier wird im aktuellen Verzeichnis alle Dateien mit der Endung txt durchsucht und dabei der String „Alter Text“ durch den String „Neuer Text“ ersetzt.

Setzte ich öfters bei INI-Dateien und INF-Dateien für Anpassungen ein – funktioniert wunderbar!

**Achtung: Die alte Datei wird überschrieben!**
