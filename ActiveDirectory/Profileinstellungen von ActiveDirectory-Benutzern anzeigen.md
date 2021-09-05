Wenn man bei einer Migration aber alle (im AD unter Profil stehenden) Einstellungen – also Profilpfad, Anmeldeskript und Basisordner – der Benutzer übersichtlich angezeigt haben will – dann geht das folgendermaßen :

```console
Get-ADUser -filter * -properties scriptpath, homedrive, homedirectory, profilepath | sort Name | FT Name, Homedrive, HomeDirectory, scriptpath, profilepath
```

Damit werden alle User angezeigt – sortiert in diesem Fall nach Name.

Damit nichts abeschnitten wird muss man entweder das Powershell-Fenster breiter machen oder man schreibt es in eine Datei:

```console
Get-ADUser -filter * -properties scriptpath, homedrive, homedirectory, profilepath | sort Name | FT -autosize Name, Homedrive, HomeDirectory, scriptpath, profilepath | Out-String -Width 4096 | Out-File C:\user.txt
```

Die Ausgabe schaut dann ungefähr so aus:

> Name	Homedrive	HomeDirectory		scriptpath	profilepath
>
> ----	---------	-------------		----------	-----------
>
> admin	H:        	\\sv-home\admin$     	login.bat     	\\sv-profile\admin$
> 
> test	H:        	\\sv-home\test$     	login.bat     	\\sv-profile\test$

Hat mir schon oft geholfen 🙂
