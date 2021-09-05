Es gibt manchmal mal das Problem unter Exchange Server 2013 und 2016 dass Emails nicht versendet werden und in Entwürfe (Drafts) bzw. manchmal auch in Postausgang hängen bleiben.

Das Problem tritt sowohl in Outlook als auch in der Outlook Web App (OWA) auf.

Der Grund war bei mir bisher immer eine fehlerhafte DNS-Konfiguration des Exchanges!

Vor allem bei mehreren Netzwerkkarten oder bei mehreren DNS-Servern kann hier die Automatik versagen.

**Einzustellen ist das am einfachsten in der ECP:**

![](https://github.com/friedlandreas/Guides/blob/84a1b3b74f92a09da4a3c1057d551d4ae26905b4/images/Mail-stuck-drafts-01.png)

**Hier stehen die DNS-Lookups (intern und extern) standardmäßig auf „Alle Netzwerkkarten“:**

![](https://github.com/friedlandreas/Guides/blob/84a1b3b74f92a09da4a3c1057d551d4ae26905b4/images/Mail-stuck-drafts-02.png)

**Hier kann die richtige Netzwerkkarte ausgewählt werden – oder auch ein DNS-Server manuell eingetragen werden:**

![](https://github.com/friedlandreas/Guides/blob/84a1b3b74f92a09da4a3c1057d551d4ae26905b4/images/Mail-stuck-drafts-03.png)

Danach sollte das Problem gelöst sein 🙂
