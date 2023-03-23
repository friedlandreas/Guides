Will man von einer p12- bzw. PFX-Datei das Ablaufdatum anzeigen geht das recht einfach:

```console
openssl pkcs12 -in cert.pfx -nokeys | openssl x509 -noout -enddate
```

Wenn man gleich das Passwort mitgeben will

```console
openssl pkcs12 -in cert.p12 -nokeys -passin pass:'SuperSicheresPasswort' | openssl x509 -noout -enddate
```
![p12 Enddatum anzeigen](https://github.com/friedlandreas/Guides/blob/6a45284c394a9db616063abca1b22faede1e371f/images/p12-enddatum-anzeigen.PNG)
