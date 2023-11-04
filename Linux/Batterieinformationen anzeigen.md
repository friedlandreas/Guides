Unter Linux (in meinem Fall Fedora) lassen sich recht einfach Infos zu den Batterien im Notebook anzeigen:

### Batterien anzeigen

```console
sudo upower -e
```

### Infos anzeigen

```console
sudo upower -i /org/freedesktop/UPower/devices/battery_CMB1
```

### Beispiel
![Batterieinfos Fedora](https://github.com/friedlandreas/Guides/blob/d00fb7ec6ea095236605a00b22c409b8ce69af93/images/Batterieinfos-Fedora.png)
