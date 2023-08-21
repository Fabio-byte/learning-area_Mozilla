**Documento: metodo querySelector()**

Il metodo `querySelector()` del Document restituisce il primo elemento all'interno del documento che corrisponde al selettore specificato o al gruppo di selettori. Se non vengono trovate corrispondenze, verrà restituito `null`.

Nota: Il matching viene effettuato utilizzando una traversa in pre-ordine in profondità dei nodi del documento a partire dal primo elemento nel markup del documento e iterando attraverso i nodi sequenziali in base all'ordine del numero dei nodi figli.

Sintassi
```javascript
querySelector(selettori)
```

Parametri
- `selettori`: Una stringa contenente uno o più selettori da corrispondere. Questa stringa deve essere una stringa di selettore CSS valida; se non lo è, verrà generata un'eccezione `SyntaxError`. Per ulteriori dettagli sui selettori e su come gestirli, consulta la sezione "Localizzazione degli elementi DOM utilizzando i selettori".

Nota: I caratteri che non fanno parte della sintassi CSS standard devono essere scappati utilizzando il carattere backslash. Poiché JavaScript utilizza anche l'escape con il backslash, sii particolarmente attento quando scrivi stringhe letterali utilizzando questi caratteri. Per ulteriori informazioni, consulta la sezione "Escape dei caratteri speciali".

Valore di ritorno
Un oggetto Element che rappresenta il primo elemento nel documento che corrisponde all'insieme specificato di selettori CSS, o verrà restituito `null` se non ci sono corrispondenze.

Se hai bisogno di una lista di tutti gli elementi che corrispondono ai selettori specificati, dovresti utilizzare invece `querySelectorAll()`.

Eccezioni
- `SyntaxError`
- `DOMException`
Viene generata se la sintassi dei selettori specificati non è valida.

Note sull'uso
- Se il selettore specificato corrisponde a un ID utilizzato in modo errato più di una volta nel documento, verrà restituito il primo elemento con quell'ID.

I pseudo-elementi CSS non restituiranno mai elementi, come specificato nell'API dei Selettori.

Escape dei caratteri speciali
Per corrispondere a un ID o a selettori che non seguono la sintassi CSS standard (utilizzando in modo inappropriato due punti o spazi, ad esempio), devi scappare il carattere con un backslash (`\`). Poiché il backslash è anche un carattere di escape in JavaScript, se stai inserendo una stringa letterale, devi scapparlo due volte (una volta per la stringa JavaScript e un'altra volta per `querySelector()`):

```html
<div id="foo\bar"></div>
<div id="foo:bar"></div>

<script>
  console.log("#foo\bar"); // "#fooar" (\b è il carattere di controllo backspace)
  document.querySelector("#foo\bar"); // Non corrisponde a nulla

  console.log("#foo\\bar"); // "#foo\bar"
  console.log("#foo\\\\bar"); // "#foo\\bar"
  document.querySelector("#foo\\\\bar"); // Corrisponde al primo div

  document.querySelector("#foo:bar"); // Non corrisponde a nulla
  document.querySelector("#foo\\:bar"); // Corrisponde al secondo div
</script>
```

Esempi
Trovare il primo elemento corrispondente a una classe
In questo esempio, viene restituito il primo elemento nel documento con la classe "myclass":

```javascript
const el = document.querySelector(".myclass");
```

Selettori complessi
I selettori possono anche essere molto potenti, come dimostrato nel seguente esempio. Qui viene restituito il primo elemento `<input>` con il nome "login" (`<input name="login"/>`) situato all'interno di un `<div>` la cui classe è "user-panel main" (`<div class="user-panel main">`) nel documento:

```javascript
const el = document.querySelector("div.user-panel.main input[name='login']");
```

Negazione
Poiché tutte le stringhe di selettori CSS sono valide, puoi anche negare i selettori:

```javascript
const el = document.querySelector(
  "div.user-panel:not(.main) input[name='login']",
);
```

Questo selezionerà un input con un div genitore con la classe user-panel ma non la classe main.

Specifiche
Specificazione
Standard DOM
# ref-for-dom-parentnode-queryselector①
Compatibilità con i browser
Segnala problemi con questi dati di compatibilità su GitHub
desktop	mobile
Chrome
Edge
Firefox
Opera
Safari
Chrome Android
Firefox per Android
Opera Android
Safari su iOS
Samsung Internet
WebView Android
querySelector

1
Mostra la cronologia	
12
Mostra la cronologia	
3.5
Mostra la cronologia	
10
Mostra la cronologia	
3.1
Mostra la cronologia	
18
Mostra la cronologia	
4
Mostra la cronologia	
10.1
Mostra la cronologia	
2
Mostra la cronologia	
1.0
Mostra la cronologia	
4.4
Mostra la cronologia
Legenda
Suggerimento: puoi fare clic/toccare su una cella per ulteriori informazioni.

Supporto completo
Supporto completo
Vedi anche
Localizzazione degli elementi DOM utilizzando i selettori
Element.querySelector()
Document.querySelectorAll()
Element.querySelectorAll()
