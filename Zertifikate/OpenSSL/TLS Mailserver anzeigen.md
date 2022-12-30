Um bei einem Mail-Server die TLS-Konfig zu testen kann mit

```console
 sudo openssl s_client -starttls smtp -connect mailserver:587
```

abgefragt werden 🙂

Kommen Zertifikate, TLS-Version, etc als Ausgabe - alles was man braucht 😏
