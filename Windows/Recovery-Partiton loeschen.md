
Standardmäßig legt Windows eine Wiederherstellungspartition an. Wenn man die Sytem-Partiton vergrößern will ist diese allerdings leider im Weg :neutral_face:

![Windows RecoveryPartion](https://github.com/friedlandreas/Guides/blob/12a8d216974699b0e3436a9172c8a01653640b4f/images/Windows-RecoveryPartition-01.png)

Da die Wiederherstellungspartition läst sich ohne negativen Auswirkungen löschen - man braucht halt dann eine ISO um bei Bedarf ein Wiederherstellungsystem zu booten :blush:

Es ist auch relativ leicht diese zu löschen:

Dazu eine Eingabeaufforderung als Administrator starten und 

```console
diskpart
```

starten.

Mit 

```console
list disk
```

die Disks anzeigen und mit 

```console
select disk X
```

die Disk auswählen auf der sich die Partiton befindet. 


Dannach mit 
```console
list partition 
```

die Partitionen anzeigen und mit 

```console
select partition X
```

die Wiederherstellungspartition auswählen (meistens so um die 700 MB bis 1 GB groß).

Jetzt kann mit 

```console
delete partition override 
```
die Wiederherstellungspartition gelöscht werden.

![Windows RecoveryPartion](https://github.com/friedlandreas/Guides/blob/12a8d216974699b0e3436a9172c8a01653640b4f/images/Windows-RecoveryPartition-02.png)

Dannach mit 
```console
list partition 
```

noch kurz checken ob alles passt und mit

```console
exit
```

aus diskaprt raus - und schon kann man easy die Systempartion vergrößern :blush:

![Windows RecoveryPartion](https://github.com/friedlandreas/Guides/blob/12a8d216974699b0e3436a9172c8a01653640b4f/images/Windows-RecoveryPartition-03.png)
