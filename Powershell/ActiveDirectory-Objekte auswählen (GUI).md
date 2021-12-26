Wenn man in einen Powershell-Script AD-Objekte auswählen will (Benutzer, OUs, Gruppen) will man das vielleicht über eine kleine GUI machen.

Da es standardmäßig keinen AD-Object-Picker in Powershell gibt kann man das folgendermaßen in Powershell nachbauen:

```Powershell
#Get Group
$selectedgroup = Get-ADGroup -Filter * |
    Select-Object -Property Name, GroupCategory,GroupScope, SamAccountName,DistinguishedName |
        Sort-Object -Property Name | Out-GridView -OutputMode Single -Title "Please choose a group"

if(!$selectedgroup){
    Write-Host "No group was selected" -ForegroundColor Yellow
}

write-host $selectedgroup.SamAccountName

#Get OU
$selectedou= Get-ADOrganizationalUnit -Filter * |
    Select-Object -Property Name,DistinguishedName |
        Sort-Object -Property Name | Out-GridView -OutputMode Single -Title "Please choose a OU"

if(!$selectedou){
    Write-Host "No OU was selected" -ForegroundColor Yellow
}

write-host $selectedou.DistinguishedName

#Get User
$selecteduser= Get-ADuser -Filter * -SearchBase "OU=Abteilung01,OU=Benutzer,DC=nextgo,DC=local" |
    Select-Object -Property Name, SamAccountName,DistinguishedName |
        Sort-Object -Property Name | Out-GridView -OutputMode Multiple -Title "Please choose a User / multiple Users"

if(!$selecteduser){
    Write-Host "No User was selected" -ForegroundColor Yellow
}

write-host $selecteduser.SamAccountName
```

Mit der Auswahl kann man dann in den Scripten weitermachen :-)

Quelle: https://stackoverflow.com/questions/66670058/powershell-active-directory-picke
