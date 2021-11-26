# Classi

Finora abbiamo visto solo i tipi base. Ma se volessimo rappresentare nel nostro mondo qualcosa di più complesso? Ad esempio se volessimo rappresentare in modo semplice un libro con diverse caratteristiche, come ad esempio autore, titolo, numero di pagine, peso, colore? Ci servirebbe un modo per comporre i tipi base insieme, per costruire il concetto che vogliamo rappresentare, un po' come dei mattoncini lego che costruiscono un oggetto più grande.

Il modo più comune in informatica per raggiungere questo obiettivo è creare delle **classi** di oggetti.

> Come sempre, nei diversi linguaggi di programmazione ci sono moltissime varianti del concetto di classe. Noi per ora ci limitiamo a vedere C++ e Python (nota: C non ha il concetto di classe).

Una classe possiamo immaginarla come uno _stampino_ per creare _oggetti_ tutti simili fra di loro.

Useremo in modo estensivo le classi, quindi è bene cominciare a prendere subito familiarità con questo concetto.

> Per approfondimenti vedi anche il materiale del [secondo anno](https://wbigger.github.io/book-programming/chap2/01-classes.html).

Quando da una classe creiamo un oggetto, dobbiamo dire al programma come fare a _costruire_ quel dato oggetto, ad esempio qual'è il titolo del libro, o l'autore, e così via. Abbiamo quindi bisogno di una funzione che ci aiuti in questo compito; tale funzione prende il nome di _costruttore_ della classe.