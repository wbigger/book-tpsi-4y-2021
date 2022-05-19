# HTTP

L'HTTP (HyperText Transfer Protocol) è il principale protocollo a livello applicativo (livello 7 ISO/OSI) che si usa per il web. Le specifiche sono gestite direttamente dal w3c.

L'HTTP si fonda su un'architettura di tipo client-server. Il _client_ per definizione è _la macchina che effettua la richiesta_, mentre il _server_ è _la macchina che gestisce la richiesta e fornisce una risposta_.

> Una stessa macchina, in momenti diversi, si può comportare sia da client che da server.

Il protocollo HTTP prevede quindi due messaggi: la richiesta (_request_, da client a server) e la risposta (_response_, da server a client).

<object data="assets/http-arrows.html" style="width:100%;"> 
    Your browser doesn’t support the object tag. 
</object>

L'HTTP di default comunica attraverso la porta 80. Quando usiamo un browser senza specificare la porta, il browser stesso aggiunge automaticamente questa porta di default per noi.

## Versione sicura
L'HTTP trasmette l'intestazione ed il corpo del messaggio in chiaro, cioè in modo non criptato, ponendo dei problemi sia di sicurezza quando si scambiano delle credenziali, sia di privacy, in quanto un qualsiasi utente che si pone in ascolto del nostro traffico (detto anche _man-in-the-middle_) ha libero accesso al conenuto di tutti i messaggi inviati e ricevuti.

Per ovviare a questo problema, è nato il protocollo HTTPS (_HTTP Secure_), che utilizza un layer di cifratura di tipo SSL/TLS per criptare la comunicazione. 

NOTA: l'HTTPS nasconde il contenuto del messaggio (intestazione e corpo), ma non l'URL stesso, quindi un man-in-the-middle può comunque sapere verso quali siti stiamo navigando. Per aumentare la privacy, è in fase di fase di approvazione il protocollo _DNS over HTTPS_ (abbreviato in DoH) per criptare anche la comunicazione tra il browser ed il server DNS.

L'HTTPs di default comunica attraverso la porta 443.

## Sessioni e cookies
L'HTTP è un protocollo senza stato ("stateless"), cioé a livello di protocollo ogni richiesta è del tutto indipendente dalla precedente. Come può fare quindi il server a sapere che più richieste provengono dalla stessa macchina, ad esempio per mantenere lo stato del carrello? In altre parole, come fanno client e server a mantenere una _sessione_ persistente tra più messaggi HTTP?

Per fare questo, si utilizza in generale la strategia dei _cookies_ (biscotti). Client e server concordano una stringa casuale che verrà trasmessa nell'header di tutte le richieste HTTP, in modo che il server possa tenere traccia delle varie richieste.

Ovviamente, se qualcuno venisse a conoscenza dei nostri cookies, li potrebbe utilizzare per violare la nostra privacy o per truffarci. È quindi importante che i cookies siano adeguatamente protetti in tutta lo loro vita:
- il browser deve assicurare che solo il sito che ha generato il cookie può accederci e nessun altro
- deve essere usato il protocollo HTTPS, per criptare l'intestazione della richiesta che contiene il cookie stesso


## Request
Una richiesta HTTP è formata da:
- una linea di richiesta (_request line_), dove viene specificato il metodo, l'URL di destinazione ed il protocollo richiesto (in genere HTTP/1.1)

```
GET /image/logo.png HTTP/1.1
```

> In questo esempio, nella linea di richiesta ho solo la parte dell'URL che segue il dominio, in quanto l'host viene specificato successivamente nell'intestazione.

- un'intestazione (_header_), formata da una serie di campi (_fields_), con la sintassi `nome:valore`

```
Host:www.example.com
Accept-language:en
```

- opzionalmente il corpo del messaggio (_message body_)

### Metodi HTTP
I metodi HTTP sono una parte fondamentale del protocollo, indicano l'azione desiderata del client riguardo la risorsa specificata nell'URL.

Questo argomento merita una pagina a parte, trovate tutti i dettagli [qui](./03-http-rest.html).

### Request header fields
I più comuni campi dell'intestazione della richiesta sono:

- `Host`: l'unico campo obbligatorio da HTTP/1.1, con l'IP o il dominio che identifica il server di destinazione
- `User-agent`: specifica il browser utilizzato dal client, ad esempio nel mio caso è `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.64 Safari/537.36`
- `Accept-language`: specifica in quale lingua il client si aspetta la risposta
- `Cookie`: una stringa che identifica il _cookie_ per mantenere lo stato tra client e server, come abbiamo visto in precedenza

Per una lista completa, potete consultare il [sito ufficiale](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) del w3c oppure su [wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields).


## Response
Una risposta HTTP è formata da:
- una linea di stato (_status line_), che contiene la versione del protocollo di risposta, lo status code e opzionalmente una frase di risposta:
```
HTTP/1.1 200 OK
```
- un'intestazione (_header_), formata da una serie di campi (_fields_), con la sintassi `nome:valore`, come nel caso della richiesta
```
Content-Type: text/html
```
> Nota: i campi delle intestazioni di richiesta e risposta non sono tutti uguali, alcuni sono validi solo per le domande, alcuni solo per le risposte, alcuni per entrambi.


- opzionalmente il corpo del messaggio (_message body_)

### Request header fields
I più comuni campi dell'intestazione della richiesta sono:
- `Date`: specifica la data della risposta
- `Content-Lenght`: specifica la dimensione in byte del body
- `Content-Type`: specifica il [Media-Type](https://en.wikipedia.org/wiki/Media_type#Common_examples_[10]) del body, i più comuni sono:
   - `text/html` per le pagine HTML
   - `application/json` per i messaggi JSON
   - `application/pdf` per un file PDF
   - `image/png` o `image/jpeg` per le immagini
   - `video/mp4` e `video/ogg` per i video
   - `audio/mpeg` e `audio/ogg` per l'audio

La lista completa dei possibili Media-Type la trovate [qui](https://www.iana.org/assignments/media-types/media-types.xhtml).


### Status codes
Il dato più importante in una risposta HTTP è il _codice di stato_ (status code), che identifica se la richiesta è andata a buon fine ed in caso negativo qual è stato il problema.

I codici di stato sono divisi in 5 categorie:
- 1xx informational – richiesta ricevuta, continua l'elaborazione.
- 2xx successful – l'azione è stata ricevuta con successo, compresa ed accettata.
- 3xx redirection – il client deve eseguire ulteriori azioni per soddisfare la richiesta.
- 4xx client error – la richiesta è sintatticamente scorretta o non può essere soddisfatta.
- 5xx server error – il server ha fallito nel soddisfare una richiesta apparentemente valida.

Per una lista completa degli status codes, vi consiglio di consultare la pagina ufficiale di [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
). 

Di seguito alcuni dei codici più comuni che abbiamo visto a lezione.

#### 2xx successful
200: OK. Risposta standard per le richieste HTTP andate a buon fine.

201: Created. La richiesta è stata soddisfatta, restituendo la creazione di una nuova risorsa.

#### 4xx client error
400: Bad Request. La richiesta non può essere soddisfatta a causa di errori di sintassi.

403: Forbidden. La richiesta è legittima ma il server si rifiuta di soddisfarla.

404:Not Found. La risorsa richiesta non è stata trovata ma in futuro potrebbe essere disponibile.

429: Too many requests. Il client ha effettuato troppe richieste in un intervallo di tempo ridotto.

#### 5xx server error
500: Internal Server Error. Messaggio di errore generico senza alcun dettaglio.

501: Not Implemented. Il server non è in grado di soddisfare il metodo della richiesta.

504: Gateway Timeout. Il server si sta comportando come un gateway o un proxy e non ha ricevuto una risposta tempestiva dal server di upstream.
