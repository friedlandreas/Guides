```console
Get-MailboxStatistics -server servername | sort TotalItemSize | FT DisplayName,TotalItemSize
```

Die Ausgabe erfolgt dann schön geordnet nach Postfachgröße 🙂
