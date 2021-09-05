Wenn man auf einem Windows Server 2016 oder 2019 auf eine WebDAV-Freigabe zugreifen will, muss man ein Feature nachinstallieren das in der Standardinstallation nicht aktiviert ist.

Dazu am besten eine Powershell als Admin starten und folgendes eingeben:

```console
Install-WindowsFeature WebDAV-Redirector –Restart
```

Jetzt wird das Feature installiert und der Server neu gestartet.

Nach dem Neustart ist ein Zugriff auf die WebDAV-Freigabe (z.B. Nextcloud) möglich

![Windows WebDAV](https://github.com/friedlandreas/Guides/blob/6687ce5a5cf3073e70a277bc9ca5e08dc13c02c6/images/Windows-WebDAV.png)
