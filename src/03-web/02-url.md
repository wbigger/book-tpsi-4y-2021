# URL

L'URL (Uniform Resource Locator) è uno dei mattoncini base del web e serve per identificare in maniera univoca una risorsa all'interno del web stesso. Volendo fare un paragone, è l'equivalente dell'IP per Internet.

Una risorsa può essere teoricamente qualsiasi cosa, ma tipicamente è una delle seguenti:
- una pagina web (.html)
- un file (es. immagine, audio)
- un JSON (una stringa di testo contenente informazioni)

## Sintassi
Un URL ha la seguente sintassi:

`protocollo://host/percorso?query#fragment`

Vediamo di seguito in dettaglio ogni parte.

### Protocollo
I protocolli che usiamo solitamente sono:
- http (da usare con cautela perché non sicuro)
- https

Altri protocolli molto usati sono:
- ftp per trasferire i file
- ssh per aprire una sessione remota

### Host
L'host è la macchina su cui si trova la risorsa. Può essere:
- un indirizzo IP (IPv4 o IPv6)
- un nome di dominio (es. google.com)

Per maggiori informazioni su come viene mappato un indirizzo IP ad un nome di dominio, rimando a [questa pagina](https://wbigger.github.io/book-tpsi-5y/04-deploy/04-domains.html).

### Percorso
Il percorso individua la risorsa all'interno dell'host. Può essere il path di un file all'interno della macchina, oppure un percorso generico che viene _instradato_ (_routed_) dal web server verso una specifica funzione che si occuperà di gestire la richiesta.

### Query
La _query_ serve per modificare in qualche modo la richiesta della risorsa.
Ad esempio, se la risorsa è la lista dei prodotto di abbigliamento di un certo ecommerce, attraverso una query posso chiedere di visualizzare solo i prodotti con un certo prezzo, o solo i primi 10 prodotti, etc.

### Fragment
Un _fragment_ individua una porzione della risorsa restituita.

Per le pagine web, ad esempio, ogni id crea un nuovo fragment. Posso quindi saltare ad un certo punto di una pagina specificando l'id al termine dell'URL, come in [questo](https://en.wikipedia.org/wiki/URI_fragment#Basics) caso.
