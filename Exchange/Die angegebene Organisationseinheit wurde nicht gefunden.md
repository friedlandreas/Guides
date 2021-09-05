Hatte bei einem Exhange das Problem das wenn man einen bestimmte Benutzer bearbeiten will, folgender Fehler kommt:

**„Die angegebene Organisationseinheit wurde nicht gefunden. Stellen Sie sicher, dass Sie die Identität der Organisationseinheiten korrekt eingegeben haben.“**

![Exchange Fehler](https://github.com/friedlandreas/Guides/blob/9cb60650e25f998e2325ceebf93fbf69a1850766/images/Exchange2013-Organisationseinheit-Fehler-1.png)

und in der Ereignisanzeige taucht der Fehler **MSExchange CmdletLogs** mit der **Event-ID 6 (Cmdlet fehlgeschlagen. Cmdlet Get-UserPrincipalNamesSuffix, Parameter {OrganizationalUnit=domain.tld/OU})** auf:

![Exchange Fehler - Eventlog](https://github.com/friedlandreas/Guides/blob/9cb60650e25f998e2325ceebf93fbf69a1850766/images/Exchange2013-Organisationseinheit-Fehler-2.png)

Der Grund für den Fehler liegt darin, dass in der Domain der User-Container vom Default-Wert abweicht. Das kann z.B. bei einer Migration von einem Small Business Server sein, da hier der Standard-Container der Benutzer verschachtelt unter der MyBusiness-OU liegt. Oder der Admin hat den Pfad manuell geändert.

Man kann den Wert am einfachsten in der Powershell mit 

```console 
Get-ADDomain
```

überprüfen:

![Powershell - Get-AdDomain](https://github.com/friedlandreas/Guides/blob/9cb60650e25f998e2325ceebf93fbf69a1850766/images/Exchange2013-Organisationseinheit-Fehler-3.png)

Wenn dieser nicht dem Standard-Wert **„CN=Users,DC=Domainname,DC=tld“** entspricht (also in meinem Beispiel CN=Users,DC=test,DC=local) – kommt es zu dem beschriebenen Fehler.

Wenn man den Standard-Container für die Benutzer wieder auf den Standardwert setzt funktioniert alles wieder.

Am einfachsten geht es mit folgendem Befehl:

```console
redirusr „CN=Users,DC=Domainname,DC=tld“
```

also z.B.

```console
redirusr „CN=Users,DC=test,DC=local“
```

![Powershell - Redirusr - Get-AdDomain](https://github.com/friedlandreas/Guides/blob/9cb60650e25f998e2325ceebf93fbf69a1850766/images/Exchange2013-Organisationseinheit-Fehler-4.png)

Ohne Neustart von Servern oder Dienste funktioniert die Bearbeitung der User sofort wieder 🙂
