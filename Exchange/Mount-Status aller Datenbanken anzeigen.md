Um den Mount-Status aller Datenbanken des bzw. der Exchange-Server anzuzeigen, reicht in der Exchange-PowerShell ein

```console
Get-MailboxDatabase -Status | Sort Name | Format-Table Name, Server, Mounted
```

:-)

Quelle: https://www.alitajran.com/get-exchange-mailbox-database-mount-status-with-powershell/
