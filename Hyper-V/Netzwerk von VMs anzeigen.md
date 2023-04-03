Um die konfiguriereten Netzwerke bzw. virtuelle Switche von VMs unter Hyper-V anzuzeigen kann man neben der GUI-Tools (Hyper-V-Manager, Windows Admin Center, etc) das ganze auch schön mittels Powershell tun:

virtueller Switch einer VM:

```console
get-vm 44_docker | Select -ExpandProperty Networkadapters | Select vmname, switchname | Format-Table -AutoSize
```

virtuelle Switche aller laufender VMs:

```console
get-vm | Where-Object {$_.State -eq 'Running'}|  Select -ExpandProperty Networkadapters | Select vmname, switchname | Format-Table -AutoSize
```

virtuelle Switche aller VMs:

```console
get-vm | Select -ExpandProperty Networkadapters | Select vmname, switchname | Format-Table -AutoSize
```

Man kann natürlich auch mehr Infos anzeigen -> z.B. kann man zusätzlich auch die IPs anzeigen 

```console
get-vm |  Select -ExpandProperty Networkadapters | Select vmname, switchname, ipaddresses | Format-Table -AutoSize
```

Sieht dann zum Beispiel so aus:

![Hyper-V IP-Adressen der Vms](https://github.com/friedlandreas/Guides/blob/376aa19eab7f999ec8b2a92ff6c6514982b86359/images/Hyper-V-IP-Adressen-VMs.PNG)
