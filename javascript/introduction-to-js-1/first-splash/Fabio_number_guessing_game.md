Fabio_number_guessing_game.md

Ecco una versione semplificata in italiano dei concetti e degli esempi presenti nel link che hai fornito:

**Titolo: Un primo approccio a JavaScript**

Ora che hai imparato qualcosa sulla teoria di JavaScript e su cosa puoi farci, ti daremo un'idea di come sia il processo di creazione di un semplice programma JavaScript, guidandoti attraverso un tutorial pratico. Qui costruirai passo dopo passo un semplice gioco "Indovina il numero".

**Prerequisiti:** Conoscenza di base dei computer, una comprensione di base di HTML e CSS, una comprensione di cosa sia JavaScript.
**Obiettivo:** Acquisire una prima esperienza nella scrittura di codice JavaScript e ottenere almeno una comprensione di base di cosa comporti scrivere un programma JavaScript.

Non ci aspettiamo che impari JavaScript alla fine di questo articolo, né che comprendi tutto il codice che ti chiediamo di scrivere. Vogliamo piuttosto darti un'idea di come le caratteristiche di JavaScript lavorino insieme e come sia scrivere JavaScript. Nei prossimi articoli affronterai tutte le caratteristiche mostrate qui in modo molto più dettagliato, quindi non preoccuparti se non capisci tutto subito!

**Pensare come un programmatore**

Una delle cose più difficili da imparare nella programmazione non è la sintassi da imparare, ma come applicarla per risolvere problemi reali. Devi iniziare a pensare come un programmatore: questo generalmente implica esaminare le descrizioni di ciò che il tuo programma deve fare, capire quali caratteristiche di codice sono necessarie per raggiungere quegli obiettivi e come farle lavorare insieme.

Ciò richiede una combinazione di duro lavoro, esperienza con la sintassi di programmazione e pratica, oltre a un po' di creatività. Più programmi, migliore diventerai. Non possiamo prometterti che svilupperai una "mente da programmatore" in cinque minuti, ma ti offriremo molte opportunità per esercitarti a pensare come un programmatore durante il corso.

Detto questo, diamo un'occhiata all'esempio che costruiremo in questo articolo e rivediamo il processo generale di scomposizione in compiti tangibili.

**Esempio - Gioco Indovina il numero**

In questo articolo ti mostreremo come costruire il semplice gioco che puoi vedere qui sotto:

[Qui c'è un esempio di gioco "Indovina il numero"]

Immagina che il tuo capo ti abbia dato il seguente incarico per creare questo gioco:

"Voglio che tu crei un semplice gioco di tipo 'Indovina il numero'. Dovrebbe scegliere un numero casuale tra 1 e 100, quindi sfidare il giocatore a indovinare il numero in 10 tentativi. Dopo ogni tentativo, il giocatore dovrebbe essere informato se ha indovinato o meno, e se ha sbagliato, se il tentativo era troppo basso o troppo alto. Dovrebbe anche dire al giocatore quali numeri ha indovinato in precedenza. Il gioco terminerà una volta che il giocatore indovina correttamente o una volta che finiscono i tentativi. Alla fine del gioco, al giocatore dovrebbe essere data l'opzione di ricominciare a giocare."

Guardando questo incarico, la prima cosa che possiamo fare è scomporlo in compiti semplici e azioni concrete, nel modo più simile possibile a quello di un programmatore:

1. Genera un numero casuale tra 1 e 100.
2. Registra il numero di tentativi in corso. Inizia da 1.
3. Fornisci al giocatore un modo per indovinare il numero.
4. Quando viene inviato un tentativo, registrane il valore da qualche parte in modo che l'utente possa vedere i tentativi precedenti.
5. Verifica se il numero è corretto.
6. Se è corretto:
   - Mostra un messaggio di congratulazioni.
   - Impedisci al giocatore di effettuare ulteriori tentativi (potrebbe causare problemi al gioco).
   - Mostra un controllo che consente al giocatore di riavviare il gioco.
7. Se è sbagliato e il giocatore ha ancora tentativi:
   - Informa il giocatore che ha sbagliato e se il suo tentativo era troppo alto o troppo basso.
   - Consentigli di inserire un altro tentativo.
   - Incrementa il numero di tentativi di 1.
8. Se è sbagliato e il giocatore non ha più tentativi:
   - Informa il giocatore che il gioco è finito.
   - Impedisci al giocatore di effettuare ulteriori tentativi (potrebbe causare problemi al gioco).
   - Mostra un controllo che consente al giocatore di riavviare il gioco.
9. Una volta che il gioco riparte, assicurati che la logica del gioco e l'interfaccia utente siano completamente reimpostate e torna al passo 1.

**Configurazione iniziale**

Per iniziare questo tutorial, ti chiediamo di creare una copia locale del file "number-guessing-game-start.html" (visualizzalo dal link fornito). Aprilo sia nel tuo editor di testo che nel tuo browser. Al momento vedrai un semplice titolo, un paragrafo di istruzioni e un modulo per inserire un tentativo, ma al momento il modulo non farà nulla.

Il luogo in cui aggiungeremo tutto il nostro codice è all'interno dell'elemento <script> alla fine dell'HTML:

```html
<script>
  // Il tuo codice JavaScript andrà qui
</script>
```

**Aggiungere variabili per memorizzare i dati**

Cominciamo. Innanzitutto, aggiungi le seguenti righe all'interno dell'elemento <script>:

```javascript
let randomNumber = Math.floor(Math.random() * 100) + 1;

const guesses = document.querySelector(".guesses");
const lastResult = document.querySelector(".lastResult");
const lowOrHi = document.querySelector(".lowOrHi");

const guessSubmit = document.querySelector(".guessSubmit");
const guessField = document.querySelector(".guessField");

let guessCount = 1;
let resetButton;
```

Questa sezione di codice imposta le variabili e le costanti di cui abbiamo bisogno per

 memorizzare i dati che il nostro programma utilizzerà.

Le variabili sono essenzialmente nomi per valori (come numeri o stringhe di testo). Crei una variabile con la parola chiave "let" seguita da un nome per la tua variabile.

Le costanti vengono utilizzate anche per dare nomi ai valori, ma a differenza delle variabili, non puoi modificare il valore una volta impostato. In questo caso, stiamo usando costanti per memorizzare i riferimenti a parti dell'interfaccia utente. Il testo all'interno di alcuni di questi elementi potrebbe cambiare, ma ogni costante fa sempre riferimento allo stesso elemento HTML con cui è stato inizializzato. Crei una costante con la parola chiave "const" seguita da un nome per la costante.

Puoi assegnare un valore alla tua variabile o costante con un segno uguale (=) seguito dal valore che vuoi dargli.

Nel nostro esempio:

- La prima variabile, "randomNumber", viene assegnata a un numero casuale tra 1 e 100, calcolato utilizzando un algoritmo matematico.
- Le prime tre costanti vengono utilizzate per memorizzare un riferimento ai paragrafi dei risultati nel nostro HTML e vengono utilizzate per inserire i valori nei paragrafi più avanti nel codice (nota come siano all'interno di un elemento <div>, che è a sua volta utilizzato per selezionare tutti e tre in seguito per il ripristino, quando si riavvia il gioco):

```html
<div class="resultParas">
  <p class="guesses"></p>
  <p class="lastResult"></p>
  <p class="lowOrHi"></p>
</div>
```

Le due costanti successive memorizzano i riferimenti all'input di testo del modulo e al pulsante di invio e vengono utilizzate per controllare l'invio del tentativo in seguito.

```html
<label for="guessField">Inserisci un tentativo: </label>
<input type="number" id="guessField" class="guessField" />
<input type="submit" value="Invia tentativo" class="guessSubmit" />
```

Le ultime due variabili memorizzano un conteggio di tentativi pari a 1 (usato per tenere traccia di quanti tentativi ha effettuato il giocatore) e un riferimento a un pulsante di ripristino che non esiste ancora (ma lo farà più avanti).

Nota: Imparerai molto di più sulle variabili e le costanti in seguito nel corso, a partire dal prossimo articolo.

**Funzioni**

Di seguito, aggiungi quanto segue sotto il tuo codice JavaScript precedente:

```javascript
function checkGuess() {
  alert("Sono un segnaposto");
}
```

Le funzioni sono blocchi di codice riutilizzabili che puoi scrivere una volta e far eseguire più volte, evitando la necessità di ripetere il codice tutto il tempo. Questo è davvero utile. Esistono diverse modalità per definire le funzioni, ma per ora ci concentreremo su un tipo semplice. Qui abbiamo definito una funzione utilizzando la parola chiave "function", seguita da un nome e parentesi tonde. Dopo di ciò, mettiamo due parentesi graffe ({}). All'interno delle parentesi graffe inseriamo tutto il codice che vogliamo eseguire ogni volta che chiamiamo la funzione.

Quando vogliamo eseguire il codice, digitiamo il nome della funzione seguito dalle parentesi.

Proviamo ora. Salva il tuo codice e aggiorna la pagina nel tuo browser. Poi vai nella console JavaScript degli strumenti per sviluppatori e inserisci la seguente riga:

```javascript
checkGuess();
```

Dopo aver premuto Invio, dovresti vedere comparire un avviso che dice "Sono un segnaposto"; abbiamo definito una funzione nel nostro codice che crea un avviso ogni volta che la chiamiamo.

Nota: Imparerai molto di più sulle funzioni più avanti nel corso.

**Operatori**

Gli operatori di JavaScript ci permettono di effettuare test, fare calcoli matematici, unire stringhe e altre azioni simili.

Se non l'hai già fatto, salva il tuo codice, aggiorna la pagina nel tuo browser e apri la console JavaScript degli strumenti per sviluppatori. Poi possiamo provare a digitare gli esempi mostrati di seguito: digita ciascuno di essi dalle colonne "Esempio", premi Invio dopo ciascuno e osserva i risultati che restituiscono.

Cominciamo dai operatori aritmetici, ad esempio:

| Operatore | Nome         | Esempio       |
|-----------|--------------|---------------|
| +         | Addizione    | 6 + 9         |
| -         | Sottrazione  | 20 - 15       |
| *         | Moltiplicazione | 3 * 7       |
| /         | Divisione    | 10 / 5        |

Ci sono anche alcuni operatori di abbreviazione disponibili, chiamati operatori di assegnazione composta. Ad esempio, se vuoi aggiungere un nuovo numero a uno esistente e restituire il risultato, potresti fare così:

```javascript
let numero1 = 1;
numero1 += 2;
```

Questo è equivalente a:

```javascript
let numero2 = 1;
numero2 = numero2 + 2;
```

Quando eseguiamo test vero/falso (ad esempio all'interno di condizioni, come vedremo tra poco), utilizziamo gli operatori di confronto. Ad esempio:

| Operatore | Nome              | Esempio          |
|-----------|-------------------|------------------|
| ===       | Uguaglianza rigorosa (è esattamente uguale?) | 5 === 2 + 4 // false |
|           |                   | 'Chris' === 'Bob' // false |
|           |                   | 5 === 2 + 3 // true |
|           |                   | 2 === '2' // false; numero vs stringa |
| !==       | Non uguaglianza (non è lo stesso?) | 5 !== 2 + 4 // true |
|           |                   | 'Chris' !== 'Bob' // true |
|           |                   | 5 !== 2 + 3 // false |
|           |                   | 2 !== '2' // true; numero vs stringa |
| <         | Minore di         | 6 < 10 // true   |
|           |                   | 20 < 10 // false |
| >         | Maggiore di       | 6 > 10 // false  |
|           |                   | 20 > 10 // true  |

**Stringhe di testo**

Le stringhe vengono utilizzate per rappresentare il testo. Abbiamo già visto una variabile di tipo stringa: nel codice seguente, "Sono un segnaposto" è una stringa:

```javascript
function checkGuess() {
  alert("Sono un segnaposto");
}
```

Puoi dichiarare stringhe utilizzando virgolette doppie (") o virgolette singole ('), ma devi utilizzare la stessa forma per l'inizio e la fine di una singola dichiarazione di stringa: non puoi scrivere "Sono un segnaposto'.

Puoi anche dichiarare stringhe utilizzando gli apici inversi (`). Le stringhe dichiarate in questo modo vengono chiamate "template letterali" e hanno alcune proprietà speciali. In particolare, puoi incorporare altre variabili o addirittura espressioni al loro interno:

```javascript
const nome = "Mahalia";
const saluto = `

Ciao ${nome}`;
```

Questo ti fornisce un meccanismo per unire stringhe insieme.

**Condizioni**

Tornando alla nostra funzione `checkGuess()`, è sicuro dire che non vogliamo solo far apparire un messaggio segnaposto. Vogliamo verificare se il tentativo di un giocatore è corretto o meno e rispondere in modo appropriato.

A questo punto, sostituisci la tua attuale funzione `checkGuess()` con questa versione:

```javascript
function checkGuess() {
  const userGuess = Number(guessField.value);
  if (guessCount === 1) {
    guesses.textContent = "Tentativi precedenti:";
  }
  guesses.textContent = `${guesses.textContent} ${userGuess}`;

  if (userGuess === randomNumber) {
    lastResult.textContent = "Congratulazioni! Hai indovinato!";
    lastResult.style.backgroundColor = "green";
    lowOrHi.textContent = "";
    setGameOver();
  } else if (guessCount === 10) {
    lastResult.textContent = "!!!GAME OVER!!!";
    lowOrHi.textContent = "";
    setGameOver();
  } else {
    lastResult.textContent = "Sbagliato!";
    lastResult.style.backgroundColor = "red";
    if (userGuess < randomNumber) {
      lowOrHi.textContent = "L'ultimo tentativo era troppo basso!";
    } else if (userGuess > randomNumber) {
      lowOrHi.textContent = "L'ultimo tentativo era troppo alto!";
    }
  }

  guessCount++;
  guessField.value = "";
  guessField.focus();
}
```

Questa è parecchia quantità di codice — wow! Passiamo ora attraverso ogni sezione e spieghiamo cosa fa.

La prima riga dichiara una variabile chiamata `userGuess` e ne imposta il valore sull'attuale valore inserito nel campo di testo. Eseguiamo anche questo valore attraverso il costruttore `Number()` incorporato, solo per assicurarci che il valore sia sicuramente un numero. Dal momento che non cambiamo questa variabile, la dichiariamo con `const`.
Successivamente, incontriamo il nostro primo blocco di codice condizionale. Un blocco di codice condizionale ti consente di eseguire il codice selettivamente, a seconda che una determinata condizione sia vera o meno. Assomiglia un po' a una funzione, ma non lo è. La forma più semplice di blocco condizionale inizia con la parola chiave `if`, poi alcune parentesi tonde e alcune parentesi graffe. All'interno delle parentesi tonde includiamo un test. Se il test restituisce vero, eseguiamo il codice all'interno delle parentesi graffe. Se non lo fa, non lo facciamo e passiamo al pezzo di codice successivo. In questo caso, il test verifica se la variabile `guessCount` è uguale a 1 (cioè se è il primo turno del giocatore o no):

```javascript
guessCount === 1;
```

Se lo è, facciamo sì che il contenuto di "guesses" sia uguale a "Tentativi precedenti:". Se non lo è, non lo facciamo.
Successivamente, utilizziamo un "template literal" per aggiungere il valore corrente di `userGuess` alla fine del paragrafo "guesses", con uno spazio vuoto in mezzo.
Il blocco successivo effettua alcune verifiche:
- Il primo `if () { }` verifica se il tentativo dell'utente è uguale al `randomNumber` impostato all'inizio del nostro JavaScript. Se è così, il giocatore ha indovinato correttamente e il gioco è vinto, quindi mostriamo al giocatore un messaggio di congratulazioni con un bel colore verde, cancelliamo il contenuto della casella delle informazioni sul tentativo basso/alto e facciamo girare una funzione chiamata `setGameOver()`, di cui parleremo dopo.
- Ora abbiamo concatenato un altro test alla fine dell'ultimo test utilizzando una struttura `else if () { }`. Questo verifica se il turno attuale è l'ultimo tentativo dell'utente. Se è così, il programma fa la stessa cosa del blocco precedente, ma con un messaggio di game over invece di un messaggio di congratulazioni.
- L'ultimo blocco concatenato alla fine di questo codice (`else { }`) contiene il codice che viene eseguito solo se nessuno degli altri due test restituisce vero (cioè il giocatore non ha indovinato correttamente, ma ha ancora altri tentativi). In questo caso diciamo loro che hanno sbagliato, quindi effettuiamo un altro test condizionale per verificare se il tentativo è stato più alto o più basso della risposta, mostrando un ulteriore messaggio adeguato per dirgli se il tentativo è stato alto o basso.
Le ultime tre righe nella funzione (righe 26-28 sopra) ci preparano per il successivo tentativo da sottoporre. Aggiungiamo 1 alla variabile `guessCount` in modo che il giocatore esaurisca il suo turno (`++` è un'operazione di incremento, incrementa di 1), svuotiamo il valore del campo di testo del modulo e lo mettiamo nuovamente a fuoco, pronto per l'inserimento del prossimo tentativo.

**Eventi**

A questo punto, abbiamo una funzione `checkGuess()` ben implementata, ma non farà nulla perché non l'abbiamo ancora chiamata. Idealmente, vogliamo chiamarla quando viene premuto il pulsante "Invia tentativo" e per farlo dobbiamo usare un evento. Gli eventi sono azioni che avvengono nel browser, ad esempio il clic su un pulsante, il caricamento di una pagina, la riproduzione di un video, ecc. In risposta a queste azioni, possiamo eseguire blocchi di codice. Gli eventi vengono osservati da "ascoltatori di eventi" che richiamano "gestori di eventi", che sono appunto blocchi di codice che vengono eseguiti in risposta all'avvenimento di un evento.

Aggiungi la seguente riga sotto la tua funzione `checkGuess()`:

```javascript
guessSubmit.addEventListener("click", checkGuess);
```

Qui stiamo aggiungendo un "listener" di evento al pulsante `guessSubmit`. Questo è un metodo che richiede due valori in input (chiamati argomenti): il tipo di evento che stiamo ascoltando (in questo caso "click") come stringa e il codice che vogliamo eseguire

 quando si verifica l'evento (in questo caso la funzione `checkGuess()`). Nota che non è necessario specificare le parentesi quando lo scriviamo all'interno di `addEventListener()`.

Prova a salvare e aggiornare il tuo codice ora, e il tuo esempio dovrebbe funzionare, almeno fino a un certo punto. L'unico problema ora è che se indovini la risposta corretta o termini i tentativi, il gioco si romperà perché non abbiamo ancora definito la funzione `setGameOver()` che dovrebbe essere eseguita una volta finito il gioco. Aggiungiamo ora il nostro codice mancante e completiamo la funzionalità dell'esempio.

**Completare la funzionalità del gioco**

Aggiungiamo quella funzione `setGameOver()` alla fine del nostro codice e poi la analizziamo. Aggiungi questo ora, sotto il resto del tuo JavaScript:

```javascript
function setGameOver() {
  guessField.disabled = true;
  guessSubmit.disabled = true;
  resetButton = document.createElement("button");
  resetButton.textContent = "Inizia nuovo gioco";
  document.body.append(resetButton);
  resetButton.addEventListener("click", resetGame);
}
```

Le prime due righe disabilitano l'input del campo di testo del modulo e il pulsante impostando le loro proprietà "disabled" su "true". Questo è necessario, perché se non lo facessimo, l'utente potrebbe inviare altri tentativi dopo che il gioco è finito, cosa che farebbe impazzire le cose.
Le tre righe successive generano un nuovo elemento `<button>`, ne impostano l'etichetta testuale su "Inizia nuovo gioco" e lo aggiungono alla parte inferiore del nostro HTML esistente.
L'ultima riga imposta un "listener" di evento sul nostro nuovo pulsante in modo che quando viene premuto, venga eseguita una funzione chiamata `resetGame`.
Ora dobbiamo definire anche questa funzione! Aggiungi il seguente codice, nuovamente alla fine del tuo JavaScript:

```javascript
function resetGame() {
  guessCount = 1;

  const resetParas = document.querySelectorAll(".resultParas p");
  for (const resetPara of resetParas) {
    resetPara.textContent = "";
  }

  resetButton.parentNode.removeChild(resetButton);

  guessField.disabled = false;
  guessSubmit.disabled = false;
  guessField.value = "";
  guessField.focus();

  lastResult.style.backgroundColor = "white";

  randomNumber = Math.floor(Math.random() * 100) + 1;
}
```

Questo blocco di codice abbastanza lungo reimposta completamente tutto com'era all'inizio del gioco, in modo che il giocatore possa fare un altro tentativo. Esso:
- Riporta `guessCount` a 1.
- Svuota tutto il testo dei paragrafi informativi. Selezioniamo tutti i paragrafi all'interno di `<div class="resultParas">` utilizzando il metodo `querySelectorAll()`, quindi iteriamo su ciascuno di essi, impostando il loro `textContent` su '' (una stringa vuota).
- Rimuove il pulsante di reset dal nostro codice.
- Abilita gli elementi del modulo, svuota e mette a fuoco il campo di testo, pronto per un nuovo tentativo.
- Rimuove il colore di sfondo dal paragrafo `lastResult`.
- Genera un nuovo numero casuale in modo che non si stia indovinando lo stesso numero di nuovo!

A questo punto, dovresti avere un gioco completamente funzionante (anche se semplice) — congratulazioni!

L'unica cosa che ci rimane da fare in questo articolo è parlare di alcune altre importanti caratteristiche del codice che hai già visto, anche se potresti non avertene ancora reso conto.

**Cicli**

Una parte del codice sopra che dobbiamo esaminare più in dettaglio è il ciclo `for...of`. I cicli sono un concetto molto importante nella programmazione, che ti consente di eseguire un pezzo di codice più e più volte, fino a quando una determinata condizione viene soddisfatta.

Per iniziare, vai di nuovo alla console JavaScript degli strumenti per sviluppatori del tuo browser e inserisci quanto segue:

```javascript
const frutta = ["mele", "banane", "ciliegie"];
for (const frutto of frutta) {
  console.log(frutto);
}
```

Cosa è successo? Le stringhe 'mele', 'banane', 'ciliegie' sono state stampate nella tua console.

Questo è grazie al ciclo. La riga `const frutta = ['mele', 'banane', 'ciliegie'];` crea un array. Affronteremo una guida completa sugli array più avanti in questo modulo, ma per ora: un array è una raccolta di elementi (in questo caso stringhe).

Un ciclo `for...of` ti offre un modo per ottenere ciascun elemento nell'array ed eseguire del codice JavaScript su di esso. La riga `for (const frutto of frutta)` dice:

- Prendi il primo elemento in `frutta`.
- Imposta la variabile `frutto` su quell'elemento, quindi esegui il codice tra le parentesi `{}`.
- Prendi l'elemento successivo in `frutta` e ripeti 2, fino a raggiungere la fine di `frutta`.

In questo caso, il codice all'interno delle parentesi `{}` sta scrivendo `frutto` nella console.

Ora vediamo il ciclo nel nostro gioco di indovinare i numeri — quanto segue si trova all'interno della funzione `resetGame()`:

```javascript
const resetParas = document.querySelectorAll(".resultParas p");
for (const resetPara of resetParas) {
  resetPara.textContent = "";
}
```

Questo codice crea una variabile contenente un elenco di tutti i paragrafi all'interno di `<div class="resultParas">` utilizzando il metodo `querySelectorAll()`, poi itera su ciascuno di essi, rimuovendo il contenuto del testo di ciascuno.

Nota che anche se `resetPara` è una costante, possiamo comunque cambiare le sue proprietà interne come `textContent`.

Continuazione:

**Una piccola discussione sugli oggetti**

Aggiungiamo un'ulteriore piccola miglioria prima di affrontare questa discussione. Aggiungi la seguente riga appena sotto la riga `let resetButton;` vicino all'inizio del tuo JavaScript, quindi salva il tuo file:

```javascript
guessField.focus();
```

Questa riga utilizza il metodo `focus()` per mettere automaticamente il cursore di testo nel campo di testo `<input>` non appena la pagina viene caricata, consentendo all'utente di iniziare a digitare il suo primo tentativo immediatamente, senza dover prima fare clic sul campo del modulo. È solo un piccolo aggiunta, ma migliora l'usabilità, dando all'utente un buon suggerimento visivo su cosa deve fare per giocare al gioco.

Analizziamo un po' più nel dettaglio cosa sta succedendo qui. In JavaScript, la maggior parte degli elementi che manipolerai nel tuo codice sono oggetti. Un oggetto è una raccolta di funzionalità correlate memorizzate in un unico gruppo. Puoi creare i tuoi oggetti, ma questo è abbastanza avanzato e non lo affronteremo fino a molto più avanti nel corso. Per ora, discuteremo brevemente degli oggetti incorporati che il tuo browser contiene, che ti consentono di fare molte cose utili.

In questo caso specifico, abbiamo prima creato una costante `guessField` che memorizza un riferimento al campo di modulo di input di testo nel nostro HTML — la riga seguente si trova tra le nostre dichiarazioni all'inizio del codice:

```javascript
const guessField = document.querySelector(".guessField");
```

Per ottenere questo riferimento, abbiamo utilizzato il metodo `querySelector()` dell'oggetto `document`. `querySelector()` prende una informazione — un selettore CSS che seleziona l'elemento di cui vuoi un riferimento.

Poiché `guessField` contiene ora un riferimento a un elemento `<input>`, ora ha accesso a una serie di proprietà (fondamentalmente variabili memorizzate all'interno degli oggetti, alcune delle quali non possono avere i loro valori modificati) e metodi (fondamentalmente funzioni memorizzate all'interno degli oggetti). Un metodo disponibile per gli elementi di input è `focus()`, quindi possiamo ora utilizzare questa riga per mettere a fuoco l'input di testo:

```javascript
guessField.focus();
```

Le variabili che non contengono riferimenti a elementi di modulo non avranno il metodo `focus()` disponibile. Ad esempio, la costante `guesses` contiene un riferimento a un elemento `<p>`, e la variabile `guessCount` contiene un numero.

**Giocare con gli oggetti del browser**

Giocando un po' con gli oggetti del browser.

1. Per prima cosa, apri il tuo programma in un browser.
2. Successivamente, apri gli strumenti per sviluppatori del tuo browser e assicurati che la scheda della console JavaScript sia aperta.
3. Digita `guessField` nella console e la console ti mostrerà che la variabile contiene un elemento `<input>`. Noterai anche che la console completa automaticamente i nomi degli oggetti che esistono all'interno dell'ambiente di esecuzione, inclusa le tue variabili!
4. Digita ora quanto segue:
```javascript
guessField.value = 2;
```
La proprietà `value` rappresenta il valore attuale inserito nel campo di testo. Vedrai che inserendo questo comando, abbiamo cambiato il testo nel campo di testo!
5. Prova ora a digitare `guesses` nella console e premi invio. La console ti mostra che la variabile contiene un elemento `<p>`.
6. Prova ora a inserire la seguente riga:
```javascript
guesses.value;
```
Il browser restituirà `undefined`, perché i paragrafi non hanno la proprietà `value`.
7. Per cambiare il testo all'interno di un paragrafo, hai bisogno invece della proprietà `textContent`. Prova questo:
```javascript
guesses.textContent = "Dove si trova il mio paragrafo?";
```
8. Ora per alcune cose divertenti. Prova a inserire le seguenti righe, una dopo l'altra:
```javascript
guesses.style.backgroundColor = "yellow";
guesses.style.fontSize = "200%";
guesses.style.padding = "10px";
guesses.style.boxShadow = "3px 3px 6px black";
```
Ogni elemento sulla pagina ha una proprietà `style`, che a sua volta contiene un oggetto le cui proprietà contengono tutti gli stili CSS inline applicati a quell'elemento. Questo ci consente di impostare dinamicamente nuovi stili CSS sugli elementi utilizzando JavaScript.

**Finito per ora...**

Quindi è tutto per la costruzione dell'esempio. Sei arrivato alla fine — ben fatto! Prova il tuo codice finale, o gioca con la nostra versione finita qui. Se non riesci a far funzionare l'esempio, confrontalo con il codice sorgente.
