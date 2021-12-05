# Test del gioco
Prima di andare avanti, è bene creare una struttura di test che ci permetta di assicurarci che, qualsiasi modifica faremo in futuro al nostro codice, le funzionalità base continueranno sempre ad essere corrette.

I test sono uno degli strumenti più importanti nella cassetta degli sviluppatori per poter scrivere del buon codice nel tempo.

## Creazione del file di test
Creiamo un nuovo file chiamato `test_tris.py`. In generale il file di test ha lo stesso nome del file che deve testare, con il prefisso `test_`.

Come prima riga, importiamo la funzione che vogliamo testare.

```py
from tris import win
```

Ora creiamo una funzione di test. Ogni funzione deve avere al suo interno l'istruzione `assert` con la condizione che si vuole testare.

```py
def test_win_1():
    board = [
              ['X','X','X'],
              ['-','O','O'],
              ['-','-','-']
            ]
    assert win(board) == 'X'
```

Alla fine della funzione di test dobbiamo ricordarci di chiamare il test.

```py
test_win_1()
```

## Funzioni di test

"Un programmatore entra in un pub ed ordina una birra, 2 birre, 10 birre, 1000 birre, 0 birre, -1 birra, asdasdqwe birre."

Questa "barzelletta" nerd ricorda come dovrebbero disegnarsi i test. Bisogna testare tutte le condizioni "normali", che ci si aspetta, e cercare di immaginarsi anche tutte le cose che potrebbero andare storte.

Nel nostro caso dobbiamo prevedere:
- 8 test per la vittoria di 'X' (3 righe, 3 colonne, 2 diagonali)
- 8 test per la vittoria di 'O'
- un certo numero di test per le situazioni di non vittoria (il gioco continua)