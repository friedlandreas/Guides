Wenn man das Problem hat, dass der NetworkManager unter Debian das Netzwerk-Interface nicht managen kann - z.B. für Cockpit - kann das super einfach eingeschaltet werden:

 ```console
vim /etc/NetworkManager/NetworkManager.conf
 ```

und dort 

 ```console
[ifupdown]
managed=false
 ```
in
 ```console
[ifupdown]
managed=true
 ```
ändern.  
Reboot -> Fertig :-)
