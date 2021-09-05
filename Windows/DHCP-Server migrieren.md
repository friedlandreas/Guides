Aufgabenstellung: einen DHCP-Server migrieren und die Konfiguration – inkl. Reservierungen, Optionen, etc – übernehmen.

**Lösung: Powershell!**

Auf dem **neuen Server die DHCP-Rolle installieren – aber noch nicht in der Domäne autorisieren.**

Dann auf dem **neuen Server eine Powershell öffnen** und als erstes einen Ordner erstellen

```console
mkdir c:\dhcp
```

Dann exportieren wir die Konfiguration

```console
Export-DhcpServer -ComputerName alter_DHCP_Server -Leases -File C:\dhcp\dhcpexp.xml –verbose
```

um sie anschließend direkt wieder zu importieren

```console
Import-DhcpServer –ComputerName Neuer_DHCP_Server -Leases –File C:\dhcp\dhcpexp.xml -BackupPath C:\dhcp\ –Verbose
```

Danach auf dem **alten DHCP-Server die Autorisierung aufheben und am besten noch den Dienst beenden.**

Jetzt kann falls nötig der **DHCP-Server auf dem neuen Server angepasst und anschließend autorisieren.**

Fertig 🙂
