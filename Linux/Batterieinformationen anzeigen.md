Unter Linux (in meinem Fall Fedora) lassen sich recht einfach Infos zu den Batterien im Notebook anzeigen

### Batterien anzeigen

```console
sudo upower -e
```

### Infos anzeigen

```console
sudo upower -i /org/freedesktop/UPower/devices/battery_CMB1
```
