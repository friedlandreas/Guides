Ich arbeite sehr viel im Vim – auf der Konsole ist das mein Standardeditor.

Was ich sehr oft brauche – und immer mal wieder nachschauen muss ich das Suchen und Ersetzen -> deshalb schreib ich mir das jetzt mal hier auf 🙂

Einmalig ersetzen:  
```console 
:%s/[Suchstring]/[Ersetzungsstring]/ 
```

Alle Vorkommen ersetzen:  
```console 
:%s/[Suchstring]/[Ersetzungsstring]/g 
```

Alle Vorkommen ersetzen – mit Parameter i case-insensitive (Groß- und Kleinschreibung egal):  
```console 
:%s/[Suchstring]/[Ersetzungsstring]/gi 
```

Alle Vorkommen ersetzen – mit Parameter i case-insensitive (Groß- und Kleinschreibung egal) und Parameter c für Nachfrage ob ersetzt werden soll:  
```console 
:%s/[Suchstring]/[Ersetzungsstring]/gic 
```

  
**Beispiel:**

```console 
:%s/AlterServerName/NeuerServerName/gi
```

Hier wird der String AlterServerName durch den String NeuerServerName ersetzt – egal wie AlterServerName geschrieben ist -> also auch alterservername, ALTERSERVERNAME, etc

Achtung: Da der String hier als Regulärer Ausdruck interpretiert wird, müssen reservierte Zeichen, z.B. „.“, escaped werden, indem man ihm ein „\“ voranstellt.
