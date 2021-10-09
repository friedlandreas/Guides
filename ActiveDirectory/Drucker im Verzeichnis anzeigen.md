Will man sich die Drucker im ActiveDirectory anzeigen lassen die über **Im Verzeichnis anzeigen** angelegt wurden geht das super einfach über 

```console
Get-AdObject -filter "objectCategory -eq 'printqueue'" -Prop * | Select Name,serverName, @{N='ShareNames';E={$_.printShareName -join ';'}}
```

Quelle: https://social.technet.microsoft.com/Forums/azure/en-US/08ac34d8-d604-4d0e-b1b9-1a66b41030b0/get-list-of-printers-published-in-active-directory?forum=winserverpowershell
