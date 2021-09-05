Ich verwende ja recht gerne den Nginx als ReverseProxy. Aktiviert man allerdings TLS 1.3 in den ssl_protocols – so will der Nginx auch mit dem Backend immer mit TLS 1.3 sprechen. Das kann allerdings z.B. mit älteren IIS-Servern zu Problemen bzw. zu keiner Verbindung führen.

Das Problem kann man mit

```console
proxy_ssl_protocols TLSv1 TLSv1.1;
```

in der Config verhindern. So verwendet der Nginx in diesem Beispiel eben TLS1 oder TLS 1.1 um mit dem Backend zu kommunzieren – mit dem Frontend (also dem Client-Browser) wird dann trotzdem TLS1.3 gepsorchen 🙂
