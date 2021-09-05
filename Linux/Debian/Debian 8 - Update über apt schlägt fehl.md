Will man ein Debian 8 mit **apt-get update** oder **apt update** updaten und schlägt dies mit einer Meldung wie dieser fehl

> Fehl http://ftp.debian.org jessie-backports/main amd64 Packages 404 Not Found [IP: 130.89.148.12 80] W: Fehlschlag beim Holen von http://ftp.debian.org/debian/dists/jessie-backports/main/binary-amd64/Packages 404 Not Found [IP: 130.89.148.12 80] E: Einige Indexdateien konnten nicht heruntergeladen werden. Sie wurden ignoriert oder alte an ihrer Stelle benutzt.

liegt das daran, dass Debian im März 2019 die Sourcen verschoben haben – und die alten in der sources.list nicht mehr funktionieren.

Man muss jetzt nur die **sources.list** Datei in **/etc/apt/** auf die neuen Quellen ändern:

```console
deb http://security.debian.org/ jessie/updates main
deb-src http://security.debian.org/ jessie/updates main

deb http://archive.debian.org/debian/ jessie-backports main
deb-src http://archive.debian.org/debian/ jessie-backports main

deb http://archive.debian.org/debian/ jessie main contrib non-free
deb-src http://archive.debian.org/debian/ jessie main contrib non-free
```

Und zusätzlich muss noch folgender Befehl auf der Shell ausführt werden:

```console
echo "Acquire::Check-Valid-Until false;" | tee -a /etc/apt/apt.conf.d/10-nocheckvalid
```

Jetzt sollte einem gepflegten **apt update && apt upgrade -y** nichts mehr im Wege stehen 🙂
