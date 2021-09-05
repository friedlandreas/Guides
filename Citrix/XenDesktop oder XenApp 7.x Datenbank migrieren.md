Ich hatte die Aufgabe die Datenbank einer XenApp 7.6 Datenbank von einem SQL-Server auf einen anderen SQL-Server zu verschieben bzw. zu migrieren.
Es gibt unter http://support.citrix.com/article/CTX140319 eine Anleitung – die aber nur mit einigen Ergänzungen funktionierte.

**Hier ist mein Weg für den Umzug der Datebank:**

Dazu schließt alle Management Konsolen und öffnet auf **allen Delivery Controllern** eine **Powershell als Administrator** und setzt erstmal alle Datenbankverbindungen zurück:

```console
Add-PSSnapin Citrix*
Set-LogSite -State Disabled
Set-LogDBConnection -DataStore Logging -DBConnection $null
Set-MonitorDBConnection -DataStore Monitor -DBConnection $null
Set-MonitorDBConnection -DBConnection $null
Set-AcctDBConnection -DBConnection $null
Set-ProvDBConnection -DBConnection $null
Set-BrokerDBConnection -DBConnection $null
Set-EnvTestDBConnection -DBConnection $null
Set-SfDBConnection -DBConnection $null
Set-HypDBConnection -DBConnection $null
Set-ConfigDBConnection -DBConnection $null -force
Set-LogDBConnection -DBConnection $null -force
Set-AdminDBConnection -DBConnection $null -force
```

Danach kann die Datenbank über das SQL Server Management Studio auf dem alten Datenbankserver sicheren und auf dem neuen Datenbankserver wiederherstellen.

Wichtig hierbei ist dass die SQL-Logins für die Computerkonten der Delivery Controler im neuen SQL-Server vorher mit

```console
create login [domain\DeliveryControllerServername$] from windows
```

![Citrix - SQL Login](https://github.com/friedlandreas/Guides/blob/86746f185b6d6209372ffecc795e18be9fddb3cf/images/XenDesktop-Datenbank-Migration-SQL.png)

angelegt werden. Dann müssten die Berechtigungen für die Delivery Controller nach der Wiederherstellung der Datenbank passen.

Danach muss auf den Delivery Controllern in der Registry kontrolliert werden dass unter

```console
HKEY_LOCAL_MACHINE\Software\Citrix\XDservices\
```

in den einzelnen Unter-Schlüsseln unter

```console
DataStore\Connections
```

der REG_SZ-Wert **ConnectionString** leer ist.

![Citrix - DB ConnectionString](https://github.com/friedlandreas/Guides/blob/86746f185b6d6209372ffecc795e18be9fddb3cf/images/XenDesktop-Datenbank-Migration-Registry.png)

Dazu öffnet man auf allen Delivery Controllern eine Powershell als Administrator und setzt die neuen Datenbankverbindungen. 
Einfach **DatenbankServer\Instanzname** und **DatenbankName** die entsprechenden Werte eintragen. 
Wenn die Datenbank auf der Standardinstanz des SQL-Servers läuft kann auf \Instanzname verzichtet werden und nur der Servername eingetragen werden:

```console
Add-PSSnapin Citrix*
$dbs=“Server=DatenbankServer\Instanzname;Initial Catalog=DatenbankName;Integrated Security=True“
set-ConfigDBconnection -dbconnection $dbs
set-AdminDBconnection -dbconnection $dbs
set-LogDBconnection -dbconnection $dbs
set-AcctDBconnection -dbconnection $dbs
set-BrokerDBconnection -dbconnection $dbs
set-EnvTestDBconnection -dbconnection $dbs
set-HypDBconnection -dbconnection $dbs
set-MonitorDBconnection -dbconnection $dbs
set-ProvDBconnection -dbconnection $dbs
set-SfDBconnection -dbconnection $dbs
Set-LogDbConnection -DataStore logging -DbConnection $dbs
Set-MonitorDbConnection -DataStore monitor -DbConnection $dbs
Set-LogSite -State Enabled
```

Wenn das auf **allen Delivery Controllern** sauber durchgelaufen ist, kann auf dem ersten Delivery Controller das Citrix Studio öffnen.

Bei mir wollte das Studio ein **Site Upgrade und eine Aktualisierung der Delivery Controller**. Beides warf bei mir den Fehler, dass die Delivery Controller schon verbunden sind. Sonst lief alles durch.

Es funktionierte aber trotzdem danach alles sauber 🙂

Weitere Quellen:
http://support.citrix.com/article/CTX140319  
https://www.linkedin.com/pulse/20141030170612-131030064-how-to-migrate-your-citrix-xendesktop-or-xenapp-7-x-database  
http://blogs.citrix.com/2014/02/05/xendesktop-7-x-database-migration/  
http://www.dcug.de/xd7-datenbank-migrieren/  
