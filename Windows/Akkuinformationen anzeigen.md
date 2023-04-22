Wenn man unter Windows Infos über den Akku-Zustand haben will, gibt es dafür ein netten kleinen Befehl:

```console
powercfg /batteryreport
```

![Windows - powercfg](https://github.com/friedlandreas/Guides/blob/ecbb617a3139de02305ffe0b671451304d916a03/images/Windows-Akku-Infos-01.png)

Das erstellt einen Report den man sich dann anzeigen lassen kann.

So sieht dann der Report aus:

![Windows - Akku-Report](https://github.com/friedlandreas/Guides/blob/ecbb617a3139de02305ffe0b671451304d916a03/images/Windows-Akku-Infos-02.png)

Mit
```console
powercfg /batteryreport /output “C:\tem\battery_report.html”
```
kann man den Speicherort des Reports angeben :-)

