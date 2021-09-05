Manchmal muss bzw. will man alle Ereignisprotokolle auf einem Windows-System löschen.

Am einfachsten geht das mit Hilfe der Powershell.

Einfach eine Powershell als Administrator öffnen und mit

```console
wevtutil el | Foreach-Object {wevtutil cl „$_“}
```

alle Ereignisprotokolle löschen.

![Powershell alle Logs loeschen](https://github.com/friedlandreas/Guides/blob/79a9dc10c9a5b60411363f477776350725893047/images/Powershell-Clear-all-EventLogs.png)

Tipp: Will man nur bestimmte Ereignisprotokolle löschen geht das ebenfalls ganz einfach:

Mit

```console
wevtutil el
```

kann man sich die Namen aller verfügbaren Ereignisprotokolle anzeigen lassen.

![Powershell alle Logs loeschen](https://github.com/friedlandreas/Guides/blob/79a9dc10c9a5b60411363f477776350725893047/images/Powershell-Clear-all-EventLogs2.png)

und mit

```console
wevtutil cl NAMEdesEREIGNISPROTOLOLLS
```

löscht man es.

Ein

```console
wevtutil cl application
```

löscht also das Ereignisprotokoll Anwendung.
