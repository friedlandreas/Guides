Wenn auf den Domänencontrollern eines ActiveDirectorys die DFS-Replikation (DFS-R) des SYSVOL Probleme macht (z.B. im DFS-R-Log den Fehler **4012**, **2212** oder **2213** ), kann man das Problem mit einer authoritativen DFS Replikation (ähnlich wie früher bei NTFRS) relativ leicht beheben.

## Vorbereitung

Wir brauchen später die DFRSDIAG-Tools - diese sind oft nicht installiert. Bitte auf allen DCs in einer Powershell

```console
Install-WindowsFeature RSAT-DFS-Mgmt-Con
```
ausführen.

## Primärer Domaincontroller

Zum Start öffnen wir eine **adsiedit.msc** mit **administrativen Rechten** auf unseren primären DC und erstellen eine Verbindung wmit dem **Standardmäßiger Namenskontext**

![ADSIEDIT-Standardmaessiger-Namenskontext](https://github.com/friedlandreas/Guides/blob/66a839258dd1689485b73b1e08da986a65321c82/images/ADSIEDIT-Standardmaessiger-Namenskontext.png)

Jetzt navigieren wir zu 

> DC=Domain/DC=TLD/OU=Domain Controllers/CN=ErsterDomänencontrollername/CN=DFSR-LocalSettings/CN=Domain System Volume/CN=SYSVOL Subscription


![ADSIEDIT-SYSVOL-Subscription](https://github.com/friedlandreas/Guides/blob/f20a584906f63daf2aa996e059191628ea72e58a/images/ADSIEDIT-SYSVOL-Subscription-01.png)

und öffnen 
> **CN=SYSVOL Subscription** 

![ADSIEDIT-SYSVOL-Subscription-Settings](https://github.com/friedlandreas/Guides/blob/c63162fb5d23f4aca15ca20a6e3c73d92507d732/images/ADSIEDIT-SYSVOL-Subscription-02.png)

und setzten die Werte

> **msDFSR-Enabled** auf **False**

> **msDFSR-Options** auf **1**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-primary-DC](https://github.com/friedlandreas/Guides/blob/d3c909ed1feb5998d235fca921377a858d65ea83/images/ADSIEDIT-SYSVOL-Subscription-03.png)

## Alle anderen Domaincontroller

Jetzt navigieren wir in unserem ADSIEDIT zu **allen anderen DCs**

> DC=Domain/DC=TLD/OU=Domain Controllers/CN=AndereDomänencontrollernamen/CN=DFSR-LocalSettings/CN=Domain System Volume/CN=SYSVOL Subscription

und setzten **nur** den Wert

> **msDFSR-Enabled** auf **False**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-secondary-DCs](https://github.com/friedlandreas/Guides/blob/c661316310a309beba52ffa6d5e492e60952e8b5/images/ADSIEDIT-SYSVOL-Subscription-04.png)

## DFSR-Dienst

Jetzt starten wir zuerst auf unserem **primären DC** eine **CMD** mit **administrativen Rechten** und starten die AD-Replikation 

```console
repadmin.exe /syncall
```

![repadmin-syncall](https://github.com/friedlandreas/Guides/blob/6290887e804acc22e392eff15011ea8d24c4af6f/images/repadmin-syncall.png)

und statet den DFSR-Dienst durch

```console
net stop DFSR && net start DFSR
```

und **wiederholen das auf allen anderen DCs**.

Jetzt sollten im Event-Log der Event 4602 und 4114 auftauchen

![DFRS-Eventlog](https://github.com/friedlandreas/Guides/blob/8f613523194d0c86d50a76d953abf6bf12955059/images/Eventlog-DFSR-4114.png)

## DFRS-Replikation primärer DC

Da jetzt alle SYSVOLs nicht mehr an der Replikation teilnehmen können wir jetzt diese authoritativ wieder einschalten.

Auf unsern **primären DC** im **ADSIEDIT** setzten wir jetzt den Wert

> **msDFSR-Enabled** auf **True**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-primary-DC-enable](https://github.com/friedlandreas/Guides/blob/49d6cae56a06a7c107a4707e4a24575168080ab5/images/ADSIEDIT-SYSVOL-Subscription-05.png)

und starten dann in einer **CMD** mit **administrativen Rechten** die Replikation

```console
repadmin.exe /syncall
DFSRDIAG POLLAD
```

Jetzt sollte im Eventlog der Event 4602 auftauchen

![DFRS-Eventlog](https://github.com/friedlandreas/Guides/blob/d49d9001be389e60c7fb4311c0ef9e0e526bb262/images/Eventlog-DFSR-4602.png)

## DFRS-Replikation alle anderen DCs

Jetzt setzten wir im **ADSIEDIT** für **alle anderen DCs** den Wert

> **msDFSR-Enabled** auf **True**

![ADSIEDIT-SYSVOL-Subscription-msDFSR-Settings-other-DC-enable](https://github.com/friedlandreas/Guides/blob/c2eb24f83b03b6d65fcf16e1866e7a4f93bcdaed/images/ADSIEDIT-SYSVOL-Subscription-06.png)

und starten auf **jedem DC** eine **administrative CMD** und starten die Replikation mit 

```console
DFSRDIAG POLLAD
```

Dann sollte nach kurzer Zeit am primären DC im Eventlog das Event 5004 auftauchen

![DFRS-Eventlog](https://github.com/friedlandreas/Guides/blob/e9d8699e27cbe912b8612418153948881332f15b/images/Eventlog-DFSR-5004.png)

> **Tipp:** 
> Wenn das Event 5004 auf sich warten lässt - auf den DCs den DFRS-Dienst neustarten , z.B. mit **net stop DFSR && net start DFSR**

Jetzt sollte wieder alles sauber laufen 😄

Quellen: [johnlose.de](https://www.johnlose.de/2016/03/dfsr-fehler-4012-auf-sysvol-dfs-replikation-in-windows-server-2012-dc/)




