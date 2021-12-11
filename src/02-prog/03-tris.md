# Gioco del Tris
Usiamo come caso di studio il gioco del tris (Tic Tac Toe, in inglese).

## Creazione della board di gioco
Il tabellone di gioco (board) del tris è formato da 3 righe e 3 colonne. Possiamo rappresentarlo con una matrice 3x3. 

In Python possiamo creare una matrice così:

```py
board = [
          ['-','-','-'],
          ['-','-','-'],
          ['-','-','-']
        ]
```

Come vedete, nella dichiarazione della variabile non è necessario specificare la dimensione, perché viene automaticamente inferita dal valore assegnato.

Per stampare a schermo lo stato del tabellone, possiamo scrivere un doppio ciclo che va da uno a tre:
```py
    for i in range(3):
        for j in range(3):
            print(board[i][j], end=" ")
        print()
```

La funzione `range(n)` permette di iterare tra ed 0 e n-1; in questo caso quindi `i` e `j` assumeranno i valori da 0 a 2.

> `range(n)` può essere usato per iterare in molti altri modi, vedi [qui](https://docs.python.org/3/library/stdtypes.html#ranges) per maggiori dettagli.

Mettiamo questo doppio ciclo all'interno di una funzione, in modo da poterlo richiamare quando ci è necessario.

```py
# definisco la funzione
def mostra_tabellone():
    for i in range(3):
        for j in range(3):
            print(board[i][j], end=" ")
        print()

# richiamo la funzione
mostra_tabellone()
```

Notare come tutto quello che appartiene alla funzione è indentato al suo interno, mentre ciò che non ne fa parte non ha nessuna indentazione.

Ricordiamo anche che è buona norma che le funzioni comincino con un verbo, in quanto rappresentano delle azioni.


## Richiesta di un valore in input
Per chiedere un valore in modo interattivo in input all'utente, si può usare la funzione `input()`.

Ad esempio per chiedere la riga in cui inserire il proprio segno nel tabellone, potremmo scrivere:

```py
r = input("Inserisci la riga (valori da 0 a 2): ")
```

Attenzione però: la funzione `input()` ritorna una stringa, mentre noi vorremmo avere un intero. Per convertire da stringa ad intero, possiamo usare la funzione `int()`:

```py
r = int(input("Inserisci la riga (valori da 0 a 2): "))
```

Analogamente per la colonna. Complessivamente:
```py
r = int(input("Inserisci la riga (valori da 0 a 2): "))
c = int(input("Inserisici la colonna (valori da 0 a 2): "))
```

## Inserire i simboli nel tabellone

Per inserire il simbolo di un giocatore è sufficiente assegnare il carattere nel giusto elemento della variabile tabellone:

```py
board[r][c] = symbol
```

Vogliamo ripetere questa operazione finché il tabellone non è pieno oppure finché qualcuno non ha vinto. Creiamo un ciclo viene essere eseguito 9 volte. 

```py
for idx in range(9):
    mostra_tabellone()

    r = int(input("Inserisci la riga (valori da 0 a 2): "))
    c = int(input("Inserisici la colonna (valori da 0 a 2): "))
    #  aggiungere anche condizione che r,c devono essere compresi tra 0 e 2
    if board[r][c]=='-':
        board[r][c] = 'O'
```

In questo modo però stiamo assegnando sempre il simbolo 'O' , che ovviamente non è quello che vogliamo: vogliamo alternare i simboli 'X' e 'O'. Possiamo fare in modo che per `idx` pari mettiamo un simbolo, e per i dispari l'altro. Per fare questo possiamo creare una lista con i due simboli, ed assegnare il simbolo in base all'indice, come di seguito.

```py
symList = ['X','O']

for idx in range(9):
    
    symbol = symList[idx%2]

    mostra_tabellone()

    print("Il tuo simbolo è: "+symbol)

    r = int(input("Inserisci la riga (valori da 0 a 2): "))
    c = int(input("Inserisici la colonna (valori da 0 a 2): "))
    #  aggiungere anche condizione che r,c devono essere compresi tra 0 e 2
    if board[r][c]=='-':
        board[r][c] = symbol
```

Abbiamo utilizzato l'operatore modulo (`%`), che ritorna il resto di una divisione; siccome stiamo dividendo per due, il resto potrà essere solamente `0` o `1`, quindi non potrà mai succedere che esco fuori dall'array `symList` che ha esattamente due elementi.

Con questa soluzione riusciamo ad evitare di inserire un `if`. In generale è una buona regola di programmazione ridurre il numero di condizioni, sia perché di solito facilita la lettura (le condizioni sono spesso faticose da interpretare), sia perché il codice è più facile da testare. Ovviamente è solo un suggerimento da usare in base al proprio giudizio, non un obbligo.

## Controllo dei valori di ingresso
È importante controllare sempre i valori di ingresso forniti dall'utente, per rendere il codice più robusto.

Per fare questo, ci serve un ciclo che chiede all'infinito i valori di input finché questi non sono corretti. Per uscire da un ciclo si usa la parola chiave `break`.

```py
# while True esegue un ciclo infinito
while True:
        r = int(input("Inserisci la riga (valori da 0 a 2): "))
        c = int(input("Inserisici la colonna (valori da 0 a 2): "))
        #  aggiungere anche condizione che r,c devono essere compresi tra 0 e 2
        if board[r][c]=='-':
            board[r][c] = symbol
            # break esce dal ciclo
            break
```

## Controllo della condizione di vittoria

Creiamo una funzione che controlla se qualcuno ha vinto.

Vogliamo creare una funzione che ritorni `False` nel caso in cui nessuno ha vinto, altrimenti il simbolo del vincitore.

Esistono diversi modi per realizzare questa funzione. Qui ne presento una, ma ce ne sono molte altre altrettanto valide, anche senza usare cicli `for`.

```py
def win(board):
    # ripete il controllo per ogni giocatore
    for sym in symList:
        # controlla se ci sono 3 simboli uguali in una riga
        for i in range(3):
            if board[i].count(sym)==3:
                return sym

        # controlla se ci sono 3 simboli uguali in una colonna
        for i in range(3):
            if (board[0][i]==sym and 
               board[1][i]==sym and
               board[2][i]==sym):
                return sym

        # controlla le due diagonali
        if (board[0][0]==sym and
           board[1][1]==sym and
           board[2][2]==sym):
            return sym
        if (board[0][2]==sym and
           board[1][1]==sym and
           board[2][0]==sym):
            return sym
    
    return False
```

## Codice finale

```py
#!/usr/bin/env python3

print("Gioco del tic tac toe")

board = [
          ['-','-','-'],
          ['-','-','-'],
          ['-','-','-']
        ]

symList = ['X','O']

def mostra_tabellone():
    for i in range(3):
        for j in range(3):
            print(board[i][j], end=" ")
        print()

def win(board):
    for sym in symList:

        #check rows
        for i in range(3):
            if board[i].count(sym)==3:
                return sym

        #check columns
        for i in range(3):
            if (board[0][i]==sym and 
               board[1][i]==sym and
               board[2][i]==sym):
                return sym
        # check diagonals
        if (board[0][0]==sym and
           board[1][1]==sym and
           board[2][2]==sym):
            return sym
        if (board[0][2]==sym and
           board[1][1]==sym and
           board[2][0]==sym):
            return sym
    
    return False


winner=False

for idx in range(9):
    
    symbol = symList[idx%2]

    mostra_tabellone()

    print("Il tuo simbolo è: "+symbol)

    while True:
        r = int(input("Inserisci la riga (valori da 0 a 2): "))
        c = int(input("Inserisici la colonna (valori da 0 a 2): "))
        #  aggiungere anche condizione che r,c devono essere compresi tra 0 e 2
        if board[r][c]=='-':
            board[r][c] = symbol
            break
    winner=win()
    if winner:
        break
        

mostra_tabellone()
print("The winner is... "+winner+"!")
```