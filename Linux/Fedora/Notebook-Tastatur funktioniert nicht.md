Ich hatte unter Fedora das Problem, dass bei einem älteren Notebook (in dem Fall ein Fujtisu U7510) die interne Tastatur nicht funktionierte. 

Mit dem Live-System funktionierte die Notebook-Tastatur - auf dem installierten Fedora (in dem Fall die Version 43) ging sie nicht :-/

Gelöst habe ich das Problem mittels GRUB-Parameter :-)

### Grub

Zuerst wird die geöffnet

```console
sudo nano /etc/default/grub
```
und dort die Werte **i8042.reset i8042.nomux=1** and die Zeile mit **GRUB_CMDLINE_LINUX** angefügt.

Sieht bei mir dann so aus:

**GRUB_CMDLINE_LINUX="rhgb quiet i8042.reset i8042.nomux=1"**

Danach speichern wir die Datei und updaten die Konfig mit

```console
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

### Reboot

Nach einem Reboot lief die Tastatur :-)
