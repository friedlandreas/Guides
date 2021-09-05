Hat man eine Zertifikats-Datei (cert, pem oder ähnliches) und die dazugehörige KEY-Datei ist es ziemlich einfach daraus eine PFX-Datei zu erstellen – um z.B. das Zertifikat einfach in einem IIS zu installieren.

mit folgendem Befehl konvertiert man:

```console
openssl pkcs12 -inkey cert.key -in cert.cert -export -out cert.pfx
```

nur noch ein Export-Kennwort eingeben – fertig 🙂
