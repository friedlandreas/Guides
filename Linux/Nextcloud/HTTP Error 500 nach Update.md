Ich hatte das Problem das nach dem Update bzw. Upgrade (über den Web-Updater) meine Nextcloud nicht mehr erreichbar war und

> HTTP ERROR 500

ausgab.

Lösen konnte ich das Problem über die Shell (der Pfad ist euer Nextcloud-Verzeichnis):

```consol
cd /var/www/nextcloud

sudo -u www-data php occ upgrade
````

Danach lief wieder alles 🙂
