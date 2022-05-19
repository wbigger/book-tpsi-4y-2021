# Confronto con il formato XML

Un altro formato molto usato per lo scambio di dati è l'XML, anche se i due formati hanno campi di azione un po' diversi.

XML è l'acronimo di _eXtensible Markup Language_, ed è un _metalinguaggio_ che serve sia per creare linguaggi di markup, sia per trasmettere dati.

Noi ci occuperemo solo di questo secondo uso, per confrontarlo con JSON.

Un esempio di XML valido è il seguente:
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<root>
    <studenti>
        <studente>
            <nome>Maria</nome>
            <cognome>Rossi</cognome>
            <eta>18</eta>
        </studente>
        <studente>
            <nome>Marco</nome>
            <cognome>Neri</cognome>
            <eta>17</eta>
        </studente>
    </studenti>
</root>
```

L'equivalente in JSON ha il seguente formato:
```JSON
{"studente":[
  { "nome":"Maria", "cognome":"Rossi", "eta":18 },
  { "nome":"Marco", "cognome":"Neri", "eta":17 }
]}
```

Come si può facilmente vedere, il formato JSON è molto più compatto e c'è una netta distinzione sintattica tra tipi di dati, come ad esempio l'array o il numero. In XML, infatti, non c'è una sintassi specifica per dire che `studenti` è un array o `eta` è un numero. Per aggiungere queste informazioni è necessario aggiungere degli attributi o definire un ulteriore file, detto [_schema_](https://www.w3schools.com/xml/schema_simple.asp).

È possibile passare da XML e JSON in modo più o meno automatico usando dei convertitori, ad esempio [questo](https://codebeautify.org/jsontoxml).

## Somiglianze tra XML e JSON
- entrambi sono gerarchici
- entrambi sono leggibili da essere umano
- entrambi sono facilmente interpretabili da una macchina (_parsing_)
- entrambi sono standard web che possono essere usati in JavaScript

## Differenze tra XML e JSON
- JSON non ha bisogno di tag di chiusura
- JSON usa meno caratteri
- JSON è più veloce da leggere e scrivere su JavaScript
- JSON può usare gli array
- XML ha la possibilità di specificare proprietà attraverso attributi e schemi
- XML può essere usato per creare nuovi linguaggi di markup

> Nota: se necessario, in realtà anche JSON ha la possibilità di definire dei propri schemi usando i [JSON Schema](https://json-schema.org/)

# Uso di XML
Sebbene sul web ormai si usi quasi esclusivamente il formato JSON, uno dei casi in cui vengono molto usati gli schemi XML è nello sviluppo Android, in cui tutte le pagine di un'applicazione sono definite tramite XML.

Nota: nonostante la somiglianza sintattica, HTML non è un istanza di uno schema XML. 





