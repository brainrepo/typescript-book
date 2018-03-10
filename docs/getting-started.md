* [Iniziamo con TypeScript](#getting-started-with-typescript)
* [Versione di TypeScript](#typescript-version)

# Iniziamo con TypeScript

TypeScript viene compilato in JavaScript. JavaScript è comunque quello che verrà eseguito (sia nel browser sia nel server).
Avrai quindi bisogno delle seguenti cose:

* Un compilatore TypeScript (OSS disponibile su [in source](https://github.com/Microsoft/TypeScript/) o su [NPM](https://www.npmjs.com/package/typescript))
* Un editor TypeScript (puoi usare anche notepad se vuoi però valuta anche [alm 🌹](https://alm-tools.github.io/). Inoltre [TypeScript è supportato comunque da molti IDE]( https://github.com/Microsoft/TypeScript/wiki/TypeScript-Editor-Support))


![alm editor window](https://raw.githubusercontent.com/alm-tools/alm-tools.github.io/master/screens/main.png)


## Versione di TypeScript

Invece di usare una versione *stabile* del compilatore TypeScript presenteremo molte nuove cose che potrebbero non ancora essere associate ad un numero di versione. In genere raccomando di usare la versione nightly perchè **il test compiler segnalerà solo piu bug nel tempo**


La puoi installare da riga di comando con:

```
npm install -g typescript@next
```

Cosi facendo il comando `tsc` sarà aggiornato all' ultima versione. Diversi IDE supportano anche questo:

* `alm` compila sempre con l'ultima versione di TypeScript.
* In vscode, puoi usare questa versione creando il file `.vscode/settings.json` con questo contenuto:

```json
{
  "typescript.tsdk": "./node_modules/typescript/lib"
}
```

## Ottenere il codice
Il Sorgente di questo libro è disponibile nella repository github https://github.com/basarat/typescript-book/tree/master/code
diversi esempi di codice possono essere copiati dentro alm dove potrai giocarci liberamente. Per esempi di codice che richiedono
impostazioni aggiunti (e.g. moduli npm) includeremo il link al codice di esempio prima di presentare il codice. e.g.

`questo/sara/il/link/al/codice.ts`
```ts
// Questo sarà il codice discusso
```

Dopo aver impostato il necessario per lo sviluppo, tuffiamoci nella sintassi di TypeScript.