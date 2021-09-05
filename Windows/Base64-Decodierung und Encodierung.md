Man muss ja öfters mal Base64-codierte Strings decodieren oder eben Zeichenketten in Base64-Strings encodieren.

Dazu kann man unter Windows entweder Online-Dienste wie https://base64decode.org verwenden oder relativ einfach die Powershell 🙂

**Decodieren**

```console
$string = "VGVzdC1TdHJpbmc="
[Text.Encoding]::Utf8.GetString([Convert]::FromBase64String($string))
```

**Codieren**

```console
$string = "Test-String"
[Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($string))
```

![Windows Base64](https://github.com/friedlandreas/Guides/blob/45ad5c5cbb5d4195669eeba90581bc74c5ca3a1a/images/PowershellBase64.png)

Ziemlich easy 🙂
