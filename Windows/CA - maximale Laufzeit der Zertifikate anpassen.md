Will man auf einer Windows-CA Zertifikate mit einer längeren Laufzeit als den Standardwert von zwei Jahren ausstellen muss man das auf dem CA-Server anpassen.

Dazu öffnen wir 

```console
regedit
```

und gehen zu 

```console
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\CertSvc\Configuration\CA-NAME
```

dort passen wir die Werte

```console
ValidityPeriodUnits
```

und

```console
ValidityPeriod
```
an. 

![CA-Laufzeiteinstellungen](https://github.com/friedlandreas/Guides/blob/1a29ae4495813dd2335fdbb1bd903fb84cd83218/images/CA-max-Laufzeit.PNG)

Ein **ValidityPeriodUnits** mit **4** und **ValidityPeriod** mit **Years** mach also eine **Maximallaufzeit von 4 Jahren**.

Nach einem Neustart des Windows-CA-Dienstes könnnen Zertifikate mit längerer Laufzeit ausgestellt werden :-)
