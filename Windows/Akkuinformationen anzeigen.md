Wenn man unter Windows Infos über den Akku-Zustand haben will, gibt es dafür ein netten kleinen Befehl:

```console
powercfg /batteryreport
```

Das erstellt einen Report den man sich dann anzeigen lassen kann.

Mit
```console
powercfg /batteryreport /output “C:\tem\battery_report.html”
```
kann man den Speicherort des Reports angeben :-)

