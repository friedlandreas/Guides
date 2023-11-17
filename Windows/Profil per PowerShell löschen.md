Wenn man unter Windows das Profil eines Users löschen will geht das recht einfach mittels PowerShell:

```console
$user = "tina.martin"
 
Get-CimInstance -Class Win32_UserProfile | Where-Object { $_.LocalPath.split(‘\’)[-1] -eq $user } | Remove-CimInstance
```

Damit wird das Profil unter c:\Users und die Einträge in der Registry unter HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList des angegebenn Users (hier als Beispiel tina.martin) gelöscht :-)
