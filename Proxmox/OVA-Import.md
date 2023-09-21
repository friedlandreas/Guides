Man kann VMs im OVA-Format relativ einfach in Proxmox importieren:

**1) OVA-DAtei auf Proxmx-Host hochladen**

Zuerst ladet man die OVA-Datei z.B. per SCP auf den Proxmox-Host auf dem man die VM ausführen will (am besten in einen temporären Ordner)

**2) SSH auf den Proxmox-Host**

Jetzt verbinden wir uns per SSH auf den Proxmox-Host

**3) OVA entpacken**

Jetzt entpacken wir die hochgeladen Datei 

```console
tar -xvf VM.ova
```

**4) OVF importieren**

Jetzt kann die VM über die OFV-Datei importiert werden:

**qm importovf UNBENUTZTEVM-NUMMER OVF-DATEI PROXMOX-SPEICHER**

Also z.B. :

```console
qm importovf 720 VM.ovf local-lvm
```

**5) Anpassen der VM**

Jetzt kann in der Proxmox-GUI die VM angepasst werden (Name, Tag, etc).

> [!WARNING]
> Oft sind nach dem Import keine Netzwerkkarten in der VM angelegt - diese dann einfach hinzufügen

**6) VM starten**

Jetzt kann man die VM starten :-)
