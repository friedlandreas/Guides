Man kann macOS wunderbar über das Terminal updaten – und braucht so nicht den Umweg über irgendwelche GUIs (Systemsteuerung bzw. AppStore) gehen 🙂

Mit

 ```console
softwareupdate -lr
```

kan man sich alle verfügbaren empfohlenen Updates anzeigen.

Mit

 ```console
softwareupdate -ir
```
installiert man alle empfohlenen Updates 🙂

![macOS update per softwareudpate](https://github.com/friedlandreas/Guides/blob/749fede9f80f8cdec513f0a068c391ac6a26bba5/images/macos-softwareupdate-cli.png)

Falls man einen Neustart braucht kann der auch gleich mit

 ```console
sudo shutdown -r now
```

erledigt werden 🙂
