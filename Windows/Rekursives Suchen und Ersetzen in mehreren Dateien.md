Wenn man rekursiv in Dateien suchen und ersetzten will, geht das wie folgt:

```console
foreach ($f in gci -r -include „*.ini“) { (gc $f.fullname) | foreach {$_ -replace „ALTER-SERVER“, „NEUER-SERVER“ } | sc $f.fullname }
```

hier wird vom Standort der Eingabeaufforderung (also davor ein **cd c:\** wäre dann die ganze Festplatte) rekursiv alle INI-Dateien durchsucht un der String ALTER-SERVER durch den String NEUER-SERVER ersetzt 🙂
