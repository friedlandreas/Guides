Wenn man seit Windows 2012 einen Domäne neu erstellt hat, wird die Replikation des SYSVOLs schon mit DFSR (Distributed File System Replication) realisiert. Hat man aber von einer Windows 2000 oder Windows 2003 Domäne migriert wird höchstwahrscheinlich die SYSVOLs immer noch mit FRS (File Replication Service) repliziert – auch wenn man auf Windows 2012 R2 migriert hat.

Der FRS-Dienst (auch NTFRS oder auf deutsch Dateireplikationsdienst genannt) ist aber seit Windows 2003 R2 abgekündigt, fehleranfälliger, schlecht überwachbar, schlechter in der Performance, nicht mehr weiterentwickelt und mittlerweile auch tot (wird in neueren Versionen von Windows nicht mehr enthalten sein).

Spätestens mit der Migration auf Windows 2012/2012 R2 sollte deshalb die SYSVOL-Replikation auf DFSR umgestellt werden.

Hier mal eine Kurzanleitung wie man das macht:


**1) Voraussetzungen checken**

– Als erstes sollte getestet werden ob die bisherige Replikation funktioniert. Am einfachsten legt man dazu eine Textdatei in die **NETLOGON-Freigabe** eines Domain-Controllers und überprüft ob diese auf den anderen DCs auftaucht

– Auch das **FRS-Ereignisprotokoll** auf den DCs sollte überprüft werden und Fehler korrigiert werden

![FRS-Eventlog](https://github.com/friedlandreas/Guides/blob/b7f82cb47a6016f085c88e6ff86bd21a8cc8a3ef/images/FRS-Eventlog.png)

– Ausserdem **muss** die Domänenfunktionsebene mindestens **Windows2008* sein. (Zum überprüfen kann man auf in der Powershell (als Administrator ausführen) ein **Get-ADDomain* ausführen)


**2) Migration starten**

Wenn alle Voraussetzungen erfüllt sind kann man an die Migration gehen. Die Migration sollte man am besten vom Domain-Controller ausführen, der die PDC-Rolle innehat. Alle Befehle müssen in einer CMD oder Powershell als Administrator ausgeführt werden.

**2.1) Status „Starten“**

```console
dfsrmig /setGlobalState 0
```

Damit werden alle Domänencontroller auf den Status „Starten“ gesetzt. Zum verifizieren starten wir jetzt noch folgenden Befehl:

```console
dfsrmig /GetMigrationState
```

Dort sollte jetzt „Alle Domänencontroller wurden erfolgreich zum globalen Status („Starten“) migriert“ stehen.

![DFS Start](https://github.com/friedlandreas/Guides/blob/b7f82cb47a6016f085c88e6ff86bd21a8cc8a3ef/images/DFS_Start.png)

Dann können wir weitermachen...

**2.2) Status „Vorbereitet“**

```console
dfsrmig /setGlobalState 1
```

Damit werden alle Domänencontroller auf den Status „Vorbereitet“ gesetzt.

Nach einer gewissen Zeit sollte der Status auf allen Domänencontroller gesetzt worden sein. Zum überprüfen kann wieder der Befehl

```console
dfsrmig /GetMigrationState
```

abgesetzt werden.

![DFS Vorbereitet](https://github.com/friedlandreas/Guides/blob/b7f82cb47a6016f085c88e6ff86bd21a8cc8a3ef/images/DFS_Vorbereitet.png)

Wenn die Meldung „Alle Domänencontroller wurden erfolgreich zum globalen Status („Vorbereitet“) migriert“ kommt, können wir wieder weiter machen...

**2.3) Status „Umgeleitet“**

```console
dfsrmig /setGlobalState 2
```

Damit werden alle Domänencontroller auf den Status „Umgeleitet“ gesetzt.

Nach einer gewissen Zeit sollte der Status auf allen Domänencontroller gesetzt worden sein. Zum überprüfen kann wieder der Befehl

```console
dfsrmig /GetMigrationState
```

abgesetzt werden.

![DFS Umgeleitet](https://github.com/friedlandreas/Guides/blob/b7f82cb47a6016f085c88e6ff86bd21a8cc8a3ef/images/DFS_Umgeleitet.png)

Wenn die Meldung „Alle Domänencontroller wurden erfolgreich zum globalen Status („Umgeleitet“) migriert“ kommt, können wir wieder weiter machen...

**2.4) Status „Entfernt“**

```console
dfsrmig /setGlobalState 3
```

Damit werden alle Domänencontroller auf den Status „Entfernt“ gesetzt.

Nach einer gewissen Zeit sollte der Status auf allen Domänencontroller gesetzt worden sein. Zum überprüfen kann wieder der Befehl

```console
dfsrmig /GetMigrationState
```

abgesetzt werden.

![DFS Entfernt](https://github.com/friedlandreas/Guides/blob/b7f82cb47a6016f085c88e6ff86bd21a8cc8a3ef/images/DFS_Entfernt.png)

Wenn die Meldung „Alle Domänencontroller wurden erfolgreich zum globalen Status („Entfernt“) migriert“ kommt, sind wir mit der Migration fertig.

**3) Migration überprüfen**

Durch die Migration wurde der SYSVOL-Ordner unter C:\Windows zu einem SYSVOL_DFSR. ALter Ballast wie der Staging-Ordner wurde entfernt bzw. nicht mitmigriert. Die SYSVOL und NETLOGON-Freigabe zeigen nun auf die Inhalte des neuen SYSVOL_DFSR. Der Dateireplikationsdienst wurde auf allen Domänencontrollern auf deaktiviert gesetzt.

Somit wird ausschließlich über DFSR repliziert – FRS ist somit Geschichte 🙂

Für weitere und detailiertere Informationen kann hier nachgeschaut werden:
http://blogs.technet.com/b/deds/archive/2008/09/05/win2008-sysvol-migration-von-frs-auf-dfsr.aspx  
http://blogs.technet.com/b/filecab/archive/2008/02/08/sysvol-migration-series-part-1-introduction-to-the-sysvol-migration-process.aspx  
