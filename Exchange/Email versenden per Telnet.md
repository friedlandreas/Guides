Sehr oft muss ich per Telnet Emails verschicken – meistens aus Testzwecken bei Exchange oder auch anderen Mailserver-Installationen. Hier mal einen kleine Anleitung wie das geht:

Beispiel: Ich komme von einer freigegebenen IP (ohne Authentifikation) und will mit test@mail.local eine Email an an test@mail.extern versenden. (Die Befehle und Eingaben sind hervorgehoben- die Antworten des Servers normal)

In der Konsole sieht das so aus:

**telnet exchange.mail.local 25**  
220 exchange.mail.local Microsoft ESMTP MAIL Service ready at Sun, 23 Feb 2014 08:49:36 -0700  
**helo mail.local**  
250 host.local Hello [10.26.115.13]  
**mail from:test@mail.local**  
250 2.1.0 Sender OK  
**rcpt to:test@mail.extern**  
250 2.1.5 Recipient OK  
**data**  
354 Start mail input; end with .  
**From: Mein Anzeigename**  
**To: Empfänger Anzeigename**  
**Subject:Testemail mit Telnet**  
  
Inhalt der Testmail.  
**.**    
250 2.6.0 <8c642f92-e0e3-4c9e-b3d3-21054eed3244@exchange.domain.com> Queued mail for delivery  
**quit**  
221 2.0.0 Service closing transmission channel  
Connection to host lost.  

Somit haben wir die Email verschickt 😃
