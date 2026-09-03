## Schritt 1: Private Key
```shell
openssl genrsa -out key.pem 2048
```

## Schritt 2: CSR (Certificate Signing Request)
```shell
openssl req -new -key key.pem -out cert.csr
```

```
Enter pass phrase for example.com.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:XX
State or Province Name (full name) []:State
Locality Name (eg, city) [Default City]:City
Organization Name (eg, company) [Default Company Ltd]:Company
Organizational Unit Name (eg, section) []:BU
Common Name (eg, your name or your server's hostname) []:*.example.com
Email Address []:admin@example.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

## Step 3: Konfig-Datei fuer SAN
```shell
touch v3.ext
```

Dateiinhalt
```
subjectKeyIdentifier   = hash
authorityKeyIdentifier = keyid:always,issuer:always
keyUsage               = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment, keyAgreement, keyCertSign
subjectAltName         = DNS:example.com, DNS:*.example.com
issuerAltName          = issuer:copy
```

## Step 4: Generating a Self-Signed Certificate
```shell
openssl x509 -req -in cert.csr -signkey key.pem -out cert.pem -days 365 -sha256 -extfile v3.ext
```
