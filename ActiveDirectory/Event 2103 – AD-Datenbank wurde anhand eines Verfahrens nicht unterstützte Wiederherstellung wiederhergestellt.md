Ich hatte in einem AD das Problem, dass nach einem Restore aus einem Snapshot die Domain Controllern die Anmeldung der User verweigerten und auch untereinander nicht mehr replizierten. Im Eventlog wurde folgender Fehler protokolliert:

>Ereignistyp: Fehler
>Ereignis Quelle: NTDS Allgemein
>Ereigniskategorie: Steuerung
>Ereignis-ID: 2103
>Beschreibung: Die Active Directory-Datenbank wurde anhand eines Verfahrens nicht unterstützte Wiederherstellung wiederhergestellt. Active Directory können Benutzer anmelden, während das Problem weiterhin besteht. Als Ergebnis wurde der Netlogon-Dienst angehalten. Benutzer Aktion Siehe vorherige Ereignisprotokolle Einzelheiten. Weitere Informationen finden Sie im Hilfe- und Supportcenter unter http://support.microsoft.com.

Und bei der Replikation wurde die Fehlermeldung (z.B. bei repadmin /showrepl)

>Der Quellserver nimmt keine Replikationsanforderung entgegen

ausgegeben.

Das ganze Problem wurde verursacht, dass durch die nicht unterstützte Wiederherstellung – in meinem Fall ein Snapshot – die **Datenbank der Active Directorys auf Not Writeable gesetzt wurde**.

Das ganze wieder ans laufen bekommt man wenn man in der Registry auf dem DC unter

```console
HKLM\System\CurrentControlSet\Services\NTDS\Parameters
```

den Wert **„Dsa Not Writable“** von **4 auf 0** setzt.

Dazu legt man noch einen REG_DWORD **“Ignore USN Rollback”** an und setzt den Wert auf **0**

Danach muss man den **Server neustarten**.

Damit die Replikation wieder sauber funktioniert muss man auf allen DC-Servern die Befehle

```console
repadmin /options “ServerName” -DISABLE_OUTBOUND_REPL
repadmin /options “ServerName” -DISABLE_INBOUND_REPL
```

ausführen – wobei „ServerName“ mit dem jeweiligen lokalen Servernamen des DCs ersetzten.

Jetzt sollte eigentlich alles laufen.

Falls allerdings die Replikation noch nicht funktioniert – oder andere Fehler im Eventlog protokolliert werden – kann noch ein Reset des Passwortes des Computerkontos der Domaincontroller nötig sein.

Das macht man auf den DCs folgendermaßen (am besten davor einen Reboot machen):

```console
netdom resetpwd /server:anderer_dc /userd:domain\administrator /passwordd:*
```

Danach den Server rebooten.

Jetzt sollte es wirklich wieder laufen 🙂
