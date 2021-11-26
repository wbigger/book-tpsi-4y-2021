# Creare una web app con HTML5 e Python
Vorrei collegarmi subito a quello che state studiando in TPSI quest'anno e creare una semplicissima applicazione con HTML e Python.

## Caso di studio
Immaginiamo di voler gestire una biblioteca scolastica. Da un lato ci serve del codice che gira da qualche parte nel cloud che gestisce la biblioteca, ed una pagina web per poter visualizzare la lista dei libri.

Useremo Python per la prima parte (server), e HTML per la seconda parte (pagina web).

<svg height='140' width='100%'>
   
   <rect width='40%' height='100%' style='fill:rgb(0,0,0);stroke-width:3;stroke:rgb(0,0,0)'/>

   <text x="15%" y="50%" font-size="30" text-anchor="middle" fill="white">
   HTML
   </text>

   <rect width='40%' height='100%' style='fill:rgb(0,255,0);stroke-width:3;stroke:rgb(0,0,0)' x="60%"/>

   <text x="75%" y="50%" font-size="30" text-anchor="middle" fill="white">
   Python
   </text>
</svg>

## Python
Immaginiamo in maniera veramente minimale che il nostro catalogo sia formato solo dal seguente file Python, a cui diamo il nome di `library.py`.

```py
# library.py
catalogue = ["Harry Potter e il calice di fuoco", "Il rosso e il nero", "Il piccolo principe"]
```

Più essenziale di così, si muore... eppure è un codice valido e funzionante.

### Web server
Per poter far comunicare Python con la pagina HTML però, serve qualcuno che faccia da intermediario. Non posso infatti chiamare del codice Python direttamente dalla pagina web! Le pagine web possono infatti interagire unicamente tramite dei link, o più precisamente degli URL, e noi ancora non abbiamo nulla del genere.

L'intermediario che mette in comunicazione pagina web e codice sul server si chiama, in modo non troppo sorprendente, **web server**. Vediamo come si fa su Python.

Esistono diverse librerie che forniscono un web server, noi in questo tutorial useremo [Flask](https://www.palletsprojects.com/p/flask/), che è estremamente leggero e semplice da usare, anche se magari non ha tutte le funzionalità che offrono altre librerie.

Essendo una libreria esterna non di sistema, bisogna prima di tutto installarla. Come abbiamo visto, apriamo un terminale e scriviamo:
```
pip3 install flask
```

et voilà! La libreria è installata e pronta all'uso.

Ora creiamo un nuovo file nel nostro progetto, che chiamiamo `app.py`. Attenzione: il nome deve essere esattamente questo, altrimenti non funziona tutto automagicamente 🎩.

```py
from flask import Flask
from library import catalogue
import json

app = Flask("marconi")

@app.route("/")
def data_book():
    return json.dumps(
        [book for book in catalogue]
        )
```

Vediamo cosa abbiamo fatto. Abbiamo importato `Flask` dalla libreria `flask` e il nostro catalogo dal file `library` che abbiamo creato precedentemente. Importiamo anche la libreria di sistema `json`, che è utile per convertire le variabili Python nel formato stringa JSON (vedi dopo. 

La riga `app = Flask("marconi")` crea un web server e gli da il nome di "marconi" (possiamo mettere quello che preferiamo).

La riga `@app.route("/")` è un'annotazione: sta ad indicare che la funzione successiva deve essere chiamata quando qualcuno prova ad accedere alla pagina web.

La funzione `data_book()` viene quindi chiamata quando interroghiamo il web server. Questa funzione ritorna il nostro catalogo in formato JSON. È formata dalle seguenti parti:
- `json.dumps()` è una funzione che converte il parametro che gli viene passato in formato JSON
- `[book for book in catalogue]` è una sintassi tipica di Python, che crea una nuova lista con all'interno tutti gli elementi di `catalogue`.

Nel dettaglio, stiamo dicendo che per ogni elemento `book` all'interno della lista `catalogue`, vogliamo creare un elemento con esattamente lo stesso valore di `book`.

La precedente forma compatta è equivalente al seguente codice:

```py
mylist = []
for book in catalogue:
    mylist.append(book)
```

Come si può vedere, nella forma compatta non abbiamo bisogno di dichiarare la variabile di appoggio `mylist`.

Attenzione: se book **non** fosse un tipo base ma un oggetto, questa sintassi non va bene, perché Python non saprebbe come convertire automaticamente un oggetto ti tipo `Book` in una stringa JSON. Per risolvere il problema, possiamo dire a Python che per trasformare l'oggetto in JSON deve associare ad ogni proprietà della classe Book una corrispondente proprietà nella stringa JSON. Per fare questo possiamo usare la proprietà `__dict__`, che come potete intuire dal doppio trattino basso all'inizio e alla fine, è una proprietà di sistema, assegnata automaticamente a tutti gli oggetti di una classe. La funzione precedente diventerebbe quindi:

```py
def data_book():
    return json.dumps(
        [book.__dict__ for book in catalogue]
        )
```



### Il formato JSON
Fate attenzione: [JSON](https://www.json.org/) è un formato per scambiarsi i dati tra macchine (machine-to-machine), ma che può essere letto e scritto abbastanza facilmente anche dagli esseri umani. JSON quindi non è un codice, o un'applicazione, o una libreria, ma è un formato di stringa che permette alle macchine di comunicare fra loro in modo comprensibile. Volendo fare un paragone con la lingua umana, è come la sintassi della frase: per capirsi le persone devono mettere nel corretto ordine soggetto, verbo e complementi, altrimenti non ci si capisce.

JSON usa le seguenti convenzioni:
- le parentesi graffe per definire gli oggetti
- le parentesi quadre per le liste
- la virgola per separare gli elementi di una lista
- i due punti per definire le proprietà di un oggetto

Ad esempio, per definire una lista di due oggetti, ognuno con le proprietà `title` e `author`, scriveremo:
```json
[
    {
        "title":"Harry Potter e il calice di fuoco",
        "author":"J.K.Rowling"
    },
    {
        "title":"Il rosso e il nero",
        "author":"Stendhal"
    },
    {
        "title":"Il piccolo principe",
        "author":"Antoine de Saint-Exupéry"
    }
]
```
Per generare o validare stringhe JSON, è possibile usare servizi online come ad esempio [JSON lint](https://jsonlint.com/?json=[{%22title%22:%22Harry%20Potter%20e%20il%20calice%20di%20fuoco%22,%22author%22:%22J.K.Rowling%22},{%22title%22:%22Il%20rosso%20e%20il%20nero%22,%22author%22:%22Stendhal%22},{%22title%22:%22Il%20piccolo%20principe%22,%22author%22:%22Antoine%20de%20Saint-Exup%C3%A9ry%22}]).

### Lanciare il web server
Per lanciare il web server, aprite un terminale nella cartella del vostro progetto e scrivete:

```
python3 -m flask run
```
Se tutto va bene, vi dovrebbe comparire la scritta `Running on http://127.0.0.1:5000/`. Ecco quindi il link che ci serviva per far comunicare la pagina web con la nostra applicazione!

## HTML
Ora creiamo un nuovo file, sempre nel nostro progetto, che chiamiamo `index.html`.

```hmtl
<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Biblioteca scolastica</title>
</head>
<body>
    <ul>
    </ul>    
</body>
</html>
```

È una semplice pagina che visualizza una lista, in questo momento vuota.

Come facciamo a riempire la lista con i dati presi dal web server? Ci serve un po' di JavaScript.


### JavaScript
Subito dopo il tag `</body>` e subito prima del tag `</html>`, nella penultima riga insomma, aggiungiamo il codice che ci serve. 

Prima di tutto scarichiamo ed importiamo una libreria JavaScript che ci semplificherà molto la vita e chi si chiama [JQuery](https://jquery.com). Potete scaricare il file direttamente cliccando con il tasto destro [qui](https://code.jquery.com/jquery-3.4.1.min.js) e scegliendo "Salva link come" o qualcosa di simile. Salvate il file sempre nella cartella di progetto.

Quindi aggiungiamo la seguente riga:
```html
<script src="jquery-3.4.1.min.js"></script>
```

OK, abbiamo importato la libreria. Ora dobbiamo prendere i dati dal web server. Lo facciamo scrivendo subito dopo un nostro pezzo di codice all'interno del tag `<script>`.

```html
<script>
    // Prende i dati come JSON dall'URL
    // quando ha finito di prendere i dati, chiama la funzione "makeList"
    $.getJSON("http://127.0.0.1:5000/").done(makeList);
</script>
```

Attenzione a quello che succede. Il codice dentro il tag script è JavaScript. Il simbolo del dollaro (`$`) indica che stiamo usando la libreria JQuery che abbiamo importato subito prima. Quando i dati sono stati completamente ricevuti (ci potrebbe volere del tempo, se i libri fossero molti), viene chiamata la funzione `makeList`, che dobbiamo ancora definire.

Subito dopo la riga precedente, creiamo ora la funzione `makeList`:
```js
function makeList(jsonBooks) {
    for (book of jsonBooks) {
        let newItem = `<li>${book}</li>`;
        $("ul").append(newItem);
    }
}
```

Vediamo cosa abbiamo fatto. Nella prima riga abbiamo creato una funzione con la keyword `function`; la funzione prende in input un parametro che gli viene passato da JQuery quando i dati sono stati ricevuti.

Subito dopo c'è un ciclo `for`, molto simile a quello del Python, con qualche differenza:
- JavaScript usa le parentesi dopo la keyword `for`
- JavaScript usa la keyword `of` invece che `in` per iterare all'interno di una lista
- JavaScript usa le parentesi graffe per contenere il corpo del `for`


All'interno del `for`, nella prima riga creiamo il nuovo item che vogliamo andare ad aggiungere alla lista.

Nella riga successiva, c'è un istruzione che dice:
- usando JQuery (`$`), seleziona la lista non ordinata (`ul`)
- all'interno della lista, aggiungi alla fine (`append`) il nuovo elemento appena creato

Il codice finale di tutta la pagina verrà come segue:
```hmtl
<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Biblioteca scolastica</title>
</head>
<body>
    <ul>
    </ul>    
</body>
<script src="jquery-3.4.1.min.js"></script>
<script>
    // Prende i dati come JSON dall'URL
    // quando ha finito di prendere i dati, chiama la funzione "makeList"
    $.getJSON("http://127.0.0.1:5000/").done(makeList);
    function makeList(jsonBooks) {
    for (book of jsonBooks) {
        let newItem = `<li>${book}</li>`;
        $("ul").append(newItem);
    }
}
</script>
</html>
```

### Go Live
Su Visual Studio Code (detto anche VSCode per brevità), potete lanciare questa pagina con "Go Live" nella barra in basso, lo trovate sulla destra. Se non lo vedete, assicuratevi di aver installato l'estensione "Live Server" su VSCode.

Al primo lancio vedrete che non succede niente. Per controllare cosa è successo, aprite la console di debug premendo con il tasto destro in qualsiasi punto della pagina web nel browser e cliccando su "Analizza elemento" o "Ispeziona elemento", quindi nel pannello che si apre, selezionate la tab console.

Se avete fatto tutto correttamente, dovrebbe comparirvi un messaggio di errore del tipo:
```
Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at http://127.0.0.1:5000/. (Reason: CORS header ‘Access-Control-Allow-Origin’ missing).
```

È normale, perché state usando due web-server diversi per la stessa pagina, questa è una cosa potenzialmente pericolosa ed il browser vi impedisce di farlo. Per aggirare la limitazione, il modo più semplice è installare queste estensioni per [Firefox](https://addons.mozilla.org/it/firefox/addon/cors-everywhere/) o per [Chrome](https://chrome.google.com/webstore/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf). In questo modo vi caricherà la pagina correttamente anche in questo caso.

> Ovviamente non è questo il modo più corretto di procedere. Per fare le cose per bene, bisogna spostare tutto su Flask, anche le pagine HTML. È un'operazione abbastanza semplice ma la vedremo dopo che vi sarete impratichiti con questa parte.
