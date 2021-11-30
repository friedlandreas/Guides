Wenn der Befehl **gpupdate** in der **CMD** ausgeführt wird, kann dies zu folgendem Fehler führen:

> Fehler bei der Verarbeitung der Gruppenrichtlinie. Es wurde versucht, registrierungsbasierte Richtlinieneinstellungen für das Gruppenrichtlinienobjekt „LocalGPO“ zu lesen…

Wenn dieser Fehler auftritt, konnte die Datei **Registry.pol** nicht aktualisiert werden. Diese Datei versteckt sich in folgendem Ordner:

```console
C:\Windows\System32\GroupPolicy\Machine\
```
Wenn man dann z.B. mit

```console
del C:\Windows\System32\GroupPolicy\Machine\Registry.pol
```

die Datei löscht und dann nochmal **gpupdate** ausführt klappt es wieder :-)
