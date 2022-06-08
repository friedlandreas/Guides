Will man eine PFX-Datei in eine PEM-Datei umwandeln in der der Key und Zertifikat enthalten sind (manche Software will das so :-/ ) geht das mit OpenSSL ganz einfach:

Ohne Passwort-Schutz:

```console
openssl pkcs12 -in cert.pfx -out cert.pem -nodes
```

Mit Passwort-Schutz

```console
openssl pkcs12 -in cert.pfx -out cert.pem 
```

Fertig :-)

Quelle: https://stackoverflow.com/questions/15144046/converting-pkcs12-certificate-into-pem-using-openssl
