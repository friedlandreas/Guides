Ich wollte auf einem nginx-Server einen ReverseProxy für Exchange einrichten. Für MAPI-over-HTTP und den Zugriff von Mac-Clients hab ich mich an meine Anleitung gehalten – aber leider scheitert der Start des nginx mit der Fehlermeldung

> unknown directive more_set_input_headers

Für den Teil

```console
more_set_input_headers 'Authorization: $http_authorization';
proxy_set_header Accept-Encoding "";
more_set_headers -s 401 'WWW-Authenticate: Basic realm="exch2016.test.local"';
```

braucht es eine nginx-Erweiterung – das headers-more-nginx-module.

Ob das Modul installiert ist kann mittels

```console
nginx -V
```

![nginx Module anzeigen](https://github.com/friedlandreas/Guides/blob/eae3ff7701af7eea1a37b278c3b1730357b9b280/images/nignx-module-anzeigen.png)

geprüft werden.

Falls es dort nicht zu finden ist kann es einfach entweder mit dem nginx-extras-Paket oder manuell nachinstalliert werden:

```console
sudo apt-get install nginx-extras
```

bzw.

```console
sudo apt-get libnginx-mod-http-headers-more-filter
```

Falls jetzt der Start immer noch nicht funktioniert kann es sein das die Module beim Start nicht geladen werden.

Dazu muss in der **/etc/nginx/nginx.conf** ganz oben (unter pid /run/nginx.pid;)

**include /etc/nginx/modules-enabled/*.conf;**

hinzugefügt werden.

![nginx config](https://github.com/friedlandreas/Guides/blob/eae3ff7701af7eea1a37b278c3b1730357b9b280/images/nginx-nginx-conf.png)

Danach den nginx neustarten – dann sollte es gehen 🙂
