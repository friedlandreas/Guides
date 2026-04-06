Man kann ja **nc** (netcat) für vieles verwenden - wirklich das oft beschworende "Schweizer Taschenmesser" im Netzwerkbereich  

Auch als Telnet-Ersatz kann es verwendet werden - allerdings braucht es unter macos um z.B. auch SMTP zu testen noch den Parameter **-c**

 ```console
nc -c mail.test.domain 25
```

Dann klappts auch 😊
