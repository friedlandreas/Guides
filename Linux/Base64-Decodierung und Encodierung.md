Unter Linux geht eine Base64-Decodierung  super einfach auf der Shell mittels dem base64-Tool:

**Decodieren**

```console
echo `echo VGVzdC1TdHJpbmc= | base64 --decode`
```

**Codieren**

```console
echo -n 'Test-String' | base64
```
![Linux Base64](https://github.com/friedlandreas/Guides/blob/e8b813d98854821bd7a897afd5c67891d7572669/images/LinuxBase64.png)

Super simpel 🙂

