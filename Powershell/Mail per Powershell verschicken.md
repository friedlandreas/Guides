Will man per PowerShell schnell mal einen SMTP-Server testen, kann man das gute alte Send-MailMessage verwenden:

```console
$creds = get-credential

Send-MailMessage -From test@meinedomain.com -To test@externedomain.com -Subject "Test Email" -Body "Test SMTP Service from Powershell on Port 587" -SmtpServer smtp.server.test -Credential $creds -UseSsl -Port 587
```

Es wird zwar gemeckert das der Befehl obsolete ist -> zum schnellen Testen hats bei mir allerdings immer gereicht :-)
