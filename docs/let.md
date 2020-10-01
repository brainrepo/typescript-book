### let

`var` Le variabili in JavaScript sono *function scoped*. Questo è diverso da molti altri linguaggi (C# / Java ecc.) dove le variabili sono *block scoped*. Se si porta una mentalità *block scoped* in JavaScript, ci si aspetterebbe che quanto segue stampi `123`, invece stamperà `456`:

```ts
var foo = 123;
if (true) {
    var foo = 456;
}
console.log(foo); // 456
```
Questo perché `{` non crea un nuovo *variable scope*. La variabile `foo` è la stessa all'interno del *blocco* if come lo è all'esterno del blocco if. Questa è una fonte comune di errori nella programmazione JavaScript. Per questo motivo TypeScript (ed ES6) introduce la parola chiave `let` per consentire di definire variabili con vero *block scope*. Questo se si usa `let` invece di `var` si ottiene un vero elemento unico disconnesso da ciò che si potrebbe aver definito al di fuori dello scope. Lo stesso esempio è dimostrato con `let`:

```ts
let foo = 123;
if (true) {
    let foo = 456;
}
console.log(foo); // 123
```

Un altro posto in cui `let` ti salverebbe dagli errori sono i cicli.

```ts
var index = 0;
var array = [1, 2, 3];
for (let index = 0; index < array.length; index++) {
    console.log(array[index]);
}
console.log(index); // 0
```
In tutta sincerità riteniamo che sia meglio usare `let` ogni volta che è possibile, perché porta a minori sorprese per gli sviluppatori multilingue nuovi ed esistenti.

#### Funzioni che creano un nuovo scope
Visto che ne abbiamo parlato, vorremmo dimostrare che le funzioni creano un nuovo variable scope in JavaScript. Considera quanto segue:
```ts
var foo = 123;
function test() {
    var foo = 456;
}
test();
console.log(foo); // 123
```
Questo si comporta come ci si aspetterebbe. Senza questo sarebbe molto difficile scrivere codice in JavaScript.

#### JS generato
Il JS generato da TypeScript è una semplice ridenominazione della variabile `let` se un nome simile esiste già nello scope circostante. Ad esempio, viene generato quanto segue, così com'è con una semplice sostituzione di `var` con `let`:

```ts
if (true) {
    let foo = 123;
}

// becomes //

if (true) {
    var foo = 123;
}
```
Tuttavia, se il nome della variabile è già preso dallo scope circostante, allora viene generato un nuovo nome di variabile come mostrato (notare `_foo`):

```ts
var foo = '123';
if (true) {
    let foo = 123;
}

// becomes //

var foo = '123';
if (true) {
    var _foo = 123; // Renamed
}
```

#### Switch
You can wrap your `case` bodies in `{}` to reuse variable names reliably in different `case` statement as shown below: 

```ts
switch (name) {
    case 'x': {
        let x = 5;
        // ...
        break;
    }
    case 'y': {
        let x = 10;
        // ...
        break;
    }
}
```

#### let in closures
A common programming interview question for a JavaScript developer is what is the log of this simple file:

```ts
var funcs = [];
// create a bunch of functions
for (var i = 0; i < 3; i++) {
    funcs.push(function() {
        console.log(i);
    })
}
// call them
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```
One would have expected it to be `0,1,2`. Surprisingly it is going to be `3` for all three functions. Reason is that all three functions are using the variable `i` from the outer scope and at the time we execute them (in the second loop) the value of `i` will be `3` (that's the termination condition for the first loop).

A fix would be to create a new variable in each loop specific to that loop iteration. As we've learnt before we can create a new variable scope by creating a new function and immediately executing it (i.e. the IIFE pattern from classes `(function() { /* body */ })();`) as shown below:

```ts
var funcs = [];
// create a bunch of functions
for (var i = 0; i < 3; i++) {
    (function() {
        var local = i;
        funcs.push(function() {
            console.log(local);
        })
    })();
}
// call them
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```
Here the functions close over (hence called a `closure`) the *local* variable (conveniently named `local`) and use that instead of the loop variable `i`.

> Note that closures come with a performance impact (they need to store the surrounding state).

The ES6 `let` keyword in a loop would have the same behavior as the previous example:

```ts
var funcs = [];
// create a bunch of functions
for (let i = 0; i < 3; i++) { // Note the use of let
    funcs.push(function() {
        console.log(i);
    })
}
// call them
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```

Using a `let` instead of `var` creates a variable `i` unique to each loop iteration.

#### Summary
`let` is extremely useful to have for the vast majority of code. It can greatly enhance your code readability and decrease the chance of a programming error.



[](https://github.com/olov/defs/blob/master/loop-closures.md)
