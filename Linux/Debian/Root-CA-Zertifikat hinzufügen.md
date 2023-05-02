Um in Debian eine Root-Ca hinzufügen muss man folgendes machen:

1. CA-Datei (muss crt-Datei sein) kopieren nach /usr/local/share/ca-certificates/
 
    ```console
    sudo cp foo.crt /usr/local/share/ca-certificates/foo.crt
    ```
    
2. CA-Store updaten

    ```console
    sudo update-ca-certificates
    ```

fertig :-)
