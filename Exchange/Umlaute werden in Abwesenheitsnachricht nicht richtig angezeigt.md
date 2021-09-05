Ich hatte bei einem Exchange 2013 das Problem, dass Umlaute in Abwesenheitsnachrichten (Out of Office) bzw. Automatischen Antworten nicht dargestellt wurden – diese wurden mit einem ? ersetzt. Das sah dann so aus:

![OOF ohne Umlaute](https://github.com/friedlandreas/Guides/blob/109a067799d95f2748db15c70704add03a802af8/images/OOFUmlaute.jpg)

Ich habe das Problem damit behoben, dass ich den **ContentType** der **RemoteDomain** auf dem Exchange von **MimeText** auf **MimeHTMLText** mittels der Exchange Management Shell umgestellt habe:

```console
get-remotedomain | set-remotedomain -ContentType MimeHtmlText
```

Danach waren alle Umlaute in den Automatischen Antworten und Abwesenheitsnotizen (OOF halt 😉 ) wieder richtig

![OOF mit Umlaute](https://github.com/friedlandreas/Guides/blob/109a067799d95f2748db15c70704add03a802af8/images/OOFUmlauteOOF.jpg)
