Für bestimmte Outook-Zugriffe (über ReverseProxys, Mac, nicht in selber Domäne, etc) braucht man die Standardauthentifiziereung für MAPI und für EWS. 

Diese kann man super einfach per Script aktivieren:

```powershell
### IIS EWS
$iisSiteName = "Default Web Site"
$iisAppName = "EWS"
Write-Host Enable windows authentication
Set-WebConfigurationProperty -Filter '/system.webServer/security/authentication/basicAuthentication' -Name 'enabled' -Value 'true' -PSPath 'IIS:\' -Location "$iisSiteName/$iisAppName"
### IIS MAPI
$iisSiteName = "Default Web Site"
$iisAppName = "mapi"
Write-Host Enable windows authentication
Set-WebConfigurationProperty -Filter '/system.webServer/security/authentication/basicAuthentication' -Name 'enabled' -Value 'true' -PSPath 'IIS:\' -Location "$iisSiteName/$iisAppName"
### IIS reset
iisreset
write-host "Fertig!"
```

Danach lässt sich Outlook per Username/Passwort starten 😃

**Achtung:** Manche CU-Updates setzen das auch gerne mal zurück - einfach nach dem CU-Upgrade ausführen
