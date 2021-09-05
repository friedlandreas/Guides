Ein Active Directory (AD) zu pflegen und zu bereinigen ist ein stetiger Vorgang. Mit der Zeit entstehen durch ausgetauschte Computer – egal ob Clients oder Server – Leichen im AD. Denn durch das hinzufügen zu einer Arbeitsgruppe wird das Computerkonto im AD nicht automatisch gelöscht. Es wird nur deaktiviert und bleibt bestehen. Wenn man nicht sofort dran denkt bleiben diese ewig im AD stehen…

Einfach kann man diese Computerkonten mit der AD-Powershell finden und auch gleich entfernen. Hier ein paar Beispiele:

Alle deaktivierten Computerkonten, also alle Computer (Clients und Mitgliedsserver) die aus der Domäne entfernt und in eine AG hinzugefügt oder manuell deaktiviert wurden, werden mit diesem Befehl angezeigt:
```console
Search-ADAccount -AccountDisabled -ComputersOnly | Sort-Object | FT Name -A
```

Sollen die deaktivierten Computerkonten aus einer bestimmten Organisationseinheit (OU) angezeigt werden, so gilt es diesen Befehl zu verwenden:
```console
Search-ADAccount -AccountDisabled -Searchbase “OU=,DC=Domäne,DC=de” -ComputersOnly | Sort-Object | FT Name -A
```

Alle deaktivierten Computerkonten werden auf Nachfrage, nacheinander mit diesem Befehl gelöscht:
```console
Search-ADAccount -AccountDisabled -ComputersOnly | Sort-Object| Remove-ADComputer
```

Deaktivierte Computerkonten aus einer bestimmten OU werden auf Nachfrage mit diesem Befehl entfernt:
```console
Search-ADAccount -AccountDisabled -Searchbase “OU=,DC=Domäne,DC=de” -ComputersOnly | Sort-Object| Remove-ADComputer
```

Sollen alle deaktivierten Computerkonten auf einmal ohne Nachfrage gelöscht werden, so muss der Parameter „-Confirm:“ mit dem Wert „$False“ mit angegeben werden. Sprich:
```console
Search-ADAccount –AccountDisabled -ComputersOnly | Remove-ADComputer -Confirm:$False
```

Ohne Nachfrage werden die deaktivierten Computerkonten aus einer OU wie folgt gelöscht:
```console
Search-ADAccount –AccountDisabled -Searchbase “OU=,DC=Domäne,DC=de” -ComputersOnly | Remove-ADComputer -Confirm:$False
```

Alle Computer die sich seit 180 Tagen nicht am AD angemeldet haben werden mit dem folgenden Befehl angezeigt. Damit der Parameter AccountInactive verwendet werden kann, muss sich jedoch der Domänenfunktionsmodus mindestens auf der Ebene “Windows Server 2003” befinden:
```console
Search-ADAccount -AccountInactive –Timespan 180 –ComputersOnly | Sort-Object | FT Name -A
```

Möchte man sich alle Computer aus einer bestimmten OU anzeigen, die sich seit 180 Tagen nicht mehr am AD angemeldet haben, so sieht der Befehl folgendermaßen aus:
```console
Search-ADAccount -AccountInactive –Timespan 180 -Searchbase “OU=,DC=Domäne,DC=de” –ComputersOnly | Sort-Object | FT Name -A
```

Gelöscht werden die Computerkonten dann wie folgt:
```console
Search-ADAccount -AccountInactive –Timespan 180 -ComputersOnly | Remove-ADComputer -Confirm:$False
```

Aus einer bestimmten OU werden die Computerkonten so entfernt:
```console
Search-ADAccount -AccountInactive –Timespan 180 -Searchbase “OU=,DC=Domäne,DC=de” -ComputersOnly | Remove-ADComputer -Confirm:$False
```

Alle Computer die seit dem 01.01.2010 inaktiv sind und sich nicht mehr am AD angemeldet haben, werden wie folgt angezeigt:
```console
Search-ADAccount -AccountInactive -DateTime „01.01.2010“ –ComputersOnly | Sort-Object | FT Name -A
```

Alle Computer aus einer bestimmten OU, die sich seit dem 01.01.2010 nicht mehr am AD angemeldet haben, werden so angezeigt:
```console
Search-ADAccount -AccountInactive -DateTime „01.01.2010“ -Searchbase “OU=,DC=Domäne,DC=de” –ComputersOnly | Sort-Object | FT Name -A
```

Alle Computerkonten die sich seit dem 01.01.2010 nicht mehr am AD angemeldet haben, lassen sich dann mit diesem Befehl löschen:
```console
Search-ADAccount -AccountInactive -DateTime „01.01.2010“ –ComputersOnly | Remove-ADComputer -Confirm:$False
```

Die Computer einer bestimmten OU, die seit dem 01.01.2010 inaktiv sind, werden wie folgt gelöscht:
```console
Search-ADAccount -AccountInactive -DateTime „01.01.2010“ -Searchbase “OU=,DC=Domäne,DC=de” –ComputersOnly | Remove-ADComputer -Confirm:$False
```

Hoffe das hilft 🙂
