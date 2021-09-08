Eine Domäne

```console
sudo certbot certonly --webroot -w /var/www/letsencrypt -d meineseite.de 
```

oder mehrere Domänen

```console
sudo certbot certonly --webroot -w /var/www/letsencrypt -d meineseite.de -d www.meineseite.de
```
