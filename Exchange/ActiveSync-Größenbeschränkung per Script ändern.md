Um die Größenbeschränkung von ActiveSync (im Default 10 MB) per Script anzupassen reichen folgende Zeilen:

**CMD als Administrator** öffnen und 

```console
%windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:69730304
%windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:68096
%windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:69730304
%windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:68096
%windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:69730304
iisreset
```

ausführen.

Das Script hebt die Größe auf 50 MB an.

Werte lassen sich einfach anpassen - aber Achtung: 

maxAllowedContentLength = Wert in Bytes  
maxRequestLength = Wert in KiloBytes  
MaxDocumentDataSize = Wert in Bytes  

Funktioniert ab Exchange 2016 🙂

Mehr Infos unter https://www.frankysweb.de/exchange-2016-groessenbeschraenkung-fuer-activesync-veraendern/
