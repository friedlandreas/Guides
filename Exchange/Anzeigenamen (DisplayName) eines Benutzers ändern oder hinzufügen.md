Wenn man den Anzeigenamen für eines Benutzer ändern oder hinfügen will, kann dies einfach über Die Exchange Management Shell machen.

Erst sollte man sich den aktuellen Anzeigenamen anzeigen lassen:

```console
Get-Mailbox –Database “Name der Postfachdatenbank” |select Name,displayname
```

dann kann man mittels

```console
set-mailbox “Alias oder E-Mail-Adresse” –DisplayName “Neuer Anzeigename”
```

den neuen Anzeigenamen setzten.
