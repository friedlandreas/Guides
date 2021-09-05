VMware empfiehlt bei einem HA-Cluster eine redundante Anbindung des Verwaltungsnetzwerk („Management Network“) . Wenn dies nicht möglich bzw. gewollt ist wird eine Warnmeldung angezeigt:

**Dieser Host verfügt momentan über keine Verwaltungsnetzwerkredundanz**

Damit diese Warnmeldung ausgeblendet wird muss in den erweiterten Clustereinstellungen den Parameter

```console
das.ignoreRedundantNetWarning
```

mit dem Wert

```console
True
```

eingetragen werden
