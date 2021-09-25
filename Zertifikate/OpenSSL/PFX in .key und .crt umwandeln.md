Ich muss öfters mal Zerifikate im PFX-Format umwandeln in .key und .crt-Datein für z.B. den WebServer NGINX umwandeln. Das geht mit OpenSSL ganz einfach:

Das eigentliche Zertifikat:

```console
openssl pkcs12 -in cert.pfx -clcerts -nokeys -out cert.crt
```

Den Privat Key bekommt man mit:

```console
openssl pkcs12 -in cert.pfx -nocerts -out cert-encrypted.key
openssl rsa -in cert-encrypted.key -out cert.key
```

Der zweite Befehl beim Privat Key konvertieren ist dafür da, dass z.B. beim starten des WebServers nicht nach der PEM pass phrase gefragt wird (beim NGINX kommt beim starten sonst der Fehler: Starting nginx: Enter PEM pass phrase:)
