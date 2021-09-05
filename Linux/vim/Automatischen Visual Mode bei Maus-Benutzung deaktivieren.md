Ich bin ja ein eingefleischter Vim-Benutzer. Doch manchmal öffnet man Vim und es geht der Visual Mode automatisch an weil er erkennt dass man eine Maus benutzt – gerne wenn man mit Putty unter Windows arbeitet.

Ich mag den Visual Mode aber so gar nicht und deaktiviere ihn eigentlich immer.

Das geht einfach wenn man im Vim ist mit:

```console
:set mouse-=a
```

Wenn man es grundsätzlich ausschalten will fügt man einfach folgende Zeile in die vimrc-Datei ( vim ~/.vimrc ) ein:

```console
set mouse-=a
```

Einfügen (oder die Datei erstellen) und speichern. Beim nächsten Start von Vim sollte der Modus deaktiviert sein 🙂
