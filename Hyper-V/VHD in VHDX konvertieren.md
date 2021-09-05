Ich muss öfters mal VHD in VHDX konvertieren. Dazu kann man natürlich den Hyper-V Manager benutzen oder – meine persönliche Vorliebe – die Powershell.

Um es im Hyper-V Manager zu erledigen, muss man die Aktion **„Datenträger bearbeiten“ (Edit Disk)** auswählen und dort die Quell-VHD-Datei selektieren. Danach ist der Menüpunkt **„Konvertieren“ (Convert)** zu wählen und dann das VHDX-Format anzugeben.

Deutlich schöner geht das in der **Powershell**:

```console
Convert-VHD -Path c:\temp\source.vhd -DestinationPath c:\temp\destination.vhdx -VHDType Fixed
```

für eine VHDX mit fester Größe oder

```console
Convert-VHD -Path c:\temp\source.vhd -DestinationPath c:\temp\destination.vhdx -VHDType Dynamic
```

für eine VHDX mit wachsender (dynamischer) Größe.

Hat man jetzt einen ganze Menge VHDs zu konvertieren kann man dies auch mit der Powershell automatisieren:

```console
Set-Location c:\temp
gci -Filter *.vhd | foreach {Convert-VHD -Path $_.Name -DestinationPath „$($_.Basename).vhdx“ -VHDType Fixed}
```

![vhd to vhdx](https://github.com/friedlandreas/Guides/blob/43eda2dccde3ac8eae32af8b1b2ff33c3d7d0a06/images/vhdtovhdx.png)

Dabei werden alle VHD-Dateien automatisch nacheinander in VHDX-Dateien (in diesem Fall mit fester Größe) konvertiert. Die Dateinamen bleiben hierbei gleich – nur die Dateiendung ändert sich natürlich. Es kann natürlich hier auch ein anderer Zielpfad eingegeben werden, z.B.:

```console
gci -Filter *.vhd | foreach {Convert-VHD -Path $_.Name -DestinationPath „c:\vhdx\$($_.Basename).vhdx“ -VHDType Fixed}
```
