# 3. Classi in Javascript

Abbiamo visto come creare oggetti in Javascript, ma cosa succede se vogliamo creare molti oggetti simili? È qui che entrano in gioco le classi. Pensate a una classe come a un progetto o uno stampo per creare oggetti. Se gli oggetti fossero biscotti, la classe sarebbe la forma per i biscotti!

## 3.1 Introduzione alle classi in ES6+

Javascript ha introdotto le classi con ES6 (ECMAScript 2015), rendendo più facile e intuitivo creare oggetti con strutture simili. Le classi in Javascript sono in realtà una "sintassi zuccherata" sopra il sistema di prototipi esistente, ma non preoccupatevi di questo per ora - le classi ci permettono di scrivere codice più pulito e comprensibile.

## 3.2 Dichiarazione di una classe

Dichiariamo una classe per il nostro amico felino:

```javascript
class Gatto {
    constructor(nome, età, colore) {
        this.nome = nome;
        this.età = età;
        this.colore = colore;
    }

    miagola() {
        console.log("Miao miao!");
    }
}
```

In questo esempio, abbiamo creato una classe `Gatto`. La classe ha un metodo speciale chiamato `constructor` che viene chiamato quando creiamo un nuovo gatto. Il costruttore imposta le proprietà iniziali del gatto. Abbiamo anche aggiunto un metodo `miagola`, proprio come avevamo fatto con l'oggetto letterale.

## 3.3 Il costruttore

Il costruttore è come il "momento della nascita" per i nostri oggetti gatto. È una funzione speciale che viene chiamata automaticamente quando creiamo un nuovo gatto. Nel costruttore, usiamo la parola chiave `this` per riferirci al gatto che stiamo creando. 

Quando scriviamo `this.nome = nome`, stiamo dicendo "prendi il nome che mi è stato dato e assegnalo come proprietà di questo nuovo gatto".

## 3.4 Metodi di istanza

I metodi di istanza sono funzioni che ogni gatto creato dalla nostra classe potrà eseguire. Nel nostro esempio, `miagola()` è un metodo di istanza. Ogni gatto che creiamo avrà la sua propria copia di questo metodo.

Ora, vediamo come usare questa classe per creare dei gatti:

```javascript
let whiskers = new Gatto("Whiskers", 3, "tigrato");
let luna = new Gatto("Luna", 2, "bianco");

console.log(whiskers.nome);  // Stamperà: Whiskers
console.log(luna.età);       // Stamperà: 2

whiskers.miagola();  // Stamperà: Miao miao!
luna.miagola();      // Stamperà: Miao miao!
```

In questo esempio, abbiamo creato due gatti diversi usando la nostra classe `Gatto`. Usiamo la parola chiave `new` per dire a Javascript di creare un nuovo oggetto basato sulla nostra classe. Passiamo i valori per nome, età e colore al costruttore.

Possiamo anche aggiungere altri metodi alla nostra classe. Per esempio, potremmo aggiungere un metodo per far invecchiare il nostro gatto:

```javascript
class Gatto {
    // ... (costruttore e metodo miagola come prima)

    compleanno() {
        this.età += 1;
        console.log(`${this.nome} ora ha ${this.età} anni!`);
    }
}

let whiskers = new Gatto("Whiskers", 3, "tigrato");
whiskers.compleanno();  // Stamperà: Whiskers ora ha 4 anni!
```

Le classi ci permettono di organizzare il nostro codice in modo più strutturato e di creare molti oggetti simili in modo efficiente. Sono un pilastro fondamentale della programmazione orientata agli oggetti in Javascript moderno.

Nei prossimi capitoli, vedremo come possiamo usare le classi per implementare concetti più avanzati come l'incapsulamento e l'ereditarietà. Questi concetti ci aiuteranno a creare codice ancora più robusto e flessibile!
