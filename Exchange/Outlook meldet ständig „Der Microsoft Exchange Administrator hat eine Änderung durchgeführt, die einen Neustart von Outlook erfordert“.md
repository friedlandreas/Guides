Ich hatte den Fall, dass ein Kunden mit Exchange Server 2013 und Outlook 2013 darüber geklagt hat, dass immer wieder im Outlook die Meldung kommt 
>„Der Microsoft Exchange Administrator hat eine Änderung durchgeführt, die einen Neustart von Outlook erfordert“.

Das kommt von einem falschen Eintrag der Exchange-Datenbank im Active-Directory.

Mit dem ADSI Edit (**adsiedit.msc**) macht man folgendes:

```console
Configuration >> CN=Services >> CN=Microsoft Exchange >> CN=OrganisatonsNname >> CN=Administrative Groups >> CN=Exchange Administrative Group >> CN=Databases
```

dort auf der Datenbank bzw. den Datenbanken das Attribut **MSEXCHHomePublicMDB** überprüfen. Vor allem nach Migrationen verweist es noch auf falsche oder nicht mehr Vorhandene Datenbanken. Diesen Wert dann einfach **leeren**.

Falls der Wert schon auf **nicht gesetzt** steht – also leer ist – kann man auch einfach eine leere PublicFolder-Datenbank anlegen.

Spätestens jetzt sollte Outlook ohne die Meldung seinen Dienst tun.
