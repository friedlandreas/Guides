Will man unter Linux (in meinem Fall Debian) iperf3 als Deamon laufen lassen geht das relativ einfach wie folgt:

Erstmal installieren wir iperf3

```conole
sudo apt install iperf3
```

Danach erstellen wir die Service-Datei für den systemd-Deamon:

```conole
sudo vim /etc/systemd/system/iperf3.service
```

Dort kopieren wir folgendes rein und speichern die Datei:

```conole
[Unit] 
Description=iperf3 

[Service] 
ExecStart=/usr/bin/iperf3 --server 

[Install]
WantedBy=multi-user.target
```

Jetzt können wir den Deamon aktiveren:

```conole
sudo systemctl enable iperf3
```

Jetzt können wir den Deamon starten:

```conole
sudo systemctl start iperf3
```

Überprüfen ob der Dienst läuft:

```conole
sudo systemctl status iperf3
```

Jetzt läuft immer der iperf3-Dienst – auch nach Restart des Severs 🙂
