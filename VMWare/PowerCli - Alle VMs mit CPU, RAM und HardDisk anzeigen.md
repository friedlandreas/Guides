Um per PowerCli alle VMs mit CPU, RAM und HardDisk (zusammengerechnete Größe) anzeigen will, kann man das recht einfach per:
 
 ```console
Get-VM | Select Name, NumCpu, MemoryGB, @{N="HardDisk(GB)"; E={[math]::round((Get-HardDisk -VM $_ | Measure-Object -Sum CapacityGB).Sum,0)}} | sort name | ft -auto
```
Gibt dann als Ausgabe eine Liste die so aussieht:
```console
Name              NumCpu MemoryGB HardDisk(GB)
----              ------ -------- ------------
vm01                   4       12          140
vm02                   2        4          140
```

Praktisch  :-)

Quelle: https://community.broadcom.com/vmware-cloud-foundation/discussion/get-vm-name-mem-cpu-hard-disk
