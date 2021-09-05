Wenn man am Nginx die SSL-Ciphers updatet und danach gehen manche ältere Client-Zertifikate nicht mehr, liegt das daran das auch für die Client-Zertifikate die Ciphers gelten die unter ssl_ciphers konfiguriert sind – und ist das z.B. sha1RSA nicht mehr drin (hoffentlich 😉 ) werden auch Client-Zertifikate die mit sha1RSA nicht mehr akzeptiert.

Im Log taucht dann folgender Fehler auf:

> client SSL certificate verify error: (68:CA signature digest algorithm too weak)

und der Client bekommt

> 400 Bad Request The SSL certificate error

Um das Problem zu lösen muss man **@SECLEVEL=0** an seine **ssl_ciphers** anhängen – z.B. :

```console
ssl_ciphers 'HIGH:!aNULL:!MD5@SECLEVEL=0';
```

Danach werden die Client-Zertifikate wieder akzeptiert – die Sicherheit der eigentlichen SSL-Verbindung ist hiervon nicht betroffen 🙂
