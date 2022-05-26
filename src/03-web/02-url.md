# URL

L'URL (Uniform Resource Locator) è uno dei mattoncini base del web e serve per identificare in maniera univoca una risorsa all'interno del web stesso. Volendo fare un paragone, è l'equivalente dell'IP per Internet.

Una risorsa può essere teoricamente qualsiasi cosa, ma tipicamente è una delle seguenti:
- una pagina web (.html)
- un file (es. immagine, audio)
- una risorsa all'interno di un database

## Sintassi
Un URL ha la seguente sintassi:

`protocol://host/path?query#fragment`

Vediamo di seguito in dettaglio ogni parte.

### Protocol
I protocolli che usiamo solitamente sono:
- http (porta 80, da usare con cautela perché non sicuro)
- https (porta 443)

Altri protocolli molto usati sono:
- ftp per trasferire i file (porta 21)
- ssh per aprire una sessione remota (porta 22)

### Host
L'_host_ è la macchina su cui si trova la risorsa. Può essere:
- un indirizzo IP (IPv4 o IPv6)
- un nome di dominio (es. www.google.com)

Per maggiori informazioni su come viene mappato un indirizzo IP ad un nome di dominio, rimando a [questa pagina](https://wbigger.github.io/book-tpsi-5y/04-deploy/04-domains.html).

### Path
Il _path_ (percorso) individua la risorsa all'interno dell'host. Può essere il path di un file all'interno della macchina, oppure un percorso generico che viene _instradato_ (_routed_) dal web server verso una specifica funzione che si occuperà di gestire la richiesta.

### Query
La _query_ (interrogazione) serve per specificare meglio la risorsa richiesta.

Ad esempio, se la risorsa è la lista dei prodotto di abbigliamento di un certo ecommerce, attraverso una query posso chiedere di visualizzare solo i prodotti con un certo prezzo, o solo i primi 10 prodotti, etc.

### Fragment
Un _fragment_ (frammento) individua una porzione della risorsa restituita.

Per le pagine web, ad esempio, ogni id crea un nuovo fragment. Posso quindi saltare ad un certo punto di una pagina specificando l'id al termine dell'URL, come in [questo](./02-url.html#sintassi) caso.
