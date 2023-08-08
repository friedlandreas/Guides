Eine einfache Authentifizierung mit Username und Passwort ist auch mit Nginx super einfach zu machen.

Das geht in relativ wenigen einfachen Schritten:

### apache2-utils

Für die einfache Verwaltung der User-Passwort-Datei installieren wir die **apache2-utils** 

```console
sudo apt update
sudo apt install apache2-utils
```

### .htpasswd-Datei

Als nächstes erstellen wir eine htpasswd-Datei (es können mehrer im System erstellt werden :slightly_smiling_face: ) und legen den ersten User (hier im Beispiel benutzer) an:

```console
sudo htpasswd -c /etc/nginx/.htpasswd benutzer
```

### Weitere Benutzer in der htpasswd-Datei anlegen

Weitere Benutzer legt man folgend an:

```console
sudo htpasswd /etc/nginx/.htpasswd andere_benutzer
```

### Aneigen der User in der htpasswd-Datei

Anzeigen kann man die Einträge einfach mit

```console
cat /etc/nginx/.htpasswd
```

Die Datei lässt sich auch einfach bearbeiten (User löschen -> einfach die Zeile löschen)

### Nginx-Config

Jetzt kann in der Nginx-Config-Datei folgender Block hinzugefügt werden

```console
auth_basic "Restricted Content"; 
auth_basic_user_file /etc/nginx/.htpasswd;
```

Man kann den Block entweder direkt im Server-Block einfügen (um die ganze Seite zu schüzten) oder in einer Location (um nur einen Teil - z.B. Admin-Portal - zu schützen) :-)

### Nginx restarten

Jetzt nur noch den Nginx neustarten

```console
sudo systemctl restart nginx
```

### Testen 

Jetzt noch testen und schon sind wir fertig :slightly_smiling_face:

Quelle: https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-22-04
   
