Will man per PowerShell auf einen Windows-DNS Einträge bearbeiten (anlegen bzw. löschen) geht das super einfach - hier am Beispiel für autodiscover.domain.de:

### DNS-Einträge löschen

```console
Remove-DnsServerResourceRecord -ZoneName "domain.de" -RRType "A" -Name "autodiscover" -RecordData "10.20.30.1"
```

### DNS-Einträge anlegen
```console
Add-DnsServerResourceRecordA -Name "autodiscover" -ZoneName "domain.de" -IPv4Address "10.20.30.1" -TimeToLive 00:01:00
```

Easy 😄

Quelle: https://docs.microsoft.com/en-us/powershell/module/dnsserver/?view=windowsserver2022-ps
