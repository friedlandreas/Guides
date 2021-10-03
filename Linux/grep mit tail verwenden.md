Will man in einem Log-File direkt mit grep suchen geht das super einfach:

```console
tail -f /var/log/service.log | grep --line-buffered Suchbegriff
```
oder
```console
tail -f /var/log/service.log | egrep --line-buffered Suchbegriff
```
Also zum Beispiel:
```console
tail -f /var/log/nginx/access.log | egrep --line-buffered Ninja
```
![grep mit tail](https://github.com/friedlandreas/Guides/blob/76f859f26b04e7258ba8b0d9b3c16ccd1100264f/images/grep_mit_tail.PNG)
