Will man mit einem Nginx eine CRL (Certificate Revocation List) von einer Windows-CA verwenden, muss diese umgewandelt werden - der Nginx kann nämlich mit dem Format nix anfangen....

Umwandeln ist allerdings per Shell ganz einfach:

```console
wget http://windows.cca/ca.crl -O /path/to/ca.crl
openssl crl -in /path/to/ca.crl -inform DER -out /path/to/ca.crl.pem
```

Das kann man auch automatisieren -> z.B. per crontab.


Dann lässt sich diese Datei in der Nginx-Konfiguration per 

```console
ssl_crl /path/to/ca.crl.pem;
```

einbinden :-)
