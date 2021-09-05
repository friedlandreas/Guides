Ich hatte den Anwendungsfall, dass ich bei einer Exchange-Migration nur immer eine bestimmte Anzahl von Postfächern umziehen konnte.

Dieses Problem lässt sich wunderbar per Powershell lösen:

```console
$a= get-mailbox -server NameDesExchangeServer | Select-Object name -First 100
 
foreach ($b in $a) {New-moverequest -Identity $b.name}
```

Kurze Erklärung:  
In der ersten Zeile schreibe ich die ersten 100 Zeilen der Ausgabe von **get-mailbox** in eine Variable.

In der zweiten Zeile übergebe ich den Postfachnamen in ein **new-moverequest** – und mache dies für jede Zeile.

Und schon hat man – in meinem Fall – 100 MoveRequest 🙂

Natürlich kann man hier noch bei **get-mailbox oder new-moverequest noch weitere Parameter und Optionen übergeben**
