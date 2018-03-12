## Equalità

Una cosa a cui fare attenzione in JavaScript è la differenza tra `==` e `===`. Siccome JavaScript tenta di
essere resiliente contro gli errori di programmazione `==` tenta di far combacciare i tipi tra due variabili
e.g. converte una stringa ad un numero in modo che tu possa comparare un numero come mostrato sotto:

```js
console.log(5 == "5"); // true   , TS Errore
console.log(5 === "5"); // false , TS Errore
```

Ad ogni modo le scelte che JavaScript fa non sempre sono ideali. Nell' esempio sotto il primo elemento è false
perchè `""` e `"0`" sono entrambe stringhe e chiaramente non sono uguali. Però nel secondo caso entrambi `0` e la stringa
vuota (`""`) sono false (i.e. valutate come `false`) e sono quindi uguali con `==`. Entrambe le dichiarazioni
sono false quando usi `===`

```js
console.log("" == "0"); // false
console.log(0 == ""); // true

console.log("" === "0"); // false
console.log(0 === ""); // false
```

> Nota che `string == number` e `string === number` producono entrambe errori di compilazione in TypeScript, quindi normalmente non devi preoccupartene.

Similmente a `==` vs. `===`, c'è `!=` vs. `!==`


Quindi Consiglio Pro: Usa sempre `===` e `!==` eccetto per i controlli su null, che copriremo più avanti.

## Equalità strutturale
Se vuoi comparare due oggetti per equalità strutturale `==`/`===` ***non*** sono sufficienti. e.g.

```js
console.log({a:123} == {a:123}); // False
console.log({a:123} === {a:123}); // False
```
Per operazioni del genere puoi utilizzare il package nmp [deep-equal](https://www.npmjs.com/package/deep-equal) e.g. 

```js
import * as deepEqual from "deep-equal";

console.log(deepEqual({a:123},{a:123})); // True
```
