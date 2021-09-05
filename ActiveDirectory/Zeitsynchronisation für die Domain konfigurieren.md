Die Zeit ist in einem Active Directory extrem wichtig – so kann man sich z.B. (bei Default-Einstellungen) mit einer Zeitdifferenz mehr als 5 Minuten zwischen Domain Controller und Client nicht authentifizieren und deshalb nicht einloggen.

Der Windows Zeitdienst (**W32Time**) ist dafür zuständig das überall in der Domäne die gleiche Zeit ist. Alle Clients syncen mit „ihrem“ Domain Controller und die Domain Controller syncen mit dem DC der die PDC-Rolle inne hat.

![AD NTP](https://github.com/friedlandreas/Guides/blob/e6aa2c1f1cdac48150def4fe1efdcfca079e82e1/images/Time-Sync-Domain.gif)

Damit überall die gleiche – und am besten auch noch die richtige 😉 – Zeit ist konfiguriert man **an dem DC mit der PDC-Rolle den Windows Zeitdienst folgendermaßen per Powershell**:

```console
w32tm /config /manualpeerlist:timeserver /syncfromflags:manual /reliable:yes /update
```

also z.B. :

```console
w32tm /config /manualpeerlist:0.de.pool.ntp.org /syncfromflags:manual /reliable:yes /update
```

oder mit mehreren NTP-Servern:

```console
w32tm /config /syncfromflags:manual /manualpeerlist:“0.de.pool.ntp.org 1.de.pool.ntp.org“ /reliable:yes /update
```

Danach den Windows Zeitdienst durchstarten

```console
Restart-Service W32Time
```

und noch einmal syncen lassen

```console
w32tm /resync
```

Mit

```console
w32tm /query /status
```

kann überprüft werden ob der Sync funktioniert – fertig 🙂

![w32tm](https://github.com/friedlandreas/Guides/blob/e6aa2c1f1cdac48150def4fe1efdcfca079e82e1/images/windows-w32tm-dc.png)

Alle anderen DCs und/oder Clients der Domäne sollten sich jetzt mit dem PDC synchronisieren.

Ebenfalls mit

```console
w32tm /query /status
```

kann überprüft werden ob das auch klappt.

Nach ein paar Minuten sollte auf allen Domain-Membern die gleiche Zeit sein 🙂
