Unter VMWare Workstation Pro und Fusion kann man die Side Channel Mitigations recht einfach deaktivieren - Anleitung hier: https://kb.vmware.com/s/article/79832

Unter dem Workstation Player geht das in der GUI leider nicht - da muss man die Konfig-Datei bearbeiten.

Folgende Schritte sind zu befolgen:

1. Die VM beenden

2. In den Ordner gehen und die Konfig-Datei der VM (die VMX-Datei) in einem Editor ändetn

3. Folgende Zeile unten anfügen: 
```console
ulm.disableMitigations="TRUE"
```

4. Speichern der Datei und starten der VM

Fertig 🙂
