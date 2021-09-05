Wenn man Benutzern aus einer AD-Gruppe z.B. Mailboxen erstellen will, geh das super einfach:

```console
Get-ADGroupMember -identity "AD-Gruppe" -Recursive | foreach { get-mailbox -identity $_.samaccountname}
```
![Exchange - Benutzern aus AD-Gruppe Mailbox erstellen](https://github.com/friedlandreas/Guides/blob/f6893e6d1caff8bee74343f94fb3ea2273c9026a/images/Exchange-ad-gruppe-mailbox-erstellen-02.png)

Fertig 🙂

Geht natürlich auch mit z.B. Berechtigungen:

```console
Get-ADGroupMember -identity "AD-Gruppe" -Recursive | foreach { Add-MailboxPermission info -User $_.samaccountname -AccessRights FullAccess -InheritanceType all }
```

![Exchange - Benutzern aus AD-Gruppe Mailbox erstellen](https://github.com/friedlandreas/Guides/blob/f6893e6d1caff8bee74343f94fb3ea2273c9026a/images/Exchange-ad-gruppe-mailbox-erstellen-01.png)

🙂
