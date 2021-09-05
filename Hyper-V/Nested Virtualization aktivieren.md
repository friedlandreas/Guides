Will man auf einem Hyper-V-Host ein VM mit aktivierter Virtualisierung – z.B. einen Server mit der Hyper-V-Rolle – installieren, muss man die VM erstellen und dann das Nested Virtualization-Feature für die VM mit folgenden Befehlen per Powershell aktivieren:

```console
get-vm VMNAME | Set-VMProcessor -ExposeVirtualizationExtensions $true                                                     
get-vm VMNAME | Set-VMNetworkAdapter -MacAddressSpoofing On 
```

Hier als Beispiel mit der VM mit dem dem Namen **55_HyperV**:

```console
get-vm 55_HyperV | Set-VMProcessor -ExposeVirtualizationExtensions $true                                                     
get-vm 55_HyperV | Set-VMNetworkAdapter -MacAddressSpoofing On 
```

![Hyper-V nested Virtualization](https://github.com/friedlandreas/Guides/blob/295019b6a635c6d37d3367d3434363ad19938a08/images/HyperV-nested-virtualization.png)

Danach lässt sich – in dem Fall HyperV – der Hypervisor installieren/aktivieren
