Eine Standardkonfiguration in Nginx um Anfragen ohne zustaendigen vHost abzufangen:

```console
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        listen 443 ssl default_server;
        listen [::]:443 ssl default_server;
        ssl_reject_handshake on;
        server_name _;

        return 444;
            
        error_log  /var/log/nginx/default_server-error.log;
        access_log /var/log/nginx/default_server-access.log;
}
```
Mit dieser Konfiguration wird keine Webseite mehr ausgegeben, wenn der Server direkt mit der IP angesprochen wird.

Direkt über die IP aufgebaute Verbindungen werden mit Statuscode 444 beantwortet und direkt beendet.

Durch die Direktive **ssl_reject_handshake on;** ist es nicht notwendig ein Zertifikat einzubinden :-)


Qelle: https://www.hosting.de/helpdesk/anleitungen/server/nginx-default-server/