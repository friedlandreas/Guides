Wenn auf einem Exchange ein Postfach deaktiviert oder gelöscht wird, werden diese nicht gleich als getrennte Postfächer angezeigt.
Entweder man wartet auf den internen Wartungsplan oder man startet die Erkennung der getrennten Mailboxen selber – ganz einfach mittels Shell 🙂

**Unter Exchange 2007 und 2010:**

Für alle Datenbanken:
```console
Get-MailboxDatabase | Clean-MailboxDatabase
```

Für eine spezifische Datenbank:
```console
Clean-MailboxDatabase Datenbankname
```

**Unter Exchange 2013, 2016 und 2019**

Für alle Datenbanken:
```console
Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -ne $null } | ForEach { Update-StoreMailboxState -Database $_.Database -Identity $_.MailboxGuid -Confirm:$False}
```

Für eine spezifische Datenbank
```console
Get-MailboxStatistics -Database Datenbankname | ForEach {Update-StoreMailboxState -Database $_.Database -Identity $_.MailboxGuid -Confirm:$False}
```

Jetzt muss man je nach Datenbankgröße in bisschen warten bis der Vorgang erledigt ist…

Dann kann man mit

```console
get-mailboxdatabase | get-mailboxstatistics | Where{ $_.DisconnectDate -ne $null } |fl displayName,Identity,disconnectdate,database
```

sich alle getrennten und gelöschten Postfächer anzeigen lassen 🙂
