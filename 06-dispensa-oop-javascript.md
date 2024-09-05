# 6. Ereditarietà

Immaginate una famiglia. I figli ereditano alcune caratteristiche dai genitori: potrebbero avere gli occhi della mamma o il naso del papà. Allo stesso tempo, hanno le loro caratteristiche uniche. Nell'ambito della programmazione, l'ereditarietà funziona in modo simile. Ci permette di creare nuove classi basate su classi esistenti, ereditando le loro caratteristiche e aggiungendone di nuove.

## 6.1 Concetto di ereditarietà

L'ereditarietà è un principio fondamentale della programmazione orientata agli oggetti che ci permette di definire una nuova classe basata su una classe esistente. La nuova classe (chiamata classe figlia o sottoclasse) eredita proprietà e metodi dalla classe esistente (chiamata classe genitore o superclasse). Questo ci permette di riutilizzare il codice e creare una gerarchia di classi.

## 6.2 Estensione di classi in Javascript

In Javascript, usiamo la parola chiave `extends` per creare una classe che eredita da un'altra. Vediamo come potremmo usare l'ereditarietà con i nostri gatti:

```javascript
class Animale {
    constructor(nome) {
        this.nome = nome;
    }

    mangia() {
        console.log(`${this.nome} sta mangiando.`);
    }

    dorme() {
        console.log(`${this.nome} sta dormendo.`);
    }
}

class Gatto extends Animale {
    constructor(nome, razza) {
        super(nome);  // Chiama il costruttore della classe genitore
        this.razza = razza;
    }

    miagola() {
        console.log(`${this.nome} fa miao!`);
    }
}

let luna = new Gatto("Luna", "Siamese");
luna.mangia();   // Luna sta mangiando.
luna.dorme();    // Luna sta dormendo.
luna.miagola();  // Luna fa miao!
console.log(luna.razza);  // Siamese
```

In questo esempio, abbiamo una classe base `Animale` con alcune proprietà e metodi comuni a tutti gli animali. Poi abbiamo creato una classe `Gatto` che estende `Animale`. La classe `Gatto` eredita tutti i metodi di `Animale` (`mangia` e `dorme`), ma aggiunge anche un suo metodo specifico (`miagola`) e una nuova proprietà (`razza`).

## 6.3 La parola chiave `super`

Avete notato la parola `super` nel costruttore di `Gatto`? Questa è una parola chiave speciale che ci permette di chiamare il costruttore della classe genitore. È come dire "Ehi, genitore! Fai la tua parte prima che io faccia la mia".

Possiamo usare `super` anche per chiamare metodi della classe genitore. Per esempio:

```javascript
class Gatto extends Animale {
    // ... altri metodi ...

    mangia() {
        super.mangia();  // Chiama il metodo mangia di Animale
        console.log(`${this.nome} fa le fusa di contentezza.`);
    }
}

luna.mangia();
// Output:
// Luna sta mangiando.
// Luna fa le fusa di contentezza.
```

In questo caso, abbiamo "esteso" il comportamento del metodo `mangia` aggiungendo un'azione specifica del gatto dopo aver chiamato il metodo della classe genitore.

## 6.4 Overriding di metodi

A volte, potremmo voler cambiare completamente il comportamento di un metodo ereditato. Questo si chiama "overriding" o sovrascrittura. Ecco un esempio:

```javascript
class Pesce extends Animale {
    dorme() {
        console.log(`${this.nome} riposa con gli occhi aperti.`);
    }
}

let nemo = new Pesce("Nemo");
nemo.dorme();  // Nemo riposa con gli occhi aperti.
```

In questo caso, abbiamo completamente sostituito il metodo `dorme` per la classe `Pesce`, perché i pesci dormono in modo diverso dagli altri animali.

L'ereditarietà è un potente strumento che ci permette di organizzare il nostro codice in modo logico e riutilizzabile. Ci consente di creare gerarchie di classi che riflettono le relazioni nel mondo reale, rendendo il nostro codice più intuitivo e facile da gestire.

Tuttavia, è importante usare l'ereditarietà con saggezza. A volte, una gerarchia di classi troppo profonda può rendere il codice difficile da capire e mantenere. Nel prossimo capitolo, esploreremo il concetto di polimorfismo, che ci darà ancora più flessibilità nel lavorare con oggetti di classi diverse!
