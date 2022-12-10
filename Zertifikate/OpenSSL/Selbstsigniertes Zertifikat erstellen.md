Um ein selbstsignierte Zertifikate zu erstellen reicht folgender Befehl:

```console
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365 -nodes
```

Nach den Abfragen hat man schon das Zertifikat 🙂

Will man die Abfragen auch gleich mitgeben - z.B. für Scripte, etc - hängt man (angepasst natürlich 😉)

```console
-subj "/C=DE/ST=Bayern/L=Musterhausen/O=Musterfirma/OU=IT/CN=*.musterfirma.de"
```

an 🙂

Quelle: https://stackoverflow.com/questions/10175812/how-to-generate-a-self-signed-ssl-certificate-using-openssl
