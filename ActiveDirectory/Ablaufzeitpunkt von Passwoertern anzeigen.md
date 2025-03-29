Will man sich den Passwort-Ablaufzeitpunkt der Benutzer-Accounts im AD anzuzeigen, geht das recht einfach mittels PowerShell:

### Alle Accounts:

```console
Get-ADUser -filter {Enabled -eq $True -and PasswordNeverExpires -eq $False} –Properties "samaccountname", "msDS-UserPasswordExpiryTimeComputed" |
Select-Object -Property "samaccountname",@{Name="ExpiryDate";Expression={[datetime]::FromFileTime($_."msDS-UserPasswordExpiryTimeComputed")}}
```

Hier wurden alle Accounts angezeigt die ativiert sind und ein ablaufendes Passwort haben:

![PowerShell Ablaufende Passwörter - alle User](https://github.com/friedlandreas/Guides/blob/60c4e6ca6a257544423f40d18342324219aba76c/images/Powershell-ablaufende-Passwoerter-alle-User.PNG)

Filter kann natürlich angepasst werden :-)

> [!TIP]
> 01.01.1601 steht für "Benutzer muss Kennwort bei der nächster Anmeldung ändern"

### Einzelner Account:

```console
Get-ADUser username –Properties "samaccountname", "msDS-UserPasswordExpiryTimeComputed" |
Select-Object -Property "samaccountname",@{Name="ExpiryDate";Expression={[datetime]::FromFileTime($_."msDS-UserPasswordExpiryTimeComputed")}}
```

Also z.B.:

```console
Get-ADUser hans –Properties "samaccountname", "msDS-UserPasswordExpiryTimeComputed" |
Select-Object -Property "samaccountname",@{Name="ExpiryDate";Expression={[datetime]::FromFileTime($_."msDS-UserPasswordExpiryTimeComputed")}}
```

![PowerShell Ablaufende Passwörter - ein User](https://github.com/friedlandreas/Guides/blob/60c4e6ca6a257544423f40d18342324219aba76c/images/Powershell-ablaufende-Passwoerter-User.PNG)
