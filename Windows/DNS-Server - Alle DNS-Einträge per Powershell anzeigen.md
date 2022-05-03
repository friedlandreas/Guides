Wenn man bei einem Windows-DNS mal alle DNS-Zonen inkl. Einträge anzeigen lassen will geht das wunderbar mit Powershell :-)

Lokaler DNS-Server:

```console
$Zones = @(Get-DnsServerZone)
ForEach ($Zone in $Zones) {
	Write-Host "`n$($Zone.ZoneName)" -ForegroundColor "Green"
	$Zone | Get-DnsServerResourceRecord
}
```

Remote DNS-Server:

```console
$DNSServer = "servername-oder-IP"
$Zones = @(Get-DnsServerZone -ComputerName $DNSServer)
ForEach ($Zone in $Zones) {
	Write-Host "`n$($Zone.ZoneName)" -ForegroundColor "Green"
	$Zone | Get-DnsServerResourceRecord -ComputerName $DNSServer
}
```

Remote DNS-Server (Ausgabe in Textdatien pro Zone):

```console
$DNSServer = "servername-oder-IP"
$Zones = @(Get-DnsServerZone -ComputerName $DNSServer)
ForEach ($Zone in $Zones) {
	Write-Host "`n$($Zone.ZoneName)" -ForegroundColor "Green"
	$Results = $Zone | Get-DnsServerResourceRecord -ComputerName $DNSServer
	echo $Results > "$($Zone.ZoneName).txt"
}
```

Super zum Backupen und so :-)

Quelle: http://sigkillit.com/2015/10/27/list-all-dns-records-with-powershell/
