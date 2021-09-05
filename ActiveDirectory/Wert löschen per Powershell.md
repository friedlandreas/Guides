Ich hatte bei einer Migration eines ActiveDirectorys das Problem das bei vielen Usern noch Login-Scripte definiert waren die ich aber nicht mehr verwenden wollte.

Will man von vielen Usern einen Wert im Active Directory löschen geht das einfach über die Powershell 🙂

Hier ein Beispiel um bei allen Usern im AD den ScriptPath zu löschen:

```console
get-ADUser -filter * | set-aduser -Clear scriptPath
```

Das kann natürlich über die Filter noch eingeschränkt werden und funktioniert natürlich auch für andere Parameter 🙂

Hier noch ein Beispiel für das Löschen des Profil-Pfads für alle User eine OU:

```console
Get-ADUser -Filter * -SearchBase „OU=TestUser,DC=domain,DC=local“ | Set-ADUser -Clear profilepath
```
