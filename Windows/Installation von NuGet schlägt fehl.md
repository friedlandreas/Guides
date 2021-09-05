Wenn man auf einem Windows-Server – in meinem Fall ein Windows Server 2016 – den NuGet Paketmanager mittels
 
```console
Install-PackageProvider -Name NuGet
```

nachinstallieren will – z.B. um die Azure PowerShell-Module zu installieren – schlägt dies seit geraumer Zeit (Seit April 2020) fehl:

![NuGet installieren schlägt fehl](https://github.com/friedlandreas/Guides/blob/1bf730493379c8a1ad54688ba7ea7fb5dc944f4b/images/Powershell-NuGet-failed.png)

Die Fehlermeldung von lautet:

> Install-PackageProvider : Für die angegebenen Suchkriterien für Anbieter „NuGet“ wurde keine Übereinstimmung gefunden.
> Der Paketanbieter erfordert das PackageManagement- und Provider-Tag. Überprüfen Sie, ob das angegebene Paket über die Tags verfügt.

Der Grund ist vermutlich ein „Upgrade“ des Azureedges, der den Lookup-Provider stellt (onegetcdn.azureedge.net/providers). Der Endpunkt lässt seit etwa April 2020 keine TLS1.0 und TLS1.1 Verbindungen mehr zu und wurde auf „TLS1.2 min“ konfiguriert. Die PowerShell (< 14393.3474) spricht per Default aber nur TLS1.1.

**Lösung**

Mit folgendem Befehl stellt man die PowerShell auf TLS 1.2 um:

```console
[Net.ServicePointManager]::SecurityProtocol=[Net.SecurityProtocolType]::Tls12
```

Danach funktioniert die Installation:

```console
Install-PackageProvider -Name NuGet
```

![NuGet installieren geht](https://github.com/friedlandreas/Guides/blob/1bf730493379c8a1ad54688ba7ea7fb5dc944f4b/images/Powershell-NuGet-work.png)

