Ich hatte das Problem das auf einem Windows 11 winget nicht mehr funktionierte.

Nur kurz gekreiselt - dann kamm nix mehr - kein install, kein upgrade funktonierte mehr.

Falls das auftritt kann man winget mittels

```console
Invoke-WebRequest -Uri https://aka.ms/getwinget -OutFile winget.msixbundle
Add-AppxPackage winget.msixbundle
del winget.msixbundle
```

wiederherstellen.

Nach dem Reset von winget funktionierte wieder alles :-)
