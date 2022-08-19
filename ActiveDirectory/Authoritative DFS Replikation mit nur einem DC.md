Wenn auf einem Domänencontroller eines ActiveDirectorys die DFS-Replikation (DFS-R) des SYSVOL Probleme macht (z.B. im DFS-R-Log den Fehler **4012**, **2212** oder **2213** ), kann man das Problem mit einer authoritative DFS Replikation (ähnlich wie früher bei NTFRS)  relativ leicht beheben.

Hat man nur einen Domänencontroller können diese Fehler totztdem auftreten - oft liegen diese Problem an einer nciht ordentlich abgeschlossen Domaincontroller-Migration.


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

![ADSIEDIT-SYSVOL-Subscription-Settings](https://github.com/friedlandreas/Guides/blob/c63162fb5d23f4aca15ca20a6e3c73d92507d732/images/ADSIEDIT-SYSVOL-Subscription-02.png)

und setzten die Werte

> **msDFSR-Enabled** auf **False**

> **msDFSR-Options** auf **1**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-primary-DC](https://github.com/friedlandreas/Guides/blob/d3c909ed1feb5998d235fca921377a858d65ea83/images/ADSIEDIT-SYSVOL-Subscription-03.png)


## DFSR-Dienst

Jetzt starten wir auf unserem DC eine **CMD** mit **administrativen Rechten** und starten die AD-Replikation 

```console
repadmin.exe /syncall
DFSRDIAG POLLAD
```

![repadmin-syncall](https://github.com/friedlandreas/Guides/blob/6290887e804acc22e392eff15011ea8d24c4af6f/images/repadmin-syncall.png)

und statet den DFSR-Dienst durch

```console
net stop DFSR && net start DFSR
```

## DFRS-Replikation einschalten

Jetzt schalten wir die Replikation authoritativ wieder ein.

Im **ADSIEDIT** setzten wir jetzt den Wert

> **msDFSR-Enabled** auf **True**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-primary-DC-enable](https://github.com/friedlandreas/Guides/blob/49d6cae56a06a7c107a4707e4a24575168080ab5/images/ADSIEDIT-SYSVOL-Subscription-05.png)

und starten dann in einer **CMD** mit **administrativen Rechten** die Replikation

```console
repadmin.exe /syncall
DFSRDIAG POLLAD
```

Jetzt sollte im Eventlog der Event 4602 auftauchen

![DFRS-Eventlog](https://github.com/friedlandreas/Guides/blob/d49d9001be389e60c7fb4311c0ef9e0e526bb262/images/Eventlog-DFSR-4602.png)

Jetzt sollte wieder alles sauber laufen 😄

Quellen: [andysblog.de](https://www.andysblog.de/windows-fehler-4012-dfsr-bei-nur-einem-domaenencontroller)



