Das ändern der Standard-Organisationseinheiten, auch OU (Organizational Unit) genannt, in denen neue Computer bzw. neue Benutzer angelegt werden, ist eigentlich sehr einfach. 

Dazu öffnet man eine **Eingabenaufforderung** und leitet mittels

```console
redircmp ou=ComputerOU,dc=Domainname,dc=local
```

die Default-OU der Computer oder mittels

```console
redirusr dc=BenutzerOU,dc=Domainname,dc=local
```

die Default-OU der Benutzer ändern bzw. umleiten.

Es kann selbstverständlich auch eine verschachtelte OU angegeben werden, wie z.B.

```console
redircmp ou=ComputerOU,ou=UnterOU,dc=Domainname,dc=local
```

Der Befehl wird mit **„Umleitung erfolgreich“** bestätigt. Wird jetzt ein Computer bzw. User angelegt landet das Objekt automatisch in der angegebenen OU!
