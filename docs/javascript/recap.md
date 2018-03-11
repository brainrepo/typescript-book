# Il tuo JavaScript è TypeScript

Ci sono (e continueranno ad esserci) molti competitori nella *sintassi* dei compilatori *javascript*. TypeScript è differente visto che *il tuo JavaScript è TypeScript*. Ecco un diagramma:

![JavaScript is TypeScript](https://raw.githubusercontent.com/basarat/typescript-book/master/images/venn.png)

Ad ogni modo questo significa che *hai bisogno di imparare JavaScript* (la buona notizia che *hai **solo** bisogno di imparare JavaScript*). TypeScript semplicemente da uno standard con cui puoi fornire *buona documentazione* su JavaScript.

* Dare una nuova sintassi non aiuta a risolvere bug (sto parlando di te, CofeeScript).
* Creare un nuovo linguaggio ti allontana troppo dall' esecuzione e dalla comunità (sto parlando di te, Dart)

TypeScript è semplicemente JavaScript documentato.

## Rendere JavaScript migliore

TypeScript cercherà di proteggerti dalle porzioni di JavaScript che non hanno mai funzionato (cosi non avrai bisogno di ricordarle):

```ts
[] + []; // JavaScript restituirà "" (che non ha molto senso), TypeScript darà errore

//
// altre cose che non hanno senso in JavaScript
// - non dare errore runtime (rendendo il debugging difficile)
// - ma TypeScript darà un errore di compilazione (rendendo il debugging non necessario)
//
{} + []; // JS : 0, TS Errore
[] + {}; // JS : "[object Object]", TS Errore
{} + {}; // JS : NaN o [object Object][object Object] a seconda del browser, TS Errore
"hello" - 1; // JS : NaN, TS Errore

function add(a,b) {
  return
    a + b; // JS : undefined, TS Errore 'unreachable code detected'
}
```

Essenzialmente TypeScript e JavaScript che segnala correzioni. Semplicemente fa un lavoro migliore di altri correttori che non hanno *informazioni sui tipi*.

## Hai ancora bisogno di imparare JavaScript

Detto questo TypeScript è molto pragmatico riguardo il fatto che *stai scrivendo JavaScript* quindi ci sono alcune cose su JavaScript che hai ancora bisogno di sapere per non essere preso alla sprovvista. Discutiamone più avanti.

> Nota: TypeScript è un superset di JavaScript. Semplicemente con documentazione che può essere usata da compilatori / IDE ;)
