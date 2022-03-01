Mit der **rc.local** kann man unter Debian Befehle/Scripte beim Starten des Servers ausführen lassen.   
Seit Debian 9 gibt es diese Datei jedoch nicht mehr. Der systemd-Daemon ist aber nach wie vor vorhanden 🙂  
Um das ausführen der **rc.local** wieder aktivieren geht man wie folgt vor:

Die Datei **/etc/rc.local** erstellen:

```console
nano /etc/rc.local
```

Folgender Inhalt sollte die Datei haben:

```sh
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

exit 0
```

und abspeichern. Falls man gleich Befehle reinschreiben will -> die Datei muss immer mit **exit 0** enden!

Jetzt machen wir die Datei ausführbar:

```console
chmod +x /etc/rc.local
```

Jetzt starten wir die systemd-Daemon:

```console
systemctl daemon-reload
```

und starten den für die rc.local-verantwortlichen Daemon

```console
systemctl start rc-local
```

Mit

```console
systemctl status rc-local
```

kann man den Status überprüfen - sollte so aussehen:

![rc.local status](https://github.com/friedlandreas/Guides/blob/5bcde2771b72200a81bbbefc4be794da5caa5f6b/images/rc.local-debian.PNG)

Nach einem Reboot werden jetzt die Befehle/Scripte in der **rc.local** ausgeführt 🙂

Quelle: https://blog.wijman.net/enable-rc-local-in-debian-bullseye/
