Ich bekomme öfters alte Windows Domainencontroller zu sehen, auf denen ein wichtiger Dienst des Active Directory nicht sauber funktioniert: der Dateireplikationsdienst – oder NTFRS – protokolliert den **Fehler 13568** im Ereignisprotokoll (im Dateireplikationsdienst-Protokoll).

Der Dateireplikationsdienst repliziert das SYSVOL-Verzeichnis auf die Domänen-Controller der Active Directory Domäne. Das ordnungsgemäße funktionieren von Gruppenrichtlinien hängt hauptsächlich vom korrektem Betrieb der SYSVOL-Verzeichnissen ab.

Wenn es zum Fehler kommt, wird in der Fehler-Meldung auch gleich eine vermeintliche Lösung vorgeschlagen:

**Führen Sie regedit aus, um diesen Registrierungsparameter zu ändern.
Klicken Sie auf „Start“, dann auf „Ausführen“, und geben Sie dann „regedit“ ein.
Erweitern HKEY_LOCAL_MACHINE.
Folgen Sie folgendem Pfad: „System\CurrentControlSet\Services\NtFrs\Parameters“
Doppelklicken Sie auf den Namen des Wertes
„Enable Journal Wrap Automatic Restore“
und aktualisieren Sie den Wert.
Ist der Name des Wertes nicht vorhanden, können Sie ihn mit dem Befehl „Neu“ und dann „DWORD-Wert“
im Menü „Bearbeiten“ hinzufügen. Geben Sie den Wert genauso ein wie oben gezeigt.**

Das Problem bei der Sache: **Die angebote Lösung sollte man nicht anwenden** – zum einem behebt es das Problem nicht un macht in Zweifelsfall das Problem noch größer…

**Um den Fehler zu beheben ist folgendes zu tun:**

Als erstes muss auf allen Domänencontrollern der Domäne der NTFRS Dienst gestoppt werden.

Das stoppen des Dienstes kann einmal in der Kommandozeile erfolgen (net stop ntfrs) oder über die Dienstesteuerung (services.msc).
Der Anzeigename des Dienstes lautet Dateireplikationsdienst.

Auf dem Domänencontroller, auf dem das SYSVOL-Verzeichnis ordnungsgemäß vorhanden ist, setzt man unter folgendem **Registry**-Pfad:

```console
„HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative Replica Sets\<GUID>“
```

den bereits vorhandenen Eintrag **Burflags** auf den Wert **D4** (Authoritative Restore).

Der Wert D4 darf nur auf einem Domänencontroller eingetragen werden.

Hinweis: Unter Cumulative Replica Sets existiert i.d.R. eine GUID, nämlich die des SYSVOL-Verzeichnisses. Wäre DFS noch im Einsatz, gäbe es noch einen weiteren Eintrag mit einer anderen GUID.

Anschließend ist auf den weiteren Domänencontrollern der Domäne (im gleichen Registry-Pfad), im vorhandenen Eintrag **Burflags**, der Wert diesmal auf **D2** (Non-Authoritative Restore) zu setzen.

**Nun gilt es zuerst auf dem Domänencontroller, auf dem Burflags auf D4 gesetzt wurde, den NTFRS-Dienst (net start ntfrs) zu starten.** 
Nach dem Start vom NTFRS bleibt der Burflags Eintrag vorhanden, lediglich der Wert wird auf 0 (genullt) zurückgesetzt.
Danach wird im Dateireplikations-Protokoll der Event-Eintrag 13566 protokolliert. Dieser bedeutet, dass eine autorisierende Wiederherstellung gestartet wurde. Die Dateien die vom FRS repliziert werden, bleiben unverändert und werden dabei als autorisierend gekennzeichnet.
Zusätzlich wird die FRS-Datenbank neu erstellt. Mit ein wenig Geduld, muss anschließend der Event-Eintrag 13516 protokolliert werden.
Denn erst dann, ist der FRS einsatzbereit.

**Wenn alles planmäßig ausgeführt wurde, ist auf den restlichen Domänencontrollern der Domäne (auf denen der Wert Burflags D2 gesetzt wurde), ebenfalls der NTFRS-Dienst zu starten**. 
Der FRS-Dienst setzt dabei ebenfalls den Wert von Burflags zurück auf 0.

Im Dateireplikations-Protokoll wird der Event-Eintrag 13565 verzeichnet. Dieser bedeutet, dass eine nicht autorisierte Wiederherstellung gestartet wurde. Anschließend wird die FRS-Datenbank neu erstellt und es wird eine vollständige Replikation des SYSVOL-Verzeichnisses durchgeführt. Wenn alles ordnungsgemäß ausgeführt wurde, wird im Dateireplikations-Protokoll der Event-Eintrag 13516 verzeichnet. Danach wäre der FRS betriebsbereit.

**Im Anschluss wäre es empfehlenswert mit DCDIAG die FRS-Replikation zu überprüfen.**

Eine abschließende Kontrolle auf allen DCs sollte folgende Aufgaben beinhalten:
1. Existiert auf allen Domänencontrollern das SYSVOL-Verzeichnis und wurde es auch freigegeben?
2. Ist der Inhalt vom SYSVOL-Verzeichnis auf allen Domänencontrollern vollständig und auf allen DCs gleich?
3. Existieren auf allen Domänencontrollern die Junction Points?
4. Werden im Dateireplikations-Protokoll der Domänencontroller noch Fehler gemeldet (was logischerweise nicht der Fall sein sollte)?
5. Melden die Diagnose-Tools Fehler?
