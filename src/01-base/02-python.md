# Python



Il linguaggio che vedremo quest'anno è [Python](https://www.python.org/). Python è un linguaggio completamente open-source, il codice sorgente è reperibile sulla pagina [ufficiale di GitHub](https://github.com/python) ed è rilasciato sotto la [Python License](https://opensource.org/licenses/Python-2.0).

<p style="margin:auto;width:500px">
<img class="right_side w20p" title="Python logo" alt="Python logo" src="assets/python-logo.png" width=200>
<img class="left_side" title="Guido van Rossum" alt="Python logo" src="assets/guido-van-rossum.jpg" width=200>
</p>

Python è stato creato alla fine degli anni '80 dall'olandese [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum), all'età di circa trent'anni. Come molti colleghi nell'ambito informatico, il suo operato è stato costantemente guidato da alcuni ideali, in particolare van Rossum credeva che la programmazione dovesse essere accessibile a tutti; le sue scelte per la sintassi del linguaggio hanno avuto sempre questa direzione. Nel 1999 sono state pubblicate delle linee guida che riassumevano questi concetti, conosciute come ["The Zen of Python"](https://www.python.org/dev/peps/pep-0020/).

> È anche possibile leggere queste linee guida direttamente dentro Python, scrivendo `import this` :)

> Se volete provare gli snippet di codice in questa pagina, potete usare il [playground online](https://code.sololearn.com/#py) di SoloLearn.

## Caratteristiche
Python ha una sintassi essenziale, eliminando quasi tutta la punteggiatura.

Esempio di un programma Python completo e valido:

```py
catalogue = ["Harry Potter e il calice di fuoco", "Il rosso e il nero", "Il piccolo principe"]
for title in catalogue:
   print(title)
print("goodbye")
```

Nella prima riga, viene dichiarata una nuova variabile `catalogue`. Il tipo della variabile viene _inferito_ dal valore assegnato; in questo caso, siccome assegniamo qualcosa che è tra parentesi quadre, il tipo di `catalogue` è una lista. Fate attenzione: la riga _non_ finisce con il punto e virgola!

Nella seconda riga c'è un ciclo `for`. Notate che non ci sono parentesi di nessun tipo, né tonde né graffe; attenzione però che la riga in questo caso finisce con i due punti Le stesse regole valgono anche per il condizionale `if`. 

Ma se non ci sono parentesi graffe, come si fa a sapere dove finisce il contenuto del ciclo `for`? Qui c'è la scelta un po' azzardata di van Rossum: usare l'indentazione del codice per definire dove finiscono i blocchi, ed obbligare lo sviluppatore ad usare le buone pratiche di indentazione. Una scelta che con il tempo tutto sommato ha ripagato!

Quindi vediamo che il contenuto del `for` è solo `print(title)`, mentre la riga successiva, la quarta, è fuori dal ciclo.

Se eseguiamo il codice, avremo il seguente output su console:

```txt
Harry Potter e il calice di fuoco
Il rosso e il nero
Il piccolo principe
goodbye
```

## Importare una libreria esterna
Se ci servono delle librerie esterne per fare delle operazioni particolari, su usano le keyword `import` e `from`. Ad esempio immaginiamo di voler stampare la data e l'ora attuali. 

```py
from datetime import datetime
print(datetime.now())
```

che avrà come output il giorno e l'ora attuali, ad esempio:

```
2019-11-29 21:57:27.676783
```

In generale, dopo il `from` ci va il nome di un file Python (senza estensione), e dopo `import` il nome di una variabile. In questo esempio, nella prima riga importiamo la variabile `datetime` da un file che si chiama con lo stesso nome. Il file `datetime` nel caso specifico non è creato da noi ma è una libreria di sistema, ma possiamo usare la stessa sintassi anche per i nostri file.

### Librerie aggiuntive
Solo le librerie esterne più comuni, come `datetime`, sono già pre-installate in Python. Esistono infatti decine di migliaia di librerie, in continuo cambiamento, scaricarle tutte all'inizio sarebbe impossibile oltre che inutile! 

Fortunatamente esiste un semplice comando per scaricare ed installare nuove librerie. Aprire un terminale sul proprio computer (anche all'interno di Visual Studio Code), e scrivere:

```
pip3 install <nome-libreria>
```

Vediamo che `pip3` è un comando che gestisce i pacchetti Python (Pip sta per "Pip installs package", è un acronimo ricorsivo), e `<nome-libreria>` è il nome della libreria che vogliamo scaricare.

## Riferimenti W3Schools

Il sito w3schools è un buon riferimento per imparare il Python. Consigliamo in particolare le seguenti pagine:
- [Tipi base](https://www.w3schools.com/python/python_datatypes.asp)
- [Liste](https://www.w3schools.com/python/python_lists.asp)
- [For loop](https://www.w3schools.com/python/python_for_loops.asp)
- [Funzioni](https://www.w3schools.com/python/python_functions.asp)
- [Classi](https://www.w3schools.com/python/python_classes.asp)

A breve ci serviranno anche i seguenti concetti:
- [JSON](https://www.w3schools.com/python/python_json.asp)
- [PIP](https://www.w3schools.com/python/python_pip.asp)