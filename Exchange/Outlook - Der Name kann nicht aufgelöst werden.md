Ich stoße öfters auf den Fehler, dass Outlook beim Einrichten des Profils beim Punkt **„Am Server anmelden“** scheitert und sich nicht am Exchange anmelden kann.

Das Exchange Autodiscover funktioniert einwandfrei (Outlook konfiguriert sich sauber selbst) – nur beim letzten Punkt – eben der Anmeldung – scheitert der Einrichtungsvorgang mit folgender Meldung:

**„Der Name kann nicht aufgelöst werden. Es steht keine Verbindung mit Microsoft Exchange zur Verfügung. Outlook muss im Onlinemodus oder verbunden sein, um diesen Vorgang abzuschließen.“**

![Outlook - Name kann nicht aufgelöst werden](https://github.com/friedlandreas/Guides/blob/7a4c7261209b6280ea05b385be41c5b712b4f4b3/images/Outlook-Name-nicht-aufl%C3%B6sen.jpg)

Das komische hierbei ist, dass dieses Problem oft nicht alle Benutzer betrifft sondern nur einzelne Benutzer. Auch können z.B. andere Benutzer an dem Rechner sich ohne Problem mit Outlook an dem Exchange anmelden.

Das Problem liegt hier an der Anmeldung von Outlook am Globalen Katalog im Active Directorys.

Man kann über einen **Registry-Schlüssel** den Globalen-Katalog-Server für Outlook bei diesen Benutzern vorgeben.

Dazu erstellt man für die betroffenen Benutzer unter

```console
HKEY_CURRENT_USER\Software\Microsoft\Exchange\Exchange Provider
```

eine Zeichenfolge (REG_SZ) mit dem Namen **DS Server**

und gibt als Wert den bzw. einen Domänencontroller an (als FQDN-Namen), der den Globalen Katalog hat.

![Registry - DS-Server](https://github.com/friedlandreas/Guides/blob/7a4c7261209b6280ea05b385be41c5b712b4f4b3/images/Outlook-ExchangeProvider-DSServer1.png)

Hier in meinen Beispiel also **dc.test.local**.

Danach führt man die Profilerstellung neu durch – und dann sollte es sauber durchlaufen 🙂

![Outlook - geht wieder](https://github.com/friedlandreas/Guides/blob/7a4c7261209b6280ea05b385be41c5b712b4f4b3/images/Outlook-Name-nicht-aufl%C3%B6sen-funktioniert.png)
