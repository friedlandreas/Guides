Will man in einem Log-File direkt mit grep suchen geht das super einfach:

```console
tail -f /var/log/service.log | grep --line-buffered Suchbegriff
```
