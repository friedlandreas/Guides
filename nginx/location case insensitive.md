Um bei einem nginx eine location auf case insensitive zu "stellen" muss die location folgende aussehen

```console
location ~* ^/location {
blabliblub;}
```
Beispiel: alle Varianten von OWA blocken:
```console
location ~* ^/owa {
deny all;}
```

Beispiel: alle Varianten von OWA weiterleiten:
```console
location ~* ^/owa {
proxy_pass https://1.2.3.4;}
```
