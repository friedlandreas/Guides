Ich brauche öfters mal von einem Video z.B. auf Youtube nur die Audiospur als z.B. MP3.

Das mach ich immer mit **youtube-dl** (im Zusammenspiel mit **ffmpeg**) – das Tool meiner Wahl für sowas 🙂

```console
youtube-dl --extract-audio --audio-format mp3 '<video URL>'
```

also z.B. :

```console
youtube-dl --extract-audio --audio-format mp3 'https://www.youtube.com/watch?v=VkpjKmsSNRU'
```
