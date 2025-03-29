
Will man ein Zertifikats-Request unter Windows an einer CA einreichen geht das recht einfach per certutil:

Zuerst lassen wir uns die zur Verfügung stehenden Vorlagen anzeigen:

```console
certutil -CATemplates
```
![certutil catemplates](https://github.com/friedlandreas/Guides/blob/ebf28b564985653b73abdf9f10ed6c464f075543/images/certutil-catemplates.PNG)

Dann können wir den Request mit Angabe der gewünschten Vorlage (angegeben wird der erste Name der Vorlage - der Name ohne Leerzeichen 🙂 ) einreichen:

```console
certreq -attrib "CertificateTemplate:{Name-der-Zertifikatvorlage}" -submit {Zertifikatantrag}.req
```

also z.B. :
```console
certreq -attrib "CertificateTemplate:WebServer" -submit c:\temp\cert.req
```

certutil lässt einem auch gleich  die CA auswählen: 

![certutil request submit](https://github.com/friedlandreas/Guides/blob/742bab512df71b34889e55eb82d753dcec26d48a/images/certutil-request-submit-01.PNG)

Wenn die CA das Zertifikat austellt kann es direkt gespeichert werden:

![certutil request submit](https://github.com/friedlandreas/Guides/blob/ebf28b564985653b73abdf9f10ed6c464f075543/images/certutil-request-submit-02.PNG)

Und schon hat man das Zert 😄
