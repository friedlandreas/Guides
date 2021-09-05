Standardmäßig kürzt nach einer gewissen Länge die Powershell die Ausgabe.

Will man das verhindern und den kompletten String oder das komplette Array sehe, kann man mit einem Befehl dieses Verhalten deaktivieren:

```console
$FormatEnumerationLimit=-1
```

Der Standardwert ist **3** -> und der kürzt. Mit **-1** wird alles angezeigt 🙂
