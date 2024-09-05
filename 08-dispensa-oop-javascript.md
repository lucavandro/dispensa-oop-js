# 8. Composizione vs Ereditarietà

Immaginate di voler costruire una casa. Potreste farlo in due modi: potreste partire da una casa esistente e modificarla (questo sarebbe come l'ereditarietà), oppure potreste costruire la vostra casa da zero, utilizzando mattoni, travi e altri componenti (questo sarebbe come la composizione). Entrambi gli approcci hanno i loro vantaggi, e in programmazione, abbiamo una scelta simile tra ereditarietà e composizione.

## 8.1 Differenze tra composizione ed ereditarietà

L'ereditarietà, come abbiamo visto, ci permette di creare nuove classi basate su classi esistenti. È come dire "un gatto è un tipo di animale". La composizione, d'altra parte, ci permette di costruire oggetti complessi combinando oggetti più semplici. È come dire "un'auto ha un motore".

Mentre l'ereditarietà crea una relazione "è un", la composizione crea una relazione "ha un". Vediamo un esempio per chiarire questa differenza:

```javascript
// Approccio con ereditarietà
class Veicolo {
    constructor(velocitàMassima) {
        this.velocitàMassima = velocitàMassima;
    }

    muovi() {
        console.log(`Mi muovo a una velocità massima di ${this.velocitàMassima} km/h`);
    }
}

class Auto extends Veicolo {
    constructor(velocitàMassima, numeroPosti) {
        super(velocitàMassima);
        this.numeroPosti = numeroPosti;
    }
}

// Approccio con composizione
class Motore {
    constructor(potenza) {
        this.potenza = potenza;
    }

    avvia() {
        console.log(`Motore avviato con potenza ${this.potenza} CV`);
    }
}

class AutoComposta {
    constructor(motore, numeroPosti) {
        this.motore = motore;
        this.numeroPosti = numeroPosti;
    }

    avvia() {
        this.motore.avvia();
        console.log(`Auto avviata con ${this.numeroPosti} posti`);
    }
}

// Uso
let autoEreditarietà = new Auto(200, 5);
autoEreditarietà.muovi();  // Mi muovo a una velocità massima di 200 km/h

let motore = new Motore(150);
let autoComposizione = new AutoComposta(motore, 5);
autoComposizione.avvia();  
// Motore avviato con potenza 150 CV
// Auto avviata con 5 posti
```

In questo esempio, l'approccio con ereditarietà crea una relazione rigida tra `Veicolo` e `Auto`. L'approccio con composizione, invece, ci permette di costruire un'`AutoComposta` utilizzando un oggetto `Motore` separato.

## 8.2 Quando usare la composizione

La composizione è spesso preferita all'ereditarietà perché offre maggiore flessibilità. Ecco alcuni scenari in cui la composizione potrebbe essere la scelta migliore:

1. Quando volete combinare funzionalità da più sorgenti. Ad esempio, un'auto potrebbe avere un motore, un sistema di navigazione e un sistema audio, tutti oggetti separati.

2. Quando volete cambiare il comportamento a runtime. Con la composizione, potete facilmente sostituire un componente con un altro.

3. Quando la relazione tra le classi non è veramente "è un". Ad esempio, un'anatra può nuotare, ma non è corretto dire che "un'anatra è un nuotatore". In questo caso, potremmo usare la composizione per aggiungere la capacità di nuotare.

## 8.3 Implementazione della composizione in Javascript

Vediamo un esempio più elaborato di composizione:

```javascript
class SistemaDiNavigazione {
    navigate(destinazione) {
        console.log(`Navigando verso ${destinazione}`);
    }
}

class SistemaAudio {
    riproduce(canzone) {
        console.log(`Riproducendo ${canzone}`);
    }
}

class Auto {
    constructor(motore, navigazione, audio) {
        this.motore = motore;
        this.navigazione = navigazione;
        this.audio = audio;
    }

    avvia() {
        this.motore.avvia();
    }

    navigaVerso(destinazione) {
        this.navigazione.navigate(destinazione);
    }

    riproduciMusica(canzone) {
        this.audio.riproduce(canzone);
    }
}

let miaAuto = new Auto(
    new Motore(200),
    new SistemaDiNavigazione(),
    new SistemaAudio()
);

miaAuto.avvia();  // Motore avviato con potenza 200 CV
miaAuto.navigaVerso("Roma");  // Navigando verso Roma
miaAuto.riproduciMusica("Highway to Hell");  // Riproducendo Highway to Hell
```

In questo esempio, l'`Auto` è composta da diversi componenti indipendenti. Questo approccio offre diversi vantaggi:

1. Flessibilità: Possiamo facilmente aggiungere o rimuovere componenti senza influenzare il resto del sistema.
2. Riusabilità: Possiamo riutilizzare questi componenti in altri contesti. Ad esempio, potremmo usare lo stesso `SistemaAudio` in una classe `CasaIntelligente`.
3. Testabilità: È più facile testare componenti più piccoli e indipendenti.

Ricordate, non c'è una regola fissa su quando usare l'ereditarietà o la composizione. Spesso, la scelta migliore dipende dal contesto specifico del vostro problema. Una buona regola pratica è "componi quando puoi, eredita quando devi".

Nel prossimo capitolo, esploreremo il sistema dei prototipi in Javascript, che è alla base di come Javascript implementa l'ereditarietà dietro le quinte!
