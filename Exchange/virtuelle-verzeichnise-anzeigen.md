Um alle auf einem Exchange-Server konfigurierten URLs der Virtuellen Verzeichnisse anzeigen zu lassen verwende ich immer folgendes Script 

Am besten einfach in der **ISE** auf dem Server starten :slightly_smiling_face:

```console
#Sripted by: Andreas Friedl
#Creation Date: 26.05.2022
#Version: 1.4

Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

$servername = $env:computername


write-host "."  
write-host ""
write-host "Uebersicht der URLs:"
write-host ""
write-host "OWA:"
Get-OwaVirtualDirectory -Server $servername | fl internalurl, externalurl
write-host "ECP:" 
Get-EcpVirtualDirectory -server $servername | fl internalurl, externalurl 
write-host "WebServices:"
Get-WebServicesVirtualDirectory -server $servername | fl internalurl, externalurl
write-host "ActveSync:"
Get-ActiveSyncVirtualDirectory -Server $servername  | fl internalurl, externalurl 
write-host "OAB:"
Get-OabVirtualDirectory -Server $servername | fl internalurl, externalurl
write-host "MAPI:"
Get-MapiVirtualDirectory -Server $servername | fl externalurl,internalurl
write-host "OutlookAnywhere:"
Get-OutlookAnywhere -Server $servername | fl externalhostname, internalhostname 
write-host "CAS:"
Get-ClientAccessService $servername | fl AutoDiscoverServiceInternalUri
write-host ""
write-host ""
pause
```
