Wenn man dem Citrix VDA (Virtual Delivery Agent) ein Zertifikat mitgeben will, bentutz man das enable-vdassl.ps1-Script. 
Will man das automatisieren z.B. um vor Ablauf des Zertifikats ein neues zu hinterlegen, kann man das wunderbar skripten:

```code
#Servername auslesen
$servername=[System.Net.Dns]::GetHostByName((hostname)).HostName
$str="*"+$servername+"*"

#Zertifikat anzeigen
Get-ChildItem -path cert:\LocalMachine\My | where { $_.notafter -gt (get-date).AddDays(180) } | Where-Object -FilterScript {$_.Subject -like $str}

#VDA konfigurieren
enable-VdaSSL.ps1 -Enable -CertificateThumbPrint (Get-ChildItem -path cert:\LocalMachine\My | where { $_.notafter -gt (get-date).AddDays(180) } | Where-Object -FilterScript {$_.Subject -like $str} | Select-Object -ExpandProperty Thumbprint) -Confirm:$False
```

Es wird der Name des Servers ausgelesen und das passende Computerzertifikat das mindestestns noch 180 Tage gültig ist dem enable-vdassl.ps1 übergeben.

Quelle: https://support.citrix.com/article/CTX220062/ssl-configuration-on-vda und https://www.carlstalhood.com/virtual-delivery-agent-vda-7-14/
