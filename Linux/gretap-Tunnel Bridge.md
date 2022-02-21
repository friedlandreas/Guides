Ich hab öfters mal die Anforderung das ich ein Interface in einen GRE-Tunnel bridgen muss - um einen L2-Tunnel zu haben.

Auf Linux (Debian) geht das ziemlich einfach:

Zuerst die Bridge-Util installieren

```console
apt install bridge-utils
```
Dann einen Gre-Tunnel bauen und über die Bridge das Interface (in meinem Fall eth1) mit dem Tunnel zusammen auf die Bridge legen

Router 1:
```console
ip link add gretap1 type gretap local 10.10.10.101 remote 10.10.10.102
ip link set dev gretap1 up
ip link set dev eth1 up
brctl addbr br1
brctl addif br1 gretap1
brctl addif br1 eth1
ip link set br1 up
```

Router 2:
```console
ip link add gretap1 type gretap local 10.10.10.102 remote 10.10.10.101
ip link set dev gretap1 up
ip link set dev eth1 up
brctl addbr br1
brctl addif br1 gretap1
brctl addif br1 eth1
ip link set br1 up
```

Jetzt ist auf beiden Routern ein transparenter L2-Tunnel -> das heißt z.B. ein DHCP-Server an eth1 auf Router 1 verteilt seine IPs jetzt auch auf allem was an eth1 auf Router 1 steckt :-)
