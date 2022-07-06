Wenn man einen IPSec-Tunnel auf einen MikroTik konfiguriert sind die Netze im Tunnel untereinander wunderbar erreichbar - vom Router selber aber nicht.

Das Problem ist das der Router nicht die "richtige" IP verwendet - und das kann bzw. muss mann über ein NAT fixen:

```console
/ip firewall nat
add chain=srcnat src-address-type=local dst-address=<remote subnet> action=src-nat to-address=<router ip>
````

also wenn das Remote-Netz 10.10.10.0/24 und der Router die IP 10.10.1.1 hat wäre es also:
```console
/ip firewall nat
add chain=srcnat src-address-type=local dst-address=10.10.10.0/24 action=src-nat to-address=10.10.1.1
````

Danach war vorm Router aus das Netz erreichbar :-)

Quelle: https://forum.mikrotik.com/viewtopic.php?t=147723#p726991
