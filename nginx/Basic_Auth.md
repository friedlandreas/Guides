Will man mit einem Nginx eine einfache Authentifizierung mittels Usernamen und Passwort einsetzten geht das mit dem auth_basic-Module:

Beispiel:

```console
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/.htpasswd;

```

# Passwort-Datei

Am einfachsten lässt sich die nötige Passwort-Datei mittels den Apache-Utils verwalten

## Installieren

Zum installieren (z.B. auf einem Debian-System):

```console
sudo apt-get update
sudo apt-get install apache2-utils
```


## Erstellen

Zum erstellen der Datei:

```console
sudo htpasswd -c /etc/nginx/.htpasswd username
```
So wird die Datei erstellt und das Passwort für den ersten Benutzer (username) nachgefragt

## User hinzufügen

Weitere User hinzufügen:

```console
sudo htpasswd /etc/nginx/.htpasswd weiterer-username
```
## User löschen

Einen User aus der Datei löschen
```console
sudo htpasswd -D /etc/nginx/.htpasswd zuloeschenderuser
```


# Nginx-Konfiguration

Jetzt kann die Konfiguration in der Nginx-Konfig vorgenommen werden

## Basic_Auth Standard-Konfig

```console
server {
    listen 80;
    listen [::]:80;

    server_name admin.test.test;

    location / {
        auth_basic "Restricted Content";
        auth_basic_user_file /etc/nginx/.htpasswd;

	      proxy_pass http://192.168.178.1;
    }
}
```

## Basic_Auth mit IP-Ausnamhmen

```console
server {
    listen 80;
    listen [::]:80;

    server_name admin.test.test;

    location / {
     	  satisfy any;
        allow 10.10.10.0/24;
        allow 1.2.3.4;
        deny all;
        auth_basic "Restricted Content";
        auth_basic_user_file /etc/nginx/.htpasswd;

	      proxy_pass http://192.168.178.1;
    }
}
```

Hier wird die Basic-Auth nur ausgeführt wenn die Anfrage nicht von den IPs in den allow-Zeilen kommen -> heißt von 1.2.3.4 kommt keine Abfrage - bei anderen kommt die Basic-Auth
