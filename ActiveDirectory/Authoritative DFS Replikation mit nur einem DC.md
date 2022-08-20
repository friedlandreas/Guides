Hat man nur einen Domänencontroller kann die DFS-Replikation (DFS-R) des SYSVOL auch Probleme machen (z.B. im DFS-R-Log den Fehler **4012**, **2212** oder **2213** ) - oft liegen diese Problem an einer nicht ordentlich abgeschlossen Domaincontroller-Migration. Auch hier kann man das Problem mit einer authoritativen DFS Replikation (ähnlich wie früher bei NTFRS) relativ leicht beheben.


## Vorbereitung

Wir brauchen später die DFRSDIAG-Tools - diese sind oft nicht installiert. Bitte auf unserem DC in einer Powershell

```console
Install-WindowsFeature RSAT-DFS-Mgmt-Con
```
ausführen.

## DFRS-Replikation ausschalten

Zum Start öffnen wir eine **adsiedit.msc** mit **administrativen Rechten** auf unseren DC und erstellen eine Verbindung wmit dem **Standardmäßiger Namenskontext**

![ADSIEDIT-Standardmaessiger-Namenskontext](https://github.com/friedlandreas/Guides/blob/66a839258dd1689485b73b1e08da986a65321c82/images/ADSIEDIT-Standardmaessiger-Namenskontext.png)

Jetzt navigieren wir zu 

> DC=Domain/DC=TLD/OU=Domain Controllers/CN=ErsterDomänencontrollername/CN=DFSR-LocalSettings/CN=Domain System Volume/CN=SYSVOL Subscription


![ADSIEDIT-SYSVOL-Subscription](https://github.com/friedlandreas/Guides/blob/d1a4b2be3c8a235108e0b80e0799ad9c0c6a332b/images/ADSIEDIT-SYSVOL-Subscription-01-SingleDC.png)

und öffnen 
> **CN=SYSVOL Subscription** 

und setzten die Werte

> **msDFSR-Enabled** auf **False**

> **msDFSR-Options** auf **1**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-DC](https://github.com/friedlandreas/Guides/blob/9aab1fe718185788b5125230342686849fe87d2a/images/ADSIEDIT-SYSVOL-Subscription-02-SingleDC.png)


## DFSR-Dienst

Jetzt starten wir auf unserem DC eine **CMD** mit **administrativen Rechten** und starten die AD-Replikation 

```console
repadmin.exe /syncall
DFSRDIAG POLLAD
```

und statet den DFSR-Dienst durch

```console
net stop DFSR && net start DFSR
```

![](https://github.com/friedlandreas/Guides/blob/75134871635f35d5bd3a8d3edd5a0317e38a20d0/images/ADSIEDIT-SYSVOL-Subscription-03-SingleDC.png)


## DFRS-Replikation einschalten

Jetzt schalten wir die Replikation authoritativ wieder ein.

Im **ADSIEDIT** setzten wir jetzt den Wert

> **msDFSR-Enabled** auf **True**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-DC-enable](https://github.com/friedlandreas/Guides/blob/d95b00fa850addf5e0c4753a01877162ab16a350/images/ADSIEDIT-SYSVOL-Subscription-04-SingleDC.png)

und starten dann in einer **CMD** mit **administrativen Rechten** die Replikation

```console
repadmin.exe /syncall
DFSRDIAG POLLAD
```

Jetzt sollte im Eventlog der Event 4602 auftauchen

![DFRS-Eventlog](https://github.com/friedlandreas/Guides/blob/d49d9001be389e60c7fb4311c0ef9e0e526bb262/images/Eventlog-DFSR-4602.png)

Jetzt sollte wieder alles sauber laufen 😄

Quellen: [andysblog.de](https://www.andysblog.de/windows-fehler-4012-dfsr-bei-nur-einem-domaenencontroller)



