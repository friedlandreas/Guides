Ich habe öfters mal folgendes Problem: Exchange-Usern wird in Outlook (und auch im OWA) die Ordnernamen englisch angezeigt, bzw. das gesamte Postfach ist auf Englisch eingestellt. Das finden viele störend.

Man kann natürlich die Sprache im OWA (unter den Regional-Einstellungen) umstellen oder auch Outlook mit outlook.exe /resetfoldernames starten – aber die Sprache eines Postfaches und auch die Ordnernamen kann man als Administrator ziemlich **einfach mit der Exchange-Powershell ändern**:

# Für ein einzelnes Postfach:

```console
Set-MailboxRegionalConfiguration -Identity “Alias oder E-MailAdresse” -Language {de-DE} -LocalizeDefaultFolderName:$true -DateFormat “dd.MM.yyyy”
```

# Für alle Postfächer:

```console
Get-Mailbox | Set-MailboxRegionalConfiguration -Language {de-DE} -LocalizeDefaultFolderName:$true -DateFormat “dd.MM.yyyy”
```

Der Parameter **–Language** gibt die Sprache des Postfaches an. In meinem Beispiel ist das “Deutsch” – es kann auch ein anderer Regional Code angegeben werden. Eine Liste mit den Codes der verfügbaren Sprachen findet sich hier: http://technet.microsoft.com/en-us/library/aa997435.aspx
