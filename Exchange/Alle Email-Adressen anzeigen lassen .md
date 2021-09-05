Um alle Email-Adressen aller Benutzer auf dem Exchange 2007 oder Exchange 2010 anzeigen zu lassen, kann man auf die Exchange-Powershell zurückgreifen:

```console
Get-Mailbox -ResultSize Unlimited |Select-Object DisplayName,ServerName,PrimarySmtpAddress, @{Name=“EmailAddresses”;Expression={$_.EmailAddresses |Where-Object {$_.PrefixString -ceq “smtp”} | ForEach-Object {$_.SmtpAddress}}} | fl
```
Das zeigt mir in der der Powershell schön alle Email inklusive der Information, welche Email-Adresse die Hauptadresse ist, auf:

> DisplayName        : Administrator  
> ServerName         : mail  
> PrimarySmtpAddress : Administrator@email.adresse  
> EmailAddresses     : {Administrator@email.adresse}  
> 
> DisplayName        : Müller Hans  
> ServerName         : mail  
> PrimarySmtpAddress : hans.mueller@email.adresse  
> EmailAddresses     : {hans.mueller@email.adresse, mueller@email.adresse}  

Will ich die Ausgabe in eine Datei umleiten, hänge ich nur ein **> c:\ausgabe.txt** drann:

```console
Get-Mailbox -ResultSize Unlimited |Select-Object DisplayName,ServerName,PrimarySmtpAddress, @{Name=“EmailAddresses”;Expression={$_.EmailAddresses |Where-Object {$_.PrefixString -ceq “smtp”} | ForEach-Object {$_.SmtpAddress}}} | fl > c:\ausgabe.txt
```
