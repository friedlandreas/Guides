# Routen

**Route erstellen**

```console
set static-route 10.20.30.0/28 nexthop gateway address 192.168.50.1 on
```

**Route löschen**

```console
set static-route 10.20.30.0/28 off
```
# Default Gateway

**Default-Gateway erstellen**

```console
set static-route default nexthop gateway address 192.168.200.254 on
```

**Default-Gateway löschen**

```console
set static-route default nexthop gateway address 192.168.200.254 off
```
