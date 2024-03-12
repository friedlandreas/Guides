Wenn man unter WSL (Windows-Subsystem für Linux) den DNS fest setzten will, muss man erstmal das autogenerieren der resolv.conf in der wsl.conf abschalten:

```console
vim /etc/wsl.conf
```

dort den Eintrag

```console
[network]
generateResolvConf=false
```

hnzufügen.

Jetzt eninfach eine /etc/resolv.conf erstellt werden

```console
vim /etc/resolv.conf
```

und dort die DNS-Einträge konfigurieren - hier einfaches Beispiel:

```console
nameserver 1.1.1.1
nameserver 9.9.9.9
```

Danach solte die Konfig-DAtei nicht mehr überschrieben werden :-)
