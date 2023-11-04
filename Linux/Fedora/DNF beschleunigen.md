Unter Fedora (und aderen z.B. Redhat, CentOS, etc) wird DNF als Paketmanager verwendet. Standardmäßig ist der allerdings recht träge beim donwnload..
Das kann man zum Glück optimieren :-)

### Konfiguration

Zuerst wird die dnf.conf geöffnet

```console
sudo dnf vim /etc/dnf/dnf.conf
```
und dort 

**max_parallel_downloads=10**

eingetragen / hinzugefügen / angepasst. 

Speichern und schon ist DNF deutlich schneller :-)

### Beispiel

![DNF-Download-Settings](https://github.com/friedlandreas/Guides/blob/67e9e7d5f6035df6c3c89cc9899b9b388070bf62/images/DNF-Download-Setting.png)

