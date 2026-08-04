
Will man unter Windows die CA einer Windows-Domäne rausfinden geht das recht einfach per certutil:


```console
certutil -config - -ping
```

Dann taucht eine Liste an verfügbaren CAs auf :-)

![certutil ping ca](https://github.com/friedlandreas/Guides/blob/936dcfda12ef79d703020d59576507a3e83cefd9/images/certutil-ca-ping-01.PNG)

und nach der Auswahl der CA gibt's dann noch Infos der CA :-)

![certutil ping ca](https://github.com/friedlandreas/Guides/blob/936dcfda12ef79d703020d59576507a3e83cefd9/images/certutil-ca-ping-02.PNG)
