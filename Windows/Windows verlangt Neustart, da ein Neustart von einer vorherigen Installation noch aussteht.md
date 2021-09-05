Bei der Installation von so mancher Software (in meinem Fall z. B. SQL Server 2008) wird vom Setup überprüft, ob vor der Installation ein Neustart erfoderlich ist.
Hatt auch seinen Sinn, da vielleicht voher Systemdateien geändert worden, etc..
Nur manchmal kannst du das Windows x-fach neustarten, er verlangt immer einen Neustart vor der Installation.

Das liegt meistens an den **Registry-Keys**:

```console
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\PendingFileRenameOperations
```

und

```console
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Updates\UpdateExeVolatile
```

wenn:
der Registrierungsschlüssel UpdateExeVolatile einen anderen Wert als 0 enthält
der Registrierungsschlüssel PendingFileRenameOperations einen beliebigen Wert aufweist

Zur Behebung der Neustart-Problematik muss der Wert **UpdateExeVolatile** auf 0 gesetzt werden und der Inhalt des Registryeinstrag **PrendingFileRenameOperations** gelöscht werden.

Bei mir war es meist der Key **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\PendingFileRenameOperations**
