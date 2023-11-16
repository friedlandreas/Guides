Einzelne Domains

```console
sudo certbot certonly --manual --preferred-challenges dns -d "www.meineseite.de" 
```

oder auch Wildcard

```console
sudo certbot certonly --manual --preferred-challenges dns -d "*.meineseite.de"
```
