# 2. Oggetti in Javascript

Gli oggetti sono il cuore della programmazione in Javascript. Possiamo pensare a un oggetto come a una sorta di contenitore che raccoglie informazioni e funzionalità correlate. Immagina di avere una scatola etichettata "gatto" - all'interno di questa scatola, potresti trovare tutte le cose che descrivono e fanno parte di un gatto.

## 2.1 Creazione di oggetti letterali

In Javascript, il modo più semplice per creare un oggetto è usando la notazione letterale. È come se stessimo scrivendo una ricetta rapida per il nostro oggetto. Vediamo un esempio:

```javascript
let mioGatto = {
    nome: "Whiskers",
    età: 3,
    colore: "tigrato"
};
```

In questo esempio, abbiamo creato un oggetto chiamato `mioGatto`. All'interno delle parentesi graffe, abbiamo definito alcune proprietà del gatto: il suo nome, la sua età e il suo colore. È come se stessimo compilando una scheda d'identità per il nostro amico felino!

## 2.2 Proprietà e metodi

Le proprietà sono le caratteristiche del nostro oggetto, come abbiamo visto nell'esempio precedente. Ma gli oggetti possono fare anche delle azioni, e queste azioni sono rappresentate dai metodi. Un metodo è semplicemente una funzione associata all'oggetto.

Aggiungiamo un metodo al nostro gatto:

```javascript
let mioGatto = {
    nome: "Whiskers",
    età: 3,
    colore: "tigrato",
    miagola: function() {
        console.log("Miao miao!");
    }
};
```

Ora il nostro gatto può miagolare! Abbiamo aggiunto un metodo chiamato `miagola` che, quando viene chiamato, farà "parlare" il nostro gatto.

## 2.3 Accesso alle proprietà e ai metodi

Per accedere alle proprietà o ai metodi di un oggetto, usiamo la notazione con il punto. È come se stessimo chiedendo all'oggetto di darci un'informazione o di fare qualcosa. Vediamo come funziona:

```javascript
console.log(mioGatto.nome);  // Stamperà: Whiskers
console.log(mioGatto.età);   // Stamperà: 3

mioGatto.miagola();  // Stamperà: Miao miao!
```

Possiamo anche modificare le proprietà di un oggetto in questo modo:

```javascript
mioGatto.età = 4;  // Il gatto ha festeggiato il compleanno!
console.log(mioGatto.età);  // Stamperà: 4
```

C'è anche un altro modo per accedere alle proprietà di un oggetto, usando le parentesi quadre. Questo metodo è particolarmente utile quando il nome della proprietà è memorizzato in una variabile o quando il nome contiene spazi o caratteri speciali:

```javascript
let proprietà = "colore";
console.log(mioGatto[proprietà]);  // Stamperà: tigrato

mioGatto["data di nascita"] = "1 Gennaio 2020";
console.log(mioGatto["data di nascita"]);  // Stamperà: 1 Gennaio 2020
```

Gli oggetti in Javascript sono molto flessibili e potenti. Possono contenere diversi tipi di dati, inclusi altri oggetti, array e funzioni. Questa flessibilità li rende uno strumento fondamentale per organizzare e strutturare il nostro codice in modo logico e intuitivo.

Nei prossimi capitoli, vedremo come possiamo usare le classi per creare "fabbriche" di oggetti, rendendo il nostro codice ancora più organizzato e riutilizzabile!
