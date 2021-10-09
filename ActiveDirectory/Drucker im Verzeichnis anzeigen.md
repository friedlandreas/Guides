Will man sich die Drucker im ActiveDirectory anzeigen lassen die über **Im Verzeichnis anzeigen** angelegt wurden geht das super einfach über 

```console
Get-AdObject -filter "objectCategory -eq 'printqueue'" -Prop * | Select Name,serverName, @{N='ShareNames';E={$_.printShareName -join ';'}}
```
:-)
