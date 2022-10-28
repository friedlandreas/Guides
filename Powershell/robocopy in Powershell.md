Will man in PowerShell das Tool robocopy für das Kopieren verwenden geht das super einfach:

```console
$source = "D:\Quelle\"
$destination = "D:\Ziel\"
$options = "/MIR /ZB /R:2 /W:2"

robocopy $source $destination $options.split(' ')
```


