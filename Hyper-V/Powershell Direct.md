Man kann auf einem Hyper-V-Host per Powershell Direct direkt ein Powerhsell-Session in eine Gast-VM starten:

```console
Enter-PSSession -VMName MyVM -Credential MyVM\Administrator
```

Nicht nur eine Shell geht -> es können auch direkt Befehle an die VM geschickt werden:

```console
Invoke-Command -VMName MyVM -ScriptBlock { command } 
```

Super praktisch :-)

Quelle bzw. Doku: https://learn.microsoft.com/de-de/virtualization/hyper-v-on-windows/user-guide/powershell-direct
