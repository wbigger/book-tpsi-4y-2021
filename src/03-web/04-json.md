# Il formato JSON

[JSON](https://www.json.org/) è un formato usato principalmente per scambiarsi dati tra macchine (machine-to-machine), ma che può essere letto e scritto abbastanza facilmente anche dagli esseri umani. JSON quindi non è un codice, o un'applicazione, o una libreria, ma è un _formato di stringa_ (ovvero una _notazione_) che permette alle macchine di comunicare fra loro in modo comprensibile. Volendo fare un paragone con la lingua umana, è come la sintassi della frase: per capirsi le persone devono mettere nel corretto ordine soggetto, verbo e complementi, altrimenti non ci si capisce.

JSON usa le seguenti convenzioni:
- i numeri devono essere scritti così come sono (es. `12`)
- i doppi apici per definire le stringhe (es. `"hello"`)
- le parentesi quadre per le liste (es. `[...]`)
- la virgola per separare gli elementi di una lista
- le parentesi graffe per definire gli oggetti (es. `{...}`)
- i due punti per definire le proprietà di un oggetto
- le proprietà di un oggetto sono separati tra loro da una virgola

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


# Approfondimenti
Per gli interessati, consiglio questo video su Youtube su [com'è nato il formato JSON](https://www.youtube.com/watch?v=-C-JoyNuQJs)