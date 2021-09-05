Unter iOS speichert man ja mittlerweile seine Fotos im HEIC-Format.

Will man aber seine Fotos weitergeben und weiß nicht ob das Betriebssystem des Empfänger HEIC bzw. HEIF unterstütz empfiehlt es sich die Fotos in das JPEG-Format umzuwandeln.

Auf dem Mac geht das wunderbar mit **Imagemagick**.

Zuerst Installieren wir **Imagemagick** per **brew**:

```console
brew install imagemagick
```

Danach kann entweder ein einzelnes Foto konvertiert werden:

```console
magick convert foto.HEIC foto.jpg
```

Oder alle Fotos in dem aktuellen Ordner

```console
magick mogrify -monitor -format jpg *.heic
```
