Falls Outlook das Offline Address Bock nicht runtrladen kann und den Fehler

> Fehler (0x8004010F) beim Ausführen der Aufgabe: Fehler beim Vorgang. Ein Objekt kann nicht gefunden werden.

wirft, kann man es folgendermaßen fixen:

### 1) VirtualDirectory anpassen

Zuerst checken wir ob über einen Browser ein Aufruf möglich ist:

Auf dem Exchange in der Shell die Guid auslesen

```console
Get-OfflineAddressBook | fl GUID
```
und dann mit einem Browser https://mailserver/OAB/Gui/OAB.xml aufrufen.

Beispielurl: (https://mailserver01/OAB/827b61b3-4e0c-4bae-aa42-c5abadcb4094/OAB.xml

Hier kommt normal auch ein Error 500.

Dann auf der Shell:

```console
Set-OfflineAddressBook -Identity "Default Offline Address Book" -VirtualDirectories $null -Verbose
Set-OfflineAddressBook -Identity "Default Offline Address Book" -GlobalWebDistributionEnabled $true -Verbose
```

Nach einem 

```console
iisreset
```

sollte es gehen.

Falls nicht:

### 2) Mailbox anbinden

Auf der Shell mit

```console
Get-OfflineAddressBook | fl GeneratingMailbox
```

ob eine Mailbox angebunden ist.

Falls da keine Mailbox drin steht mittels

```console
Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*OAB*"} | ft Name,Servername,Database
```

prüfen ob eine da ist die OAB generieren kann.

Falls keine da ist mittels

```console
New-Mailbox -Arbitration -Name "OAB Gen 2" -UserPrincipalName oabgen2@domain.local
```

eine neue erstellen.

Dann die vorhandene oder die neue Mailbox anbinden

```console
Set-Mailbox -Identity oabgen2 -Arbitration -OABGen $true -MaxSendSize 1GB
Get-OfflineAddressBook | Update-OfflineAddressBook -Verbose
```

Jetzt sollte mittels Browser https://mailserver/OAB/Gui/OAB.xml aufrufbar sein - und Outlook wieder runterladen :-)
