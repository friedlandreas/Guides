Wenn man ADFS über einen nginx-ReverseProxy betreiben will geht das wunderbar mit folgender Konfig:

```console
server {
        listen 443 ssl;
        listen [::]:443 ssl;

        server_name adfs.domain.de;

        # SSL-Einstellungen
       ssl_certificate /etc/nginx/certs/domain.de.bundle.crt;
       ssl_certificate_key /etc/nginx/certs/domain.de.key;

        proxy_ssl_session_reuse off;
        proxy_buffering off;
        ssl_session_cache off;

        location / {
        proxy_ssl_server_name on;
        proxy_ssl_name adfs.domain.de;
        proxy_pass https://10.11.12.170;
        proxy_set_header Host adfs.domain.de;
        proxy_set_header X-MS-Proxy 10.11.21.58;
        proxy_http_version 1.1;
        proxy_redirect off;
        }

        #Logging
        error_log /var/log/nginx/adfs.domain.de-error.log;
        access_log /var/log/nginx/adfs.domain.de-access.log;
}
```

Erklärung zu den IPs:   
10.11.21.58 ist der nginx-Server  
10.11.12.170 ist der ADFS-Server  

Man kann da natürlich noch optimieren - aber so funktioniert es schon mal sauber 😄

Quelle: https://forum.nginx.org/read.php?11,274340
