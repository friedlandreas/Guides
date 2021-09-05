Ich hatte das Problem eine Seite bzw. Unterseite die unter einem Nginx als ReverseProxy lief so zu konfigurieren, dass diese sich von jeder Seite einbinden lassen lies. Dies verhindern aber eigentlich die sehr sinnvollen X-Frame-Options.

Diese lassen sich aber einfach mit **proxy_hide_header X-Frame-Options** für eine Seite oder auch nur für Unterseiten deaktivieren – hier ein Beispiel für eine Unterseite:

```console
location /api {
    proxy_pass https://1.2.3.4/api;
    proxy_hide_header X-Frame-Options;
}
```

Nach einem Reload oder Restart des Nginx klappte mit der Einbindung 🙂
