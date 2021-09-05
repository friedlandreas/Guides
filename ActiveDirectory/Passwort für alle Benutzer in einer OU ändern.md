Ich hatte den Bedarf für alle Benutzer in einer OU das Passwort zu ändern – das geht super leicht per Powershell:

```console
Get-ADUser -Filter * -SearchBase "OU=ou_name,DC=domain,DC=local" | Set-ADAccountPassword -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "Temp123$" -Force)
```

Einfach die Searchbase und das Passwort anpassen – Fertig 🙂
