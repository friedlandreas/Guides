Wenn man bei einem Exchange mal schnell einen Empfangsconnector übernehmen will, kann man mit dem Befehl

```console
Get-ReceiveConnector "Connector" | Set-ReceiveConnector -RemoteIPRanges (Get-ReceiveConnector "AlterServer\Connector").RemoteIPRanges
```

super einfach die RemoteIPRanges übernehmen 🙂
