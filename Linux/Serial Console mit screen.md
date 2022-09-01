Unter Linux benutze ich für Serial Consolen am liebsten **screen**.

### screen installieren
Meistens ist screen nicht per Default installiert. Also erstmal installieren (z.B. unter Fedora)

```console
sudo dnf install screeen
```

### Serial Port rausfinden
Jetzt müssen wir den Port unseres Serial-Ports rausfinden

```console
dmesg | egrep -i --color 'serial|ttyS|ttyUSB'
```
Sieht dann so aus:

![dmseg Ausgabe](https://github.com/friedlandreas/Guides/blob/2604b4d757ef1477697705599393165c2b0e7091/images/Serial-Console-Linux-screen-01.png)

Hier gut zus ehen das mein USB-Apapter das Device **ttyUSB01** zugewiesen bekommen hat.

### screen verwenden 

Jetzt können wir uns mit **screen** connecten. Wichtig: **screen** sollte immer als root/su oder per sudo gestartet werden.

Syntax: screen device baud-rate

also z.B.:

```console
sudo screen /dev/ttyUSB0 38400
```

![screen](https://github.com/friedlandreas/Guides/blob/bf6a0e756873e70ce95ad4e8bcae715b1c10c80a/images/Serial-Console-Linux-screen-02.png)
