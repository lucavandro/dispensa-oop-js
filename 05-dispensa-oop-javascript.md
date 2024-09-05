# 5. Information Hiding

Immaginate di essere in un ristorante. Ordinate il vostro piatto preferito e, dopo un po', il cameriere ve lo porta, perfettamente preparato. Non avete bisogno di sapere esattamente come lo chef l'ha cucinato, quali utensili ha usato o come è organizzata la cucina. Tutto ciò che vi interessa è il risultato finale: un piatto delizioso. Questo è essenzialmente il concetto di information hiding nella programmazione.

## 5.1 Concetto di information hiding

L'information hiding, o "nascondere le informazioni", è un principio della programmazione orientata agli oggetti strettamente legato all'incapsulamento. Mentre l'incapsulamento si concentra sul raggruppamento di dati e metodi correlati, l'information hiding si concentra sul nascondere i dettagli interni di implementazione di un oggetto e fornire solo un'interfaccia pubblica per interagire con esso.

L'idea è di mostrare solo ciò che è necessario e nascondere tutto il resto. Questo rende il nostro codice più facile da usare, più facile da mantenere e più resistente ai cambiamenti.

## 5.2 Implementazione in Javascript

In Javascript, possiamo implementare l'information hiding usando una combinazione di proprietà private, metodi privati e un'interfaccia pubblica ben definita. Vediamo come potremmo applicare questo concetto alla nostra classe Gatto:

```javascript
class Gatto {
    #nome;
    #età;
    #livelloFame;

    constructor(nome, età) {
        this.#nome = nome;
        this.#età = età;
        this.#livelloFame = 5; // Su una scala da 0 a 10
    }

    get nome() {
        return this.#nome;
    }

    get età() {
        return this.#età;
    }

    #aumentaFame() {
        if (this.#livelloFame < 10) {
            this.#livelloFame++;
        }
    }

    #diminuisciFame() {
        if (this.#livelloFame > 0) {
            this.#livelloFame--;
        }
    }

    miagola() {
        console.log(`${this.#nome} dice: Miao!`);
        this.#aumentaFame();
    }

    mangia() {
        console.log(`${this.#nome} sta mangiando.`);
        this.#diminuisciFame();
    }

    statoFame() {
        let stato;
        if (this.#livelloFame <= 3) stato = "affamato";
        else if (this.#livelloFame <= 7) stato = "soddisfatto";
        else stato = "molto sazio";
        
        console.log(`${this.#nome} è ${stato}.`);
    }
}

let luna = new Gatto("Luna", 2);
luna.miagola();  // Luna dice: Miao!
luna.mangia();   // Luna sta mangiando.
luna.statoFame();  // Luna è soddisfatta.
```

In questo esempio, abbiamo nascosto molti dettagli interni della nostra classe Gatto:

1. Le proprietà #nome, #età e #livelloFame sono private. Non possiamo accedervi direttamente dall'esterno della classe.

2. I metodi #aumentaFame() e #diminuisciFame() sono privati. Sono usati internamente dalla classe, ma non sono accessibili dall'esterno.

3. Forniamo un'interfaccia pubblica semplice con i metodi miagola(), mangia() e statoFame(). Questi metodi nascondono la complessità interna della gestione del livello di fame.

L'utente della classe non ha bisogno di sapere come viene gestito il livello di fame internamente. Tutto ciò che deve sapere è che può far miagolare il gatto, dargli da mangiare e controllare il suo stato di fame. Questo è l'essenza dell'information hiding.

## 5.3 Symbol per proprietà private (pre-ES2022)

Prima dell'introduzione delle proprietà private con #, Javascript utilizzava i Symbol per creare proprietà "semi-private". Anche se non sono completamente privati, i Symbol offrono un modo per creare proprietà uniche che non sono facilmente accessibili dall'esterno. Ecco come potremmo usarli:

```javascript
const nome = Symbol('nome');
const età = Symbol('età');

class Gatto {
    constructor(n, e) {
        this[nome] = n;
        this[età] = e;
    }

    descriviti() {
        console.log(`Sono ${this[nome]} e ho ${this[età]} anni.`);
    }
}

let whiskers = new Gatto("Whiskers", 3);
whiskers.descriviti();  // Sono Whiskers e ho 3 anni.
console.log(whiskers[nome]);  // undefined (non possiamo accedere direttamente al Symbol)
```

Anche se i Symbol non offrono una vera privacy come le proprietà private con #, sono ancora utili in molte situazioni e sono supportati in versioni più vecchie di Javascript.

L'information hiding ci aiuta a creare codice più pulito, più facile da usare e più facile da mantenere. Nascondendo i dettagli interni e fornendo un'interfaccia pubblica ben definita, possiamo creare oggetti che sono più facili da capire e da usare correttamente. Questo ci permette di modificare l'implementazione interna senza influenzare il codice che usa i nostri oggetti, rendendo il nostro software più flessibile e resistente ai cambiamenti.

Nel prossimo capitolo, esploreremo come possiamo usare l'ereditarietà per creare relazioni tra le nostre classi e riutilizzare il codice in modo efficiente!
