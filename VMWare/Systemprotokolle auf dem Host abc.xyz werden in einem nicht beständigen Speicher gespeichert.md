Bei Installationen des ESXi auf einem USB-Stick oder einer SD-Karte wird die Warnung 

> „Systemprotokolle auf dem host abc.xyz werden in einem nicht beständigen Speicher gespeichert„ 

angezeigt. VMware logt nämlich nicht auf USB-Speicher und Sd-Karten – den die sind nach VMWare-denke „volatil“. Nur Festplatten (respektive Datastores) sind beständig.

**Lösung**

Um das Problem der Protokolle zu lösen, lasse ich die ESXi-Hosts ihre Protokolle auf den Syslog-Server des vCenters ablegen.

Dazu wird auf dem jeweiligen Host unter

**Verwaltung – Erweiterte Einstellungen**

in dem Eintrag

**„Syslog.global.loghost“**

die Adresse des Syslog-Server des vCenter-Servers eintragen.

Das Format lautet: **udp://ip.des.vCenter.Server:514**

![](https://github.com/friedlandreas/Guides/blob/ac50e4d6ebf8ff5b0f48cb6e787616cf842a34e8/images/esxi-syslog-global-loghost.png)

fertig 🙂
