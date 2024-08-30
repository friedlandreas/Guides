Will man einen User erlauben sudo ohne nochmaliger Passwortabfrage auszuführen, geht das relativ einfach :

```console
sudo visudo
```


Am Ende der Datei folgendes hinzufügen:

```console
$USER ALL=(ALL) NOPASSWD: ALL
```


Wobei hier $USER mit dem Usernamen ersetzt werden muss - also z.B.:

```console
friedl ALL=(ALL) NOPASSWD: ALL
```

Sieht dann so aus (hier unter Debian):

![visduo](https://github.com/friedlandreas/Guides/blob/1dff37f6613896a302c6c6576a2ac95fc5a7caae/images/sudo-ohne-passwort-visudo.png)


Nach dem speichern kann der User friedl sudo ohne nochmalige Passwortabfrage ausführen :blush:
