Bei einigen Zertifikaten die im Nginx verwendet werden, ist es notwendig die gesamte Zertifikatskette in dem Zertifikat mit anzugeben.

Das geht super einfach mit **cat** auf der Konsole:

```console
cat domain.tld.crt sub-ca.cer > domain-bundle.crt
```

Erst also das eigentliche Zertifikat für die Domäne (domain.tld) – dann die Zwischenzertifizierungsstelle (sub-ca). Die Stammzertifizierungsstelle (Root-CA) wird meistens nicht benötigt.

Manchmal muss man aber doch auch das Root-CA mit in Kette mit aufnehmen (z.B. bei Zertifikate einer eigenen CA) – dann wäre es:

```console
cat domain.tld.crt sub-ca.cer root-ca.cer > domain-bundle.crt
```

Erst also das eigentliche Zertifikat für die Domäne (domain.tld) – dann die Zwischenzertifizierungsstelle (sub-ca) und am Schluss die Stammzertifizierungsstelle (root-ca).

Wenn man die Zertifikate von Windows-Systemen bekommt, sollte man alle vorher mit

```console
openssl x509 -inform der -in certificate.cer -out certificate.pem
```

umwandeln und dann eben mit

```console
cat domain.tld.pem sub-ca.pem root-ca.pem > domain-bundle.crt
```

weiterverarbeiten.

In der Nginx-Config jetzt enfach das bundle.crt in der Zeile

```console
ssl_certificate /etc/nginx/ssl/domain-bundle.crt;
```

angeben und nginx dann neustarten.
