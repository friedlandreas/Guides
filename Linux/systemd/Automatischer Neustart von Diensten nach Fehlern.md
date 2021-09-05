Mit systemd kann man Dienste bei Fehlern automatisch restarten lassen.

Zuerst checkt man welche Konfig-Datei den Dienst steuert – die Datei steht unter loaded:

```console
systemctl status yourdaemon
```
![systemctl status nginx](https://github.com/friedlandreas/Guides/blob/f2bffbe1e918e02a3f8d5f0319718c15eec5e91a/images/systemd-restart-after-failure-01.png)

Hier in dem Beispiel also /lib/systemd/system/nginx.service.

Diese öffnen wir

```console
vim /lib/systemd/system/nginx.service
```

Und fügen unter **[service]** folgendes ein:

```console
Restart=on-failure
RestartSec=3s
```

Dann sieht das folgendermaßen aus:

![systemd reboot config](https://github.com/friedlandreas/Guides/blob/f2bffbe1e918e02a3f8d5f0319718c15eec5e91a/images/systemd-restart-after-failure-02.png)

Danach muss man den Dienst nochmal neu laden

```console
systemctl daemon-reload
```
