Um die konfiguriereten Netzwerke bzw. virtuelle Switche von VMs unter Hyper-V anzuzeigen kann man neben der GUI-Tools (Hyper-V-Manager, Windows Admin Center, etc) das ganze auch schön mittels Powershell tun:

#### virtueller Switch einer VM:

```console
get-vm 44_docker | Select -ExpandProperty Networkadapters | Select vmname, switchname | Format-Table -AutoSize
```

#### virtuelle Switche aller laufender VMs:

```console
get-vm | Where-Object {$_.State -eq 'Running'}|  Select -ExpandProperty Networkadapters | Select vmname, switchname | Format-Table -AutoSize
```

#### virtuelle Switche aller VMs:

```console
get-vm | Select -ExpandProperty Networkadapters | Select vmname, switchname | Format-Table -AutoSize
```

#### Zusätzliche Infos

Man kann natürlich auch mehr Infos anzeigen -> z.B. kann man zusätzlich auch die IPs anzeigen 

```console
get-vm |  Select -ExpandProperty Networkadapters | Select vmname, switchname, ipaddresses | Format-Table -AutoSize
```

#### Beispiel

Sieht dann so aus:

![Hyper-V Netzwerk der Vms](https://github.com/friedlandreas/Guides/blob/604a6cd4c46f0f995623050691199d8b1c36f8ba/images/Hyper-V-Netzwerke-VMs.PNG)
