Manche Anwendungen ignorieren den eingestellten Dark Mode (Erscheinungsbild Dunkel) auf meinem Fedora.

Sieht dann so aus:

![GNOME Dark Mode mit hellen Apps](https://github.com/friedlandreas/Guides/blob/e3329a959eef96f1ed7f705a77a8c323ee6d77c2/images/GNOME-DarkMode-Mixed.PNG)

Wenn man es gerne konsistent will geht das über gsettings per Terminal:

```console
gsettings set org.gnome.desktop.interface gtk-theme Adwaita-dark
```

![gsettings](https://github.com/friedlandreas/Guides/blob/fa6071a6a99e2ea168615f05f78cbd1e508f6bd3/images/GNOME-DarkMode-gsettings.PNG)

Und dann sieht das schön konsitent aus :

![GNOME Dark Mode](https://github.com/friedlandreas/Guides/blob/fa6071a6a99e2ea168615f05f78cbd1e508f6bd3/images/GNOME-DarkMode.PNG)

:-)

