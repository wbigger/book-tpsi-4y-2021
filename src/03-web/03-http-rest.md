# Metodi HTTP ed architettura REST

Come sappiamo, tutto il web si basa sul concetto di risorsa. In HTTP, per manipolare una risorsa usiamo i _metodi_, per questo è di particolare importanza capire bene cosa sono e come si usano.

Quando interagiamo con un qualsiasi risorsa, i diversi comandi che possiamo usare per manipolarla rientrano all'interno delle operazioni cosiddette **CRUD**: **C**reate, **R**ead, **U**pdate e **D**elete.

Di seguito una semplice tabellina che fa un paragone tra metodi HTTP e database SQL, che può esservi utile anche l'anno prossimo.

| Operazione  | SQL | HTTP/REST |
|---|---|---|
| Create |INSERT|POST (o PUT)|
| Read  |SELECT|GET|
| Update  |UPDATE|PUT / PATCH|
| Delete  |DELETE|DELETE|



## GET: selezione della risorsa
Per leggere il valore di una risorsa, usiamo l'URL della risorsa stessa ed effettuiamo la richiesta HTTP con il metodo `GET`. Ci si aspetta che lo stato della risorsa non cambi a seguito di questa chiamata.

## POST e PUT: creazione e modifica di una risorsa
Per creare una nuova risorsa si usa il metodo `POST`, specificando nel corpo i dati per la creazione della risorsa stessa. A seguito di una chiamata con successo di questo metodo, il server ritorna l'ID univoco della risorsa appena creata.

Nota: in alcuni casi si utilizza anche il metodo `PUT` per creare una nuova risorsa. Si utilizza questa strategia quando l'ID della risorsa viene fornita dal client e non deve essere generata dal server. Di solito in questo caso se la risorsa non esiste viene creata, mentre se esiste viene sovrascritta.

Nei casi di incertezza, le specifiche HTTP ci ricordano che una differenza sostanziale tra `POST` e `PUT` è l'idempotenza, come spiegato di seguito.

### Idempotenza
Per capire bene la differenza tra `POST` e `PUT`, dobbiamo introdurre il concetto di idempotenza. Un comando è _idempotente_ quando _"richieste ripetute identiche devono portare al medesimo stato dei dati sul server"_. 

Per le chiamate HTTP:

- `GET` è idempotente: facendo più richieste identiche, la risorsa è immutata ed ottengo sempre la stessa risposta

- `PUT` è idempotente: facendo più richieste identiche, il DB viene modificato solo la prima volta

- `POST` non è idempotente: facendo più richieste identiche, ad ogni chiamata verrà aggiunta una nuova risorsa e creato un nuovo ID per noi

Nella pratica, questo significa che quando uso `PUT` devo passare anche l'ID dell'elemento da creare o aggiornare, mentre con `POST` non devo fornire l'ID, perché verrà creata dal server.

Approfondimento sul concetto di idempotenza [qui]( http://blog.loris.tissino.it/2013/06/http-rest-e-api.html).

## UPDATE: modifica parziale di una risorsa
Con il metodo `UPDATE` è possibile aggiornare solo parte di una risorsa, senza doverla sovrascrivere interamente.

## DELETE: cancellazione di una risorsa
Il metodo `DELETE` permette di cancellare la o le riorse specificate.