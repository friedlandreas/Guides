Um die fünf FSMO-Rollen in einer Domäne von einem auf einen anderen Domain Controller zu verschieben hab ich früher immer das ntdsutil verwendet – aber das geht natürlich auch mit der Powershell 🙂

# Anzeigen  
Zuerst zeigen wir uns am besten alle Rolleninhaber an. 
Dazu die **AD-Powershell am Domain Controller öffnen** oder die Module mit

```console
Import-Module ActiveDirectory
```

importieren.

Die Rollen des Forest anzeigen:

```console
Get-ADForest domain.local | ft DomainNamingMaster, SchemaMaster
```

Und die Rollen der Domäne anzeigen:

```console
Get-ADDomain domain.local | ft InfrastructureMaster, PDCEmulator, RIDMaster
```

![FSMO](https://github.com/friedlandreas/Guides/blob/cd8afd8caed399352b2302bcccf044cdd3bf5f18/images/FMSO-01.png)

# Verschieben
Um eine Rolle zu verschieben muss man jetzt nur das Move-ADDirectoryServerOperationMasterRole Module im folgenden Schema verwenden:

```console
Move-ADDirectoryServerOperationMasterRole -Identity „Ziel-DC“ Role
```

Also z. B. :

```console
Move-ADDirectoryServerOperationMasterRole -Identity „dc-02“ PDCEmulator
```

![FSMO](https://github.com/friedlandreas/Guides/blob/cd8afd8caed399352b2302bcccf044cdd3bf5f18/images/FMSO-02.png)

Tipp: Man kann die Rollen auch super mit 0 – 4 abkürzen:

> 0 : PDCEmulator
> 1 : RIDMaster
> 2 : InfrastructureMaster
> 3 : SchemaMaster
> 4 : DomainNamingMaster

So kann man nämlich den Befehl schön verkürzen 🙂

Es reicht so z.B. ein

```console
Move-ADDirectoryServerOperationMasterRole -Identity „dc-02“ –OperationMasterRole 0,1
```

![FSMO](https://github.com/friedlandreas/Guides/blob/cd8afd8caed399352b2302bcccf044cdd3bf5f18/images/FMSO-03.png)

Wenn mann z.B. alle Rollen auf einmal verschieben will lohnt sich das abkürzen richtig – so reicht ein

```console
Move-ADDirectoryServerOperationMasterRole -Identity „dc-02“ –OperationMasterRole 0,1,2,3,4
```
statt

```console
Move-ADDirectoryServerOperationMasterRole -Identity „dc-02“ –OperationMasterRole PDCEmulator, RIDMaster, InfrastructureMaster, SchemaMaster, DomainNamingMaster
```

![FSMO](https://github.com/friedlandreas/Guides/blob/cd8afd8caed399352b2302bcccf044cdd3bf5f18/images/FMSO-05.png)

# Prüfen
Danach nochmal überprüfen:

```console
Get-ADForest domain.local | ft DomainNamingMaster, SchemaMaster
```

und

```console
Get-ADDomain domain.local | ft InfrastructureMaster, PDCEmulator, RIDMaster
```

![FSMO](https://github.com/friedlandreas/Guides/blob/cd8afd8caed399352b2302bcccf044cdd3bf5f18/images/FMSO-04.png)

# Verschieben erzwingen
Falls eine der Rollen nicht verschoben werden kann – weil z.B. der alte Inhaber der Rolle nicht mehr erreichbar ist – kann mit dem Parameter -force die Übertragung erzwungen werden (wie unter ntdsutil mit seize).

```console
Move-ADDirectoryServerOperationMasterRole -Identity “dc-02” –OperationMasterRole, DomainNamingMaster,PDCEmulator,RIDMaster,SchemaMaster,InfrastructureMaster –Force
```

Selbstverständlich sollte der alte Domain Controller von dem wir die Rollen mit -Force verschoben haben nie wieder angeschaltet werden!
