Wenn ich eine Maus am Notebook benutze möchte ich das mein Touchpad deaktiviert wird – unter GNOME gibts da aber standardmäßig keine Möglichkeit das in den Einstellungen entsprechend zu konfigurieren.

Allerdings kann man das per gsettings in der Shell setzen:

```console
gsettings set org.gnome.desktop.peripherals.touchpad send-events disabled-on-external-mouse
```

Jetzt wird brav das Touchpad deaktiviert wenn eine Maus aktiv ist – und auch brav wieder aktiviert wenn man die Maus absteckt bzw. ausschaltet -> egal ob USB oder Bluetooth 🙂

![GNOME Touchpad bei angeschlossener Maus deaktivieren](https://github.com/friedlandreas/guides/blob/a2751b0f4c57c15cfbf777603876f4a60ade974d/images/GNOME-Maus.png)

Um zu checken ob der Wert gesetzt ist:

```console
gsettings get org.gnome.desktop.peripherals.touchpad send-events
```

Will man wieder das Standardverhalten wieder herstellen:

```console
gsettings set org.gnome.desktop.peripherals.touchpad send-events enabled
```
