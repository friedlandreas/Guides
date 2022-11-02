Unter Proxmox VE 7.x können auf **deutschen** virtuelle Windows Server (2016 / 2019 / 2022) nicht alle VirtIO Treibern installiert werden (vorallem Netzwerk macht Probleme).

Dies betrifft die Server wenn diese als **VirtIO (paravirtualized)** eingerichtet bzw. verwendet wird und der Machine-Type **PC-Q35-6.1“ oder höher** ist. 

Sowohl während der Installation als auch später im virtuellen OS scheitert die Installation der Treiber - auch die Verwendung der aktuellesten VirtIO-Treiber (Stand 10/2022) hilft hier nicht.

## Lösung

**Vor** der Installation der DE-Version der Maschinentyp explizit auf **PC-Q35-6.0** setzen dann kann der Treiber in der PE-Umgebung oder auch später im virtuellen OS/Desktop ohne Probleme installiert werden. 

![Proxmox Machine Type ändern](https://github.com/friedlandreas/Guides/blob/67296462f5fcdf9a81e76d012bdefaea65ef1f11/images/Proxmox-7-Win-Server-Problem.PNG)

Nach erfolgreicher Treiberinstallation kann die VM heruntergefahren und der Maschinentyp kann wieder auf **PC-Q35-6.1 oder höher** geändert werden.
