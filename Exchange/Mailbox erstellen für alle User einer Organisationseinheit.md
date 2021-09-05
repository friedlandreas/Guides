Wenn man mal für alle User einer Organisationseinheit eine Exchange-Mailbox erstellen will geht das super einfach per Powershell:

```console
Get-User -OrganizationalUnit „OU=Finanzverwaltung,OU=Abteilungen,DC=test,DC=local“ | Enable-Mailbox
```

![Exchange Mailbox für alle AD-User aus OU](https://github.com/friedlandreas/Guides/blob/100b31172513fe857d904336f2d096964153c201/images/enable-mailbox-ou.png)

Kurze Erklärung: Mit **Get-User** zeigen wir uns alle Benutzer in der angegebenen OU an (muss im LDAP-Pfad-Format bzw. als DistinguishedName angegeben sein) und dann pipen wir es in ein **Enable-Mailbox** wo eben die Mailbox erstellt wird. fertig 🙂
