Wenn man Windows klonen und verteilen will, verwendet man das sysprep um das Windows für die Verteilung vorzubereiten.

Das sieht bei mir so aus:

![sysprep](https://github.com/friedlandreas/Guides/blob/7d59078fc5fa62c4b1c6b3594eb12bbe3f7327fd/images/sysprep.jpg)

Das **„Verallgemeinern“** oder auch **„generalize“** macht folgendes:

- Alle Einträge in der Ereignisanzeige werden gelöscht;
- Alle Wiederherstellungspunkte werden gelöscht;
- es deaktiviert das Konto des lokalen Administrators und löscht sein Profil;
- Security Identifier (SID) erneuern;
- Plug- und Play-Gerätetreiber, die während der Installation hinzugefügt wurden; werden gelöscht
- die Mitgliedschaft in Domänen und wechselt den PC in die Arbeitsgruppe „Workgroup“.

Das sind alles Dinge die man eigentlich alle immer haben will – außer das löschen der Gerätetreiber. Diese will man oft behalten, weil man z.B. das Image auf baugleiche Rechner verteilen will und dort dann z.B. der Grafiktreiber fehlt und nachinstalliert werden muss.

Dieses Verhalten lässt sich allerdings ganz leicht durch einen Eintrag in der Registry ausschalten:

Unter

```console
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\Sysprep\Settings\sppnp
```

setzt man den DWORD-Wert **PersistAllDeviceInstalls** auf **1**

Wenn man danach das Sysprep laufen lässt, sind im Image alle Treiber enthalten!
