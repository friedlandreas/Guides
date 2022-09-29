Die Rechte-Vererbung im ActiveDirectory ist manchmal bei bestimmten Benutzern deaktiviert – selten ist das gewollt – fast immer gibt es aber deswegen (vor allem in Verbindung mit Exchange) Probleme.

## Probleme

**- ExchangeSynchronisationsfehler 86000C0A bei betroffenen Benutzern, obwohl OWA korrekt funktioniert**

**– Dateisystems-Auflistung im Explorer schlängt mit 0x86000Cxx Fehlern fehl**

**– Fehler im Ereignisprotokoll von MSExchange ActiveSync mit dem Inhalt „Active directory Antwort: 00000005: SecErr: DSID-031521D0, problem 4003 (INSUFF_ACCESS_RIGHTS), data 0″.“**

**– Exchange: das Verschieben der Mailbox der Benutzer (z.B. bei Exchange-Migrationen) schlägt fehl**

## Lösung

Um diese Fehler zu beheben muss man bei dem Benutzer im ActiveDirectory die Vererbung aktivieren. Das geht folgendermaßen:

Zuerst müssen wir in der MMC **Active Directory Benutzer und Computer** (ADUC) die **Erweiterte Features** einschalten

![AD-Rechte-Vererben-01](https://github.com/friedlandreas/Guides/blob/ca3343dda3928e5fcdb018192fc69e5677ed8ae0/images/AD-RechteVererben01.PNG)

Dann kann beim betroffenen Bentutzer im Reiter **Sicherheit** auf **Erweitert**

![AD-Rechte-Vererben-02](https://github.com/friedlandreas/Guides/blob/ca3343dda3928e5fcdb018192fc69e5677ed8ae0/images/AD-RechteVererben02.PNG)

Und hier kann jetzt die **Vererbung aktivieren**

![AD-Rechte-Vererben-03](https://github.com/friedlandreas/Guides/blob/ca3343dda3928e5fcdb018192fc69e5677ed8ae0/images/AD-RechteVererben03.PNG)

Wenn danach der Button Vererbung deaktivieren anzeigt sollte es passen

![AD-Rechte-Vererben-04](https://github.com/friedlandreas/Guides/blob/ca3343dda3928e5fcdb018192fc69e5677ed8ae0/images/AD-RechteVererben04.PNG)

Jetzt bischen Warten -> dann sollte das Problem behoben sein 😃
