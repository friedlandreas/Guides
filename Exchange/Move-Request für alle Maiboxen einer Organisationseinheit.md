Bei Exchange-Migrationen verschiebe ich die Mailboxen der User eigentlich immer per Exchange Powershell mit dem Move-Request-Befehl.

Bei größeren Umgebungen verschiebe ich die Mailboxen gerne per Organisationseinheiten (OU). Im Active Directory sind die Benutzer eh hoffentlich schon in sinnvollen OUs strukturiert – Finanzabteilung, IT, etc. – und so kann ich hier einfach auf diese Struktur zurückgreifen.

Das geht ganz einfach über die Exchange Powershell:

```console
Get-Mailbox -OrganizationalUnit "OU=Finanzabteilung,OU=Users,DC=Domain,DC=local" | New-MoveRequest -TargetDatabase "ExchangeDB01"
```

Kurze Erklärung: Mit Get-Mailbox zeigen wir uns alle Mailboxen in der angegebenen OU an (muss im LDAP-Pfad-Format bzw. als DistinguishedName angegeben sein) und dann pipen wir es in ein New-MoveRequest mit angegebener Datenbank.

Fertig 🙂
