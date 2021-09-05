Manchmal will man entweder eine einzelne Mailbox oder alle Mailboxen auf einem Exchange in eine PST-Datei exportieren – das geht natürlich wunderbar einfach über die Powershell 😉

Zuerst muss man dem User mit dem man die PSTs exportieren will – z.B. dem Administrator – überhaupt das Recht zum Exportieren geben:

```console
New-ManagementRoleAssignment -Role "Mailbox Import Export" -User Administrator
```

![](https://github.com/friedlandreas/Guides/blob/4486d16d16fcbb834b798409451527f82200847c/images/export-mailbox-1.png)

Danach bitte die Powershell-Konsole schließen und eine neue aufmachen.

# Einzelne Mailbox exportieren

Eine einzelne Mailbox kann mit

```console
New-MailboxExportRequest -Mailbox user -FilePath \\server\freigabe\user.pst
```

exportiert werden – hier mit dem Beispiel Administrator

```console
New-MailboxExportRequest -Mailbox Administrator -FilePath \\localhost\c$\pst\administrator.pst
```
![](https://github.com/friedlandreas/Guides/blob/4486d16d16fcbb834b798409451527f82200847c/images/export-mailbox-2.png)

# Alle Mailboxen exportieren

Will man alle Mailboxen exportieren geht das mit

```console
get-mailbox | foreach {New-MailboxExportRequest -Mailbox $_.Alias -FilePath "\\server\freigabe\$_.pst"}
```

Hier mein Beispiel:

```console
get-mailbox | foreach {New-MailboxExportRequest -Mailbox $_.Alias -FilePath "\\localhost\c$\pst\$_.pst"}
```

Das Ergebnis sieht dann so aus:

![](https://github.com/friedlandreas/Guides/blob/4486d16d16fcbb834b798409451527f82200847c/images/export-mailbox-3.png)

# Status anzeigen

Die Fortschritte bzw. den Status des Exports kann man sich mit

```console
Get-MailboxExportRequest
```

anzeigen lassen.

![](https://github.com/friedlandreas/Guides/blob/4486d16d16fcbb834b798409451527f82200847c/images/export-mailbox-4.png)

# Aufräumen

Um alle Export-Request am Exchange am Ende wieder zu löschen kann man das mit

```console
Get-MailboxExportRequest | Remove-MailboxExportRequest
```

die PST-Dateien bleiben natürlich 😉
