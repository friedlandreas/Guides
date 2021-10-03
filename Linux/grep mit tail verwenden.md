Will man in einem Log-File direkt mit grep suchen geht das super einfach:

```console
tail -f /var/log/service.log | grep --line-buffered Suchbegriff
```
![grep mit tail](https://github.com/friedlandreas/Guides/blob/cd8afd8caed399352b2302bcccf044cdd3bf5f18/images/FMSO-01.png)
