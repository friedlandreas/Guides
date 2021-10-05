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
