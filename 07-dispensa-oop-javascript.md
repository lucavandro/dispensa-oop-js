# 7. Polimorfismo

Immaginate di avere un telecomando universale. Con lo stesso pulsante "accendi", potete accendere la TV, la radio o il condizionatore. Ogni dispositivo risponde allo stesso comando, ma in modo diverso. Questo è essenzialmente il concetto di polimorfismo nella programmazione: la capacità di oggetti di classi diverse di rispondere allo stesso messaggio in modi diversi.

## 7.1 Concetto di polimorfismo

Il termine "polimorfismo" deriva dal greco e significa "molte forme". Nella programmazione orientata agli oggetti, il polimorfismo ci permette di utilizzare un'interfaccia comune per tipi (classi) diversi. Questo rende il nostro codice più flessibile e più facile da estendere.

## 7.2 Implementazione del polimorfismo in Javascript

In Javascript, il polimorfismo si manifesta principalmente in due modi: attraverso l'ereditarietà (che abbiamo visto nel capitolo precedente) e attraverso le interfacce (che in Javascript sono più un concetto che una struttura formale del linguaggio).

Vediamo un esempio di polimorfismo basato sull'ereditarietà, espandendo il nostro esempio di animali:

```javascript
class Animale {
    constructor(nome) {
        this.nome = nome;
    }

    faiVerso() {
        console.log("L'animale fa un verso");
    }
}

class Gatto extends Animale {
    faiVerso() {
        console.log(`${this.nome} fa miao!`);
    }
}

class Cane extends Animale {
    faiVerso() {
        console.log(`${this.nome} fa bau!`);
    }
}

class Mucca extends Animale {
    faiVerso() {
        console.log(`${this.nome} fa muu!`);
    }
}

// Funzione che utilizza il polimorfismo
function faiParlareAnimale(animale) {
    animale.faiVerso();
}

let luna = new Gatto("Luna");
let fido = new Cane("Fido");
let bella = new Mucca("Bella");

faiParlareAnimale(luna);  // Luna fa miao!
faiParlareAnimale(fido);  // Fido fa bau!
faiParlareAnimale(bella); // Bella fa muu!
```

In questo esempio, abbiamo una classe base `Animale` con un metodo `faiVerso()`. Ogni classe derivata (`Gatto`, `Cane`, `Mucca`) sovrascrive questo metodo con la propria implementazione specifica.

La funzione `faiParlareAnimale()` è un esempio perfetto di polimorfismo in azione. Questa funzione accetta un oggetto di tipo `Animale` (o qualsiasi classe che estende `Animale`) e chiama il metodo `faiVerso()`. Non sa e non ha bisogno di sapere con quale tipo specifico di animale sta lavorando. Semplicemente chiama il metodo `faiVerso()`, e l'oggetto risponde nel modo appropriato per la sua classe.

Questo è potente perché ci permette di aggiungere nuovi tipi di animali senza dover modificare la funzione `faiParlareAnimale()`. Se domani volessimo aggiungere una classe `Pecora`, dovremmo solo assicurarci che abbia un metodo `faiVerso()`, e funzionerebbe immediatamente con il nostro codice esistente.

Ecco un altro esempio che mostra come il polimorfismo possa rendere il nostro codice più flessibile:

```javascript
class Forma {
    area() {
        return 0;
    }
}

class Rettangolo extends Forma {
    constructor(larghezza, altezza) {
        super();
        this.larghezza = larghezza;
        this.altezza = altezza;
    }

    area() {
        return this.larghezza * this.altezza;
    }
}

class Cerchio extends Forma {
    constructor(raggio) {
        super();
        this.raggio = raggio;
    }

    area() {
        return Math.PI * this.raggio * this.raggio;
    }
}

function calcolaAreaTotale(forme) {
    return forme.reduce((totale, forma) => totale + forma.area(), 0);
}

let rettangolo = new Rettangolo(5, 3);
let cerchio = new Cerchio(2);

console.log(calcolaAreaTotale([rettangolo, cerchio]));
// Output: 27.566370614359172 (15 + 12.566370614359172)
```

In questo esempio, la funzione `calcolaAreaTotale()` può lavorare con qualsiasi array di oggetti che hanno un metodo `area()`, indipendentemente dalla loro classe specifica. Questo è il polimorfismo in azione.

Il polimorfismo ci permette di scrivere codice più generico e riutilizzabile. Invece di scrivere funzioni separate per ogni tipo di oggetto, possiamo scrivere una singola funzione che lavora con un'interfaccia comune. Questo rende il nostro codice più flessibile, più facile da mantenere e più facile da estendere.

Nel prossimo capitolo, esploreremo il concetto di composizione, un'alternativa all'ereditarietà che ci offre un altro modo potente per strutturare le nostre classi e oggetti!
