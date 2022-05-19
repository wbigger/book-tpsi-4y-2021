# Modello client-server

Prima di passare a vedere nel dettaglio le tecnologie web, vediamo il paradigma su cui si basa il web stesso: il modello client-server.

Nel web, si distinguono nettamente due diverse macchine:
- il client, che invia la richiesta e visualizza una pagina web
- il server, che riceve le richieste e fornisce le pagine web da visualizzare

<p align="center">
<img title="prompt" src='./assets/client-server.png' width='70%' style="padding: 50px 0 30px 0;">
</p>

## Client
Il client è una qualsiasi macchina che visualizza le pagine web, ad esempio:
- un computer desktop
- uno smartphone
- uno smartwatch
- una smartTV
- ...

Il programma che visualizza le pagine web viene normalmente chiamato _browser_.

Esistono tanti browser differenti, ma quasi tutti sono delle varianti di questi tre:
- Chrome/Chromium, da cui deriva ad esempio Edge e Safari
- Firefox
- Opera

Nel browser possiamo usare solo HTML, CSS e JavaScript per le nostre pagine.

## Server
Il server ha il compito di gestire le richieste dei client.

Client e server, nel mondo web, comunicano tramite il protocollo _HTTP_. L'applicazione software all'interno del server che ha il compito specifico di riceve le chiamate HTTP, passarle ad un'altra applicazione, ricevere la risposta da questa applicazione e ritornare una risposta HTTP al client viene chiamata _web server_. Ad esempio, un web server molto comune in Python è _Flask_.

Sul server abbiamo una maggiore libertà di scelta delle tecnologie da usare rispetto al client. Possiamo usare una vasta gamma di linguaggi di programmazione tra cui PHP, Java, Python, C++, Rust, etc.



