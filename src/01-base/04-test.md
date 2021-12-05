# Test del gioco
Prima di andare avanti, è bene creare dei "test" che ci permettano di assicurarci che, qualsiasi modifica faremo in futuro al nostro codice, le funzionalità continueranno sempre ad essere corrette.

I test sono uno degli strumenti più importanti nella cassetta degli sviluppatori per poter scrivere del buon codice .

## Creazione del file di test
Creiamo un nuovo file chiamato `test_tris.py`. In generale si usa la convenzione che il file di test ha lo stesso nome del file che deve testare, con il prefisso `test_`.

Come prima riga, importiamo la funzione che vogliamo testare.

```py
from tris import win
```
Ricordiamo che dopo il `from` mettiamo il nome del file, senza `.py`, e dopo `import` i nomi delle funzioni o delle variabili che vogliamo importare.

Ora creiamo una funzione di test. Ogni funzione deve avere al suo interno l'istruzione `assert` con la condizione che si vuole verificare sia vera.

```py
def test_win_1():
    board = [
              ['X','X','X'],
              ['-','O','O'],
              ['-','-','-']
            ]
    assert win(board) == 'X'
```

Alla fine del file dobbiamo ricordarci di chiamare le funzioni di test.

```py
# definisco tutte le funzioni...
 
test_win_1()
# ...chiamo tutte le funzioni di test...
```

## Funzioni di test

"Un programmatore entra in un pub ed ordina una birra, 2 birre, 10 birre, 1000 birre, 0 birre, -1 birra, asdasdqwe birre."

Questa "barzelletta" nerd ricorda come dovrebbero disegnarsi i test. Bisogna testare tutte le condizioni "normali", che ci si aspetta, e cercare di immaginarsi anche tutte le cose che potrebbero andare storte.

Nel nostro caso dobbiamo prevedere:
- 8 test per la vittoria di 'X' (3 righe, 3 colonne, 2 diagonali)
- 8 test per la vittoria di 'O'
- un certo numero di test per le situazioni di non vittoria (il gioco continua)

## Adattamento del file app.py
Quando importiamo la funzione `win`, l'interprete di Python esegue tutto il file "tris.py", compresa la parte finale in cui chiede l'input dei giocatori. Non è però quello che vogliamo quando importiamo un file come libreria.

Per risolvere questo problema, Python mette a disposizione la variabile di ambiente `__name__` che assume un valore diverso in base a come è invocato il file. Per **variabile di ambiente** si intende una variabile che non è creata o assegnata direttamente da noi nel file, ma è esterna ad esso, gestita dall'interprete o dal sistema operativo. In Python queste variabili hanno sempre un doppio trattino basso come prefisso, e per questo sono anche chiamate _dunder variables_(abbreviazione di _double under score variables_), oppure _magic variables_.

In particolare, la variabile __name__ assume il valore: 
- `"__main__"` se il file è chiamato direttamente 
- il nome del modulo in cui si trova, che di default è uguale al nome del file

In altre parole, per non eseguire del codice quando il file viene importato come libreria, dobbiamo aggiungere la condizione:

```py
if __name__ == "__main__":
  # codice da eseguire
```

## Versione definitiva del codice
Potete trovare la versione completa del codice [qui](https://github.com/wbigger/2021-tris/tree/v1.0-CLI).