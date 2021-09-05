Wenn man einen ESXi-Host updaten will und den Update Manager von VMWare nicht verwenden kann oder will, empfehle ich immer das Update mittels dem Offline Bundle.

Das Update mit dem Offline Bundle ist wirklich super einfach und funktioniert eigentlich immer. Ich zeige die Vorgehensweise an einem Upgrade von ESXi 6.1 auf 6.5:

**1) Offline-Bundle hochladen**

**2) Den ESXi-Host in den Wartungsmodus versetzen**

**3) Mit SSH auf den Host verbinden (falls nötig muss der Dienst noch gestartet werden)**

**4) Jetzt geben wir uns alle Profile des Offline Bundle aus**

```console
esxcli software sources profile list -d /vmfs/volumes/datastore1/update-from-esxi6.5-5.5_update02-2068190.zip
```

Meistens wird hier das einfache Standard-Profil benötigt – kommt darauf an welches Profil der Host jetzt hat – das sieht man am einfachsten im VMWare Client

**5) Das entsprechende Profil installieren**

```console
esxcli software profile update -d /vmfs/volumes/datastore1/update-from-esxi6.5-5.5_update02-2068190.zip -p ESXi-6.5.0-20140902001-standard
```

Nach kurzer Wartezeit kommt dann die Ausgabe

![VMWare Upgrade Offline Bundle](https://github.com/friedlandreas/Guides/blob/89ddc80f9b476df7e73ffd5cdea32144b3b2b389/images/UpdateResultOfflineBundle.png)

Danach den Host rebooten

```console
reboot now
```

**6) Wartungsmodus beenden**

Jetzt noch den Wartungsmodus beenden und schon sind wir fertig 🙂
