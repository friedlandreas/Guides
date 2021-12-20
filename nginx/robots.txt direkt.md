Will man direkt eine robots.txt im nginx setzen geht das mit:

```console
location = /robots.txt { return 200 "User-agent: *\nDisallow: /\n"; }
```
bzw. mit Content-Typ-Angabe:

```console
location = /robots.txt {
   add_header Content-Type text/plain;
   return 200 "User-agent: *\nDisallow: /\n";
}
```

Qelle: https://newbedev.com/how-to-set-robots-txt-globally-in-nginx-for-all-virtual-hosts
