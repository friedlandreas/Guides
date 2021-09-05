Ich hatte bei einem Nginx als ReverseProxy das Problem das dieser oft in Fehler 

> upstream timed out (110: Connection timed out)  
 
lief und so die Seite nicht funktionierte – der User bekam dann eine **504** Fehlerseite.

Ich habe das mit dem hinzufügen der beiden Zeilen

```console
proxy_http_version 1.1;
proxy_set_header Connection „“;
```

in der Config gefixt – danach lief alles ohne Probleme.
