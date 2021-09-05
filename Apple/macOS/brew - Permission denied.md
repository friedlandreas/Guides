Ich hatte das Problem das beim ausführen von **git** bzw. **brew update** die folgende Meldung ausgegeben wurde:

> warning: unable to access ‚/Users/schaloml/.config/git/attributes‘: Permission denied


Um die fehlenden bzw. falschen Berechtigungen zu fixen muss man

```console sudo chown -R username .config ``` 

ausführen. Danach lief alles wieder sauber durch 🙂
