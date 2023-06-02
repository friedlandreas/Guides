Manchmal kommt es bei Windows Servern vor das sich das Netwerkprofil statt auf Domäne auf privates Netzwerk einstellt. 
Dann gibts Probleme mit Firewall-Regeln -> super nervig.

Meistens liegt es daran das bei der Erkennung durch den NLA-Dienst der Domänen-Controller nicht bzw. noch nicht sauber erreichbar ist - z.B. nach einem Neustart.

Man kann diese Erkennung aber mittels **Registry-Key** "optimieren":

Den **Registrierungs-Editor öffnen** und zu

```console
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NlaSvc\Parameters
```
navigieren. 
Dort einen **DWORD-Eintrag erstellen**:

```console
AlwaysExpectDomainController 
```
und den Wert auf **1** stellen.

Danach den **Server neustarten**.

Jetzt sucht der Server so langen einen Domänen-Controller bis er einen findet und stellt nicht mehr auf privates Netwerk :-)

Quelle: https://dashdot.de/2023/06/01/windows-server-privates-netzwerk-am-domaenen-controller-nach-neustart/
