Die Rechte-Vererbung im ActiveDirectory ist manchmal bei bestimmten Benutzern deaktiviert – selten ist das gewollt – fast immer gibt es aber deswegen (vor allem in Verbindung mit Exchange) Probleme.

Einige Beispiele:

**- ExchangeSynchronisationsfehler 86000C0A bei betroffenen Benutzern, obwohl OWA korrekt funktioniert**

**– Dateisystems-Auflistung im Explorer schlängt mit 0x86000Cxx Fehlern fehl**

**– Fehler im Ereignisprotokoll von MSExchange ActiveSync mit dem Inhalt „Active directory Antwort: 00000005: SecErr: DSID-031521D0, problem 4003 (INSUFF_ACCESS_RIGHTS), data 0″.“**

**– Exchange: das Verschieben der Mailbox der Benutzer (z.B. bei Exchange-Migrationen) schlägt fehl**

Bei einem Benutzer kann man die Vererbung wie **hier** beschrieben ja manuell aktivieren – bei vielen Usern ist da ein automatisierter Weg zu empfehlen….

Das kann man ganz einfach mit der Powershell erledigen! Einfach die PowerShell ISE als Administrator ausführen und folgendes Script ausführen:

```console
Import-Module activedirectory
$OU = "OU=INDIESEROUWERDENUSERGESUCHT,DC=MEINDOMAENE,DC=TLD"
$Users=get-aduser -Filter * -SearchBase $OU
 
if ($Users -ne $null) 
{
 
    foreach ($Entry in $Users) 
    {
    [string]$dn = (Get-ADUser $Entry).DistinguishedName
    $user = [ADSI]”LDAP://$dn”
    $acl = $user.objectSecurity
    Write-Host "Pruefe Benutzer:" (Get-ADUser $Entry).SamAccountName
 
        if ($acl.AreAccessRulesProtected)
        {
        Write-Host "Fixe Benutzer:" (Get-ADUser $Entry).SamAccountName
        $acl.SetAccessRuleProtection($false,$true)
        $inherited = $acl.AreAccessRulesProtected
        $user.commitchanges()
        }
    }
 
}
 
else 
{
    Write-Host "Keine Benutzer in $OU gefunden"
}
```

In der Zeile **$OU = „OU=INDIESEROUWERDENUSERGESUCHT,DC=MEINDOMAENE,DC=TLD“** einfach die ensprechende OU angeben und alle Benutzer – auch in Unter-OUs – werden angepasst 🙂
