# 4. Incapsulamento

Immaginate di avere una scatola con un lucchetto. All'interno della scatola ci sono oggetti preziosi, e solo voi avete la chiave per aprirla. Questo è essenzialmente il concetto di incapsulamento nella programmazione orientata agli oggetti. L'incapsulamento ci permette di nascondere i dettagli interni di un oggetto e di controllare come il mondo esterno può interagire con esso.

## 4.1 Concetto di incapsulamento

L'incapsulamento è uno dei principi fondamentali della programmazione orientata agli oggetti. Consiste nel raggruppare i dati (proprietà) e i metodi che operano su quei dati all'interno di un'unica unità o oggetto. Inoltre, l'incapsulamento ci permette di controllare l'accesso a questi dati, decidendo quali parti possono essere viste o modificate dall'esterno e quali no.

Torniamo al nostro esempio del gatto. Potremmo voler proteggere alcune informazioni sul gatto, come il suo numero di microchip, e permettere di modificare altre informazioni solo in modi specifici.

## 4.2 Proprietà private in Javascript (ES2022+)

Javascript ha recentemente introdotto il concetto di campi privati nelle classi, rendendoli accessibili solo all'interno della classe stessa. Questi campi sono preceduti dal simbolo #. Vediamo come potremmo usarli nella nostra classe Gatto:

```javascript
class Gatto {
    #microchip;

    constructor(nome, età, microchip) {
        this.nome = nome;
        this.età = età;
        this.#microchip = microchip;
    }

    getMicrochip() {
        return this.#microchip;
    }

    miagola() {
        console.log("Miao miao!");
    }
}

let luna = new Gatto("Luna", 2, "ABC123");
console.log(luna.nome);  // Funziona: Luna
console.log(luna.#microchip);  // Errore! Non possiamo accedere direttamente a #microchip
console.log(luna.getMicrochip());  // Funziona: ABC123
```

In questo esempio, #microchip è una proprietà privata. Non possiamo accedervi direttamente dall'esterno della classe, ma possiamo creare un metodo (getMicrochip) per leggere il suo valore quando necessario.

## 4.3 Metodi getter e setter

I metodi getter e setter sono un modo elegante per controllare l'accesso e la modifica delle proprietà di un oggetto. Sono come dei "portieri" che controllano chi entra e chi esce. Vediamo come potremmo usarli per la proprietà età del nostro gatto:

```javascript
class Gatto {
    #età;

    constructor(nome, età) {
        this.nome = nome;
        this.#età = età;
    }

    get età() {
        return this.#età;
    }

    set età(nuovaEtà) {
        if (nuovaEtà > 0) {
            this.#età = nuovaEtà;
        } else {
            console.log("L'età deve essere un numero positivo");
        }
    }

    compleanno() {
        this.età += 1;
        console.log(`${this.nome} ora ha ${this.età} anni!`);
    }
}

let whiskers = new Gatto("Whiskers", 3);
console.log(whiskers.età);  // Usa il getter: 3
whiskers.età = 4;  // Usa il setter
console.log(whiskers.età);  // 4
whiskers.età = -1;  // Usa il setter, ma non cambia l'età
console.log(whiskers.età);  // Ancora 4
whiskers.compleanno();  // Whiskers ora ha 5 anni!
```

In questo esempio, abbiamo reso la proprietà età privata (#età) e abbiamo creato un getter e un setter per controllarla. Il getter ci permette di leggere l'età, mentre il setter ci permette di cambiarla, ma solo se il nuovo valore è positivo. Questo ci dà un controllo molto più fine su come la proprietà può essere modificata.

L'incapsulamento ci aiuta a mantenere il nostro codice più organizzato e sicuro. Ci permette di nascondere i dettagli di implementazione che non devono essere accessibili dall'esterno e di controllare come le proprietà dei nostri oggetti possono essere lette o modificate. Questo rende il nostro codice più robusto e meno soggetto a errori, perché possiamo assicurarci che i nostri oggetti siano sempre in uno stato valido.

Nel prossimo capitolo, vedremo come l'incapsulamento si lega al concetto di information hiding, che ci aiuterà a creare interfacce ancora più pulite e facili da usare per i nostri oggetti!
