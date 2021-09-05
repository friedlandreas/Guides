Ich hatte auf einem Exchange-Management-Host das Problem das nach der Installation manche Befehle nicht funktionierten und folgende Fehler geworfen haben:

> Der Parameter "RecipientFilter" kann nicht an das Ziel gebunden werden. Ausnahme beim Festlegen von "RecipientFilter": "Die Datei oder Assembly<br>"Microsoft.Exchange.ManagedLexRuntime.MPPGRuntime, Version=15.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" oder eine Abhängigkeit davon wurde nicht gefunden. Das System<br>kann die angegebene Datei nicht finden."

oder

> Get-CASMailbox : Cannot bind parameter 'Filter' to the target. Exception setting "Filter": "Could not load file or assembly 'Microsoft.Exchange.ManagedLexRuntime.MPPGRuntime, Version=15.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of it\ s dependencies. The system cannot find the file specified."

Auf dem Exchange Server direkt trat der Fehler nicht auf.

Die Lösung war relativ simpel:

Man muss nur die **Microsoft.Exchange.ManagedLexRuntime.MPPGRuntime.dll** aus dem Verzeichnis **C:\Program Files\Microsoft\Exchange Server\V15\Bin** von einem Exchange Server in das gleiche Verzeichnis auf dem Mangement-Server kopieren.

![Exchange fehlende DLL](https://github.com/friedlandreas/Guides/blob/1f1237bf9c31f12b62946994ba6df9bf7d8df49e/images/Exchange-missing-DLL.png)
