# Ausgangslage

Die Exchange-CUs vom Mai 2022 haben in der ECP fast alle Funktionen für Zertifikate entfernt:

![ECP](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-01.png)

Die Zertifikate lassen sich nur noch anzeigen, Dienste zuordnen und löschen

![ECP - Zertifikate](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-02.png)

Nur noch das erstellen eines selbstsigniertes Zertifikats ist über die ECP noch möglich - alle anderen Funktonen (Erstellen, Verlängern, etc) stehen nur noch über Powershell-Befehle in der Exchange Management Shell zur Verfügung.

# Zertifikate per Powershell (Exchange-Verwaltungsshell) 

Nachfolgende eine Übersicht wie man über die Powershell (Exchange-Verwaltungsshell) die Zertifikate managen kann 

## Anzeigen

In der Exchange Management Shell kann ich mir alle Inforamationen der Zertifikate anzeigen lassen - auch filtern (z.B. nach Verwendung oder Ablaufdatum, etc) ist möglich 

### Alle Zertifikate

Um eine Übersicht aller vorhandenen Zertifikate zu erhalten 

```console
Get-ExchangeCertificate | Format-List FriendlyName,Subject,CertificateDomains,Thumbprint,NotBefore,NotAfter,IsSelfSigned
Ausgabe sieht dann wie folgt aus
```
![Exchange - Alle Zertifikate](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-03.png)

Es werden hier alle wichtigen Infos angezeigt → der Thumbprint (den brauchen wir für weitere Aktionen), Ablaufdatum, Domänen, etc.

### Verwendete Zertifikate

Um eine Übersicht aller verwendeter Zertifikate inkl. der Dienstzuordnung zu erhalten 
```console
Get-ExchangeCertificate | where {$_.services -ne "None"} | Format-List FriendlyName,Subject,CertificateDomains,Thumbprint,NotBefore,NotAfter,IsSelfSigned,Services
```
Ausgabe sieht dann wie folgt aus
![Exchange - Verwendete Zertifikate](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-04.png)

Es werden hier alle wichtigen Infos angezeigt → der Thumbprint (den brauchen wir für weitere Aktionen), Service-Bindung, Ablaufdatum, Domänen, etc

## Exportieren

Um ein Exchange-Zertifikat zu exportieren muss man folgende zwei Befehle verwenden:

```console
$bincert = Export-ExchangeCertificate -BinaryEncoded -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Password (ConvertTo-SecureString -String 'cert123' -AsPlainText -Force)
[System.IO.File]::WriteAllBytes('C:\Temp\Exchange-cert.pfx', $bincert.FileData)
```
Den Thumbprint (5113ae0233a72fccb75b1d0198628675333d010e), Passwort (cert123) und natürlich den Pfad und Namen (C:\Temp\Exchange-cert.pfx) anpassen (Lächeln)

So sieht das dann aus:

![Exchange - Zertifikate exportieren ](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-05.png)

> **Warning**
> Der Pfad (in meinem Beispiel c:\Temp ) muss vorher vorhanden sein  - sonst gibts folgende Fehlermeldung:
> ![Exchange - Zertifikate exportieren - Fehler ](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-06.png)
> Dann einfach den Pfad erstellen und den System.io.file-Befehl nochmal ausführen (Lächeln)

## Importieren

Um ein Zertifikat (im PFX-Format vorliegend) auf dem Exchange zu importieren braucht man folgenden Befehl :
```console
Import-ExchangeCertificate -PrivateKeyExportable $true -Server $env:computername -FileData ([System.IO.File]::ReadAllBytes('\\localhost\c$\temp\Exchange-cert.pfx')) -Password (ConvertTo-SecureString -String 'cert123' -AsPlainText -Force)
```

Das Passwort (cert123) und natürlich den UNC-Pfad und Namen (\\localhost\c$\temp\Exchange-cert.pfx) anpassen (Lächeln)

Pfad bitte immer im UNC-Format!

Sieht dann so aus:

![Exchange - Zertifikate importieren](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-07.png)

## Löschen

Um ein Exchange-Zertifikat zu löschen muss man folgenden Befehle verwenden:
```console
Remove-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e
```
Den Thumbprint (5113ae0233a72fccb75b1d0198628675333d010e) natürlich anpassen (Lächeln)

So sieht das dann aus:

![Exchange - Zertifikate löschen](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-07.png)

## Dienste zuweisen
Um ein Zertifikat die Dienste zuzuweisen bzw. den Diensten ein Zertifikat zuzuweisen geht recht einfach mit folgenden Befehl:
```console
Enable-ExchangeCertificate -Thumbprint 434AC224C8459924B26521298CE8834C514856AB -Services POP,IMAP,IIS,SMTP
```
Davor wie vorher berschrieben den Thumbprint des gewünschten Zertifikat holen! 

![Exchange - Zertifikate Dienste zuweisen 01](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-08.png)
![Exchange - Zertifikate Dienste zuweisen 02](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-09.png)

Prüfen:

![Exchange - Zertifikate Dienste zuweisen 03](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-10.png)

> **Warning**
> Im IIS die Bindungen prüfen → Frontend (Default Web Site) und Backend (Exchange Back End) sollten auf das neue Zertifikat gesetzt sein. Beim Backend muss meistens nochmal manuell das Zertifikat gesetzt werden!

## Verlängern

Um Zertifikate zu verlängern muss folgende Prozedur befolgt werden:

Zu verlängerndes Zertifikat anzeigen:
```console
Get-ExchangeCertificate | where {$_.Status -eq "Valid" -and $_.IsSelfSigned -eq $false} | Format-List FriendlyName,Subject,CertificateDomains,Thumbprint,NotBefore,NotAfter
```
![Exchange - Zertifikate verlängern 01](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-11.png)

Jetzt erstellen wir mit dem Thumbprint des zu verlängernden Zertifikats ein Request mit diesen beiden Befehlen
```console
$txtrequest = Get-ExchangeCertificate -Thumbprint 5DB9879E38E36BCB60B761E29794392B23D1C054 | New-ExchangeCertificate -PrivateKeyExportable $true -GenerateRequest
[System.IO.File]::WriteAllBytes('\\localhost\c$\Temp\Exchange-cert.req', [System.Text.Encoding]::Unicode.GetBytes($txtrequest))
```
Wie immer: Thumbprint und UNC-Pfad anpassen 😄

Sieh dann so aus:

![Exchange - Zertifikate verlängern 02](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-12.png)

Jetzt kann der Request in der CA eingereicht werden und das erhaltene Zertifikat am Exchange-Server gespeichert werden.

Wenn wir jetzt ein neues Zertifikat haben können wir dies jetzt importieren um den Request abzuschließen
```console
Import-ExchangeCertificate -PrivateKeyExportable $true -FileData ([System.IO.File]::ReadAllBytes('\\localhost\c$\Temp\Exchange-cert.cer'))
```
Sieht dann so aus:
![Exchange - Zertifikate verlängern 03](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-13.png)

Check ob der Request auch sauber abgeschlossen wurde:
```console
Get-ExchangeCertificate | where {$_.Status -eq "PendingRequest" -and $_.IsSelfSigned -eq $false} | Format-List FriendlyName,Subject,CertificateDomains,Thumbprint
```
![Exchange - Zertifikate verlängern 04](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-14.png)

Sollte nix zurückgeben 😄

Jetzt kann auch gleich bei Bedarf wieder die Services enabled werden:
```console
Enable-ExchangeCertificate -Thumbprint 434AC224C8459924B26521298CE8834C514856AB -Services POP,IMAP,IIS,SMTP
```
Thumbprint natürlich anpassen! 😄

![Exchange - Zertifikate verlängern 05](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-15.png)

> **Warning**
> Im IIS die Bindungen prüfen → Frontend (Default Web Site) und Backend (Exchange Back End) sollten auf das neue Zertifikat gesetzt sein. Beim Backend muss meistens nochmal manuell das Zertifikat gesetzt werden!

## Erstellen

Zuerst müssen wir alle URLs und Domänen die wir brauchen zusammensammeln:

**Für JEDE auf dem Exchange konfigurierte Domäne eine autodiscover.domäne.de**
**Für JEDE auf dem Exchange konfigurierte Domäne eine domän.de und am besten ein *.domäne.de**

Beispiel:

AD-Domäne: test.local
Mail-Domäne: test.de und test.eu
EAS-URL: mobile.test.de 
MAPI-URL extern (z.B. für MS365): outlook.test.de 
MAPI-URL intern (für Outlook): outlook.test.local
Server-Name: demo-mail01

Folgende Domänen würden wir dann im Zertifikat benötigen:

```console
outlook.test.de,outlook.test.local,AutoDiscover.test.de,AutoDiscover.test.eu,AutoDiscover.test.local,demo-mail01,demo-mail01.test.local,test.de,test.eu,test.local,*.test.de,*.test.eu,*.test.local,localhost
```

Wenn man alle Domänen zusammen hat kann das Subject erstellt werden. Das sind die Angaben wie Ort, Oganisationseinheit, etc.

Beispiel:

| Beschreibung | Wert| 
|----------|----------|
| Anzeigename des Zertifikats | CN=outlook.test.de | 
| Abteilung (IT-Abteilung) | OU=IT | 
| Organisation | O=Test GmbH | 
| Ort | L=Musterhausen | 
| Staat | S=BY | 
| Land | C=DE | 

> **Warning**
>Dies Angaben MÜSSEN im Zertifikat vorhanden sein - nix wegsparen!

Ein Subject muss dann wie folgt aussehen:

```console
"CN=outlook.test.de, OU=IT, O=Test GmbH, L=Musterhausen, S=BY, C=DE"
```

Jetzt haben wir alle Infos die wir brauchen - Jetzt können wir den eigentlichen Request erstellen:
```console
$txtrequest = New-ExchangeCertificate -PrivateKeyExportable $true -GenerateRequest -friendlyName outlook.test.de -SubjectName "CN=outlook.test.de, OU=IT, O=Test GmbH, L=Musterhausen, S=BY, C=DE" -DomainName outlook.test.de,outlook.test.local,AutoDiscover.test.de,AutoDiscover.test.eu,AutoDiscover.test.local,demo-mail01,demo-mail01.test.de,test.de,test.eu,test.local,*.test.de,*.test.eu,*.test.local,localhost
 
[System.IO.File]::WriteAllBytes('\\localhost\c$\Temp\Exchange-cert.req', [System.Text.Encoding]::Unicode.GetBytes($txtrequest))
```

-Friendlyname ist der Anzeigename des Zertifikats.

So sieht das dann aus:

![Exchange - Zertifikate erstellen - Request](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-16.png)

Jetzt kann der Request in der CA eingereicht werden → siehe auch Exchange-Anleitung.

Wenn wir jetzt ein neues Zertifikat haben können wir dies jetzt importieren um den Request abzuschließen
```console
Import-ExchangeCertificate -PrivateKeyExportable $true -FileData ([System.IO.File]::ReadAllBytes('\\localhost\c$\Temp\Exchange-cert.cer'))
```
![Exchange - Zertifikate erstellen - Import](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-17.png)

Check ob der Request auch sauber abgeschlossen wurde:
```console
Get-ExchangeCertificate | where {$_.Status -eq "PendingRequest" -and $_.IsSelfSigned -eq $false} | Format-List FriendlyName,Subject,CertificateDomains,Thumbprint
```
![Exchange - Zertifikate erstellen - Check](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-18.png)

Sollte nix zurückgeben 😄

Jetzt kann auch gleich bei Bedarf wieder die Services enabled werden:
```console
Enable-ExchangeCertificate -Thumbprint 434AC224C8459924B26521298CE8834C514856AB -Services POP,IMAP,IIS,SMTP
```
Thumbprint natürlich anpassen! 😄

![Exchange - Zertifikate erstellen - Dienste zuweisen](https://github.com/friedlandreas/Guides/blob/935cfb12adc36ce5279e66177fe0233eee1af6a5/images/exchange-certs-powershell-19.png)

> **Warning**
> Im IIS die Bindungen prüfen → Frontend (Default Web Site) und Backend (Exchange Back End) sollten auf das neue Zertifikat gesetzt sein. Beim Backend muss meistens nochmal manuell das Zertifikat gesetzt werden!

Jetzt sollte es passen 😄
