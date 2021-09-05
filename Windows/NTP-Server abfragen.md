Ich wollte auf einem Windows-System testen ob ich einen NTP-Server erreiche und ob mir dieser Server auch eine Zeit zurückgibt.

Das kann man ganz einfach per w32tm-Befehl testen:

```console
w32tm.exe /stripchart /computer:ip.addresse.oder.dnsname /dataonly /samples:1
```

Also z.B. mit IP

```console
w32tm.exe /stripchart /computer:172.17.9.78 /dataonly /samples:1
```

oder auch per DNS-Namen:

```console
w32tm.exe /stripchart /computer:ptbtime1.ptb.de /dataonly /samples:1
```

![NTP-Abfrage unter Windows](https://github.com/friedlandreas/Guides/blob/5521fe50b545f136f133376cd34fa704f6f4a5dd/images/ntp-abfragen-windows.png)
