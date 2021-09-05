Wenn man einen Nginx als ReverseProxy für einen Upstream-Server verwendet der SNI verwendet (egal ob Apache, IIS, etc) , muss man dies in der Konfiguration des Nginx beachten – sonst klappt die Verbindung nicht und wirft 502-Errors.

Die Konfiguration ist allerdings ganz einfach:

```console
location / {
    proxy_pass https://upstream-server;
    proxy_ssl_name $host;
    proxy_ssl_server_name on;
  }
```

So wird dem Upstream-Server „sauber“ mitgeteilt welche Webseite aufgerufen werden soll.

Und schon klappt der Aufruf über einen Nginx ReverseProxy 🙂

Hier eine kleine Beispiel-Komplett-Konfig:

```console
server {
    listen                  443 ssl; 
    server_name             www.domain.com;
    ssl_certificate         /etc/nginx/ssl/domain/server.crt; 
    ssl_certificate_key     /etc/nginx/ssl/domain/server.key; 
 
    proxy_read_timeout      360;
    proxy_pass_header       Date;
    proxy_pass_header       Server;
    proxy_set_header        Host $host;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        Accept-Encoding "";
 
 
    location / {
    proxy_pass https://1.2.3.4;
    proxy_ssl_name $host;
    proxy_ssl_server_name on;
    }
 
    error_log /var/log/nginx/domain-error.log;
    access_log /var/log/nginx/domain-access.log;
}
```
