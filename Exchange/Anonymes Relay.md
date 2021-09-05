Man legt den Empfangsconnector am einfachsten per Powershell an:

```console
New-ReceiveConnector -Name “Relay” -Usage Custom -PermissionGroups AnonymousUsers -Bindings 10.20.30.1:25 -RemoteIpRanges 10.20.30.243 –TransportRole FrontEndTransport
```

Dabei ist “Relay” der Name des Connectors, AnonymousUsers die Berechtigungsgruppe auf den Connector (eben anonym), Bindings die IP-Adresse und der Port auf den der Connector “hört” und RemoteIpRanges die Geräte die senden dürfen (es können natürlich auch mehr angegeben werden). Es sollte vermeidet werden, dass ein komplettes Netz anonym mailen darf – Stichwort SPAM ;-). Durch den Bindung der Empfangsconnectors auf die Transportrolle FrontEndTransport weist man es dem für „Clientverkehr“ zuständigen Dienst bzw. Rolle zu.

Jetzt muss noch eine Berechtigung für die AnonymousUsers gesetzt werden:

Bei einem deutschen Server:

```console
Get-ReceiveConnector “Relay” | Add-ADPermission -User “NT-AUTORITÄT\ANONYMOUS-ANMELDUNG” -ExtendedRights “Ms-Exch-SMTP-Accept-Any-Recipient”
```

Bei einem englischen Server:

```console
Get-ReceiveConnector “Relay” | Add-ADPermission -User “NT AUTHORITY\ANONYMOUS LOGON” -ExtendedRights “Ms-Exch-SMTP-Accept-Any-Recipient”
```

Jetzt sollte das anonyme Mailen funtkionieren 🙂
