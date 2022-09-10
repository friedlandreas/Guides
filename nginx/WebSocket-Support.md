Um bei einem nginx den Support für WebSockets (z.B. für Bitwarden) einzuschalten müssen folgende Header in der Konfiguration hinzugefügt werden

```code
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "Upgrade";
```

Also als Beispiel sieht das dann so aus:

```code

location / {
    proxy_pass http://backend;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "Upgrade";
    proxy_set_header Host $host;
}

```

nginx restarten und fertig :-)

Quelle: https://www.nginx.com/blog/websocket-nginx/
