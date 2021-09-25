Will man ein PFX-Format in .key und .pem-Datei umwandeln geht das mit OpenSSL ganz einfach:

Das eigentliche Zertifikat:

```console
openssl pkcs12 -in cert.pfx -clcerts -nokeys | openssl x509 -out cert.pem
```

Den Privat Key bekommt man mit:

```console
openssl pkcs12 -in cert.pfx -nocerts -nodes | openssl rsa -out cert.key 
```

Fertig :-)
