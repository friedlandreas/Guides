Ich verwende den Nginx ja wirklich gerne – auch als Reverse Proxy (z.B. für andere Webserver, CMS, und natürlich auch für Exchange).  
Dort setzte ich auch gerne Clientzertifikate zur Absicherung ein.  
Doch manchmal muss/soll von einer IP der Seitenaufruf aber ohne Clientzertifikat möglich sein…

Ich habe das mit einer **if-Abfrage** gelöst:

```console
if ($remote_addr = 1.2.3.4 ) 
   {
    proxy_pass http://10.10.10.1; 
    break; 
   }
 
if ($ssl_client_verify != "SUCCESS") 
   { return 403; }
```   

Hier wird der Aufruf von der IP 1.2.3.4 direkt auf den Webserver mit der IP 10.10.10.1 weitergeleitet und mit dem **break** wird die weitere Verarbeitung abgebrochen.  
Falls die Anfrage nicht von der IP 1.2.3.4 kommt wird überprüft ob eine Authentifizierung mit einem Clientzertifikat stattgefunden hat – und falls das nicht der Fall ist wird eine 403-Seite gezeigt.  
Vorraussetztung ist, dass in der Clientzertifikateskonfiguration der Wert **ssl_verify_client auf optional steht;**  

Hier ist eine komplette Beispielkonfiguration für einen Reverse Proxy mit Clientzertifikaten inkl. IP-Ausnahme:

```console
server {
    listen                  443 ssl; 
    server_name             www.domain.com;
    ssl_certificate         /etc/nginx/ssl/domain/server.crt; 
    ssl_certificate_key     /etc/nginx/ssl/domain/server.key; 
    ssl_client_certificate  /etc/nginx/ssl/clients/client_ca.pem
    ssl_verify_client       optional;
 
    # Set global proxy settings
    proxy_read_timeout      360;
    proxy_pass_header       Date;
    proxy_pass_header       Server;
    proxy_set_header        Host $host;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        Accept-Encoding "";
 
 
    location /
    {
 
    if ($remote_addr = 1.2.3.4 ) 
       {
        proxy_pass http://10.10.10.1; 
        break; 
       }
 
    if ($ssl_client_verify != "SUCCESS") 
       { return 403; }
 
    proxy_pass http://10.10.10.1;}
 
    error_log /var/log/nginx/domain-error.log;
    access_log /var/log/nginx/domain-access.log;
}
```

Funktioniert einwandfrei 🙂
