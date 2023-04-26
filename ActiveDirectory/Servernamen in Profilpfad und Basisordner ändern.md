Wenn man bei vielen Benutzern in einem Active Directory den Server im Profilpfad oder im Basisordner (Home, Home Folder) ändern muss – und nicht alle User einzeln über die GUI ändern will – kann man das am besten über die PowerShell machen.

So kann man bei allen Benutzer in einem Rutsch den Servernamen im UNC-Pfad des Profiles ändern:

```console
Import-Module ActiveDirectory

$oldServerName = "sv-alt"
$newServerName = "sv-neu"

[array]$AllUsers = Get-ADUser -filter * -Properties profilepath | Where-Object {$_.profilepath -ne $null}

foreach($user in $AllUsers){

if(($user.profilepath.ToString()).contains($oldServerName)){
$profilepath = ($user.profilepath.ToString()) -replace $oldServerName, $newServerName
Set-ADUser $user.DistinguishedName -profilepath $profilepath
}

}
```
und so kann man bei allen Benutzern den Server im UNC-Pfad des Basisordners ändern:

```console
Import-Module ActiveDirectory
 
$oldServerName = "sv-alt"
$newServerName = "sv-neu"
 
[array]$AllUsers = Get-ADUser -filter * -Properties HomeDirectory | Where-Object {$_.homedirectory -ne $null}
 
foreach($user in $AllUsers){
 
if(($user.HomeDirectory.ToString()).contains($oldServerName)){
$homeDirectory = ($user.HomeDirectory.ToString()) -replace $oldServerName, $newServerName
Set-ADUser $user.DistinguishedName -HomeDirectory $homeDirectory
}
 
}
```

Ich überprüfe immer mit [diesen Befehlen]( https://github.com/friedlandreas/Guides/blob/main/ActiveDirectory/Profileinstellungen%20von%20ActiveDirectory-Benutzern%20anzeigen.md) vorher und danach ob alles geklappt hat 🙂

So kann man wunderbar und superschnell eine schöne Bulk-Migration der Home Folder bzw. Profile machen 🙂

Bei Neueren Servern wäre das z.B. auch so möglich:

```console
Import-Module ActiveDirectory

$oldServerName = "alter-server"
$newServerName = "neuer-server"


$AllUsers = Get-ADUser -filter * -Properties HomeDirectory | Where-Object {$_.homedirectory -like "\\alter-server\*"}

foreach($user in $AllUsers)
{
$homeDirectory = ($user.HomeDirectory.ToString()) -replace $oldServerName, $newServerName
Set-ADUser $user.DistinguishedName -HomeDirectory $homeDirectory
}
```

