# 9. Prototipi in Javascript

Immaginate di essere in una grande famiglia. Quando avete bisogno di qualcosa, prima controllate se ce l'avete voi. Se non ce l'avete, chiedete a vostra madre. Se neanche lei ce l'ha, chiedete a vostra nonna. Questo processo continua finché non trovate ciò che cercate o arrivate al capostipite della famiglia che non ha nessuno a cui chiedere. Questo è essenzialmente il modo in cui funzionano i prototipi in Javascript!

## 9.1 Il sistema dei prototipi

Javascript è un linguaggio basato sui prototipi. Questo significa che l'ereditarietà in Javascript è implementata attraverso oggetti che fanno riferimento ad altri oggetti, chiamati prototipi. Ogni oggetto in Javascript ha un collegamento interno ad un altro oggetto, il suo prototipo. Quando cerchiamo una proprietà su un oggetto, se non la troviamo, Javascript la cerca nel prototipo dell'oggetto, poi nel prototipo del prototipo, e così via, fino a raggiungere la fine della catena dei prototipi.

Vediamo un esempio semplice:

```javascript
let animale = {
    mangia: function() {
        console.log("L'animale sta mangiando");
    }
};

let gatto = Object.create(animale);
gatto.miagola = function() {
    console.log("Miao!");
};

gatto.miagola();  // Miao!
gatto.mangia();   // L'animale sta mangiando
```

In questo esempio, `gatto` è un oggetto che ha `animale` come suo prototipo. Quando chiamiamo `gatto.mangia()`, Javascript prima cerca la funzione `mangia` in `gatto`. Non trovandola, la cerca nel prototipo di `gatto`, che è `animale`, e la trova lì.

## 9.2 Catena dei prototipi

La catena dei prototipi può essere più lunga di un solo livello. Ogni oggetto in Javascript ha un prototipo, tranne l'oggetto radice `Object.prototype`, che è il capostipite di tutti gli oggetti.

Vediamo un esempio più complesso:

```javascript
let animale = {
    respira: function() {
        console.log("L'animale sta respirando");
    }
};

let mammifero = Object.create(animale);
mammifero.allatta = function() {
    console.log("Il mammifero sta allattando");
};

let gatto = Object.create(mammifero);
gatto.miagola = function() {
    console.log("Miao!");
};

gatto.miagola();  // Miao!
gatto.allatta();  // Il mammifero sta allattando
gatto.respira();  // L'animale sta respirando
```

In questo esempio, abbiamo una catena di prototipi: `gatto` -> `mammifero` -> `animale`. Quando chiamiamo `gatto.respira()`, Javascript cerca la funzione `respira` prima in `gatto`, poi in `mammifero`, e infine la trova in `animale`.

## 9.3 Ereditarietà basata sui prototipi

L'ereditarietà in Javascript è implementata attraverso questa catena di prototipi. Quando definiamo una classe in Javascript (usando la sintassi delle classi introdotta in ES6), dietro le quinte Javascript sta ancora usando i prototipi.

Vediamo come funziona l'ereditarietà con le classi:

```javascript
class Animale {
    constructor(nome) {
        this.nome = nome;
    }

    respira() {
        console.log(`${this.nome} sta respirando`);
    }
}

class Gatto extends Animale {
    constructor(nome) {
        super(nome);
    }

    miagola() {
        console.log(`${this.nome} fa miao!`);
    }
}

let luna = new Gatto("Luna");
luna.miagola();  // Luna fa miao!
luna.respira();  // Luna sta respirando
```

Dietro le quinte, Javascript sta creando una catena di prototipi. Il prototipo di `luna` è `Gatto.prototype`, e il prototipo di `Gatto.prototype` è `Animale.prototype`.

Possiamo vedere questa catena di prototipi usando `Object.getPrototypeOf()`:

```javascript
console.log(Object.getPrototypeOf(luna) === Gatto.prototype);  // true
console.log(Object.getPrototypeOf(Gatto.prototype) === Animale.prototype);  // true
```

Comprendere i prototipi è fondamentale per capire come funziona Javascript sotto il cofano. Anche se nella programmazione quotidiana potreste non lavorare direttamente con i prototipi, questa conoscenza vi aiuterà a comprendere meglio il comportamento del vostro codice e a risolvere eventuali problemi.

Nel prossimo capitolo, esploreremo alcuni pattern di progettazione orientati agli oggetti comuni in Javascript. Questi pattern sfruttano spesso i concetti che abbiamo visto finora, inclusi i prototipi, per creare strutture di codice robuste e riutilizzabili!
