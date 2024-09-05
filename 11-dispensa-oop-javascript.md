# 11. Best practices e convenzioni

Immaginate di entrare in una cucina ben organizzata. Ogni utensile ha il suo posto, gli ingredienti sono etichettati chiaramente, e c'è un sistema logico per tutto. Lavorare in una cucina del genere è un piacere, vero? Lo stesso vale per il codice ben scritto. Seguire le best practices e le convenzioni nella programmazione orientata agli oggetti in Javascript è come mantenere una cucina ben organizzata: rende il vostro codice più facile da leggere, capire e mantenere, sia per voi che per gli altri sviluppatori.

## 11.1 Naming conventions per classi e metodi

Una delle prime cose che noterete in un codice ben scritto sono i nomi significativi e coerenti. In Javascript, abbiamo alcune convenzioni che è bene seguire:

1. I nomi delle classi dovrebbero iniziare con una lettera maiuscola e usare il PascalCase. Ad esempio:

```javascript
class AutoElettica {}
class GestoreDatabase {}
class InterfacciaUtente {}
```

2. I nomi dei metodi e delle proprietà dovrebbero iniziare con una lettera minuscola e usare il camelCase. Ad esempio:

```javascript
class Auto {
    accelera() {}
    frena() {}
    get velocitàAttuale() {}
    set velocitàMassima(valore) {}
}
```

3. Le costanti dovrebbero essere in maiuscolo con underscore tra le parole:

```javascript
const VELOCITA_MASSIMA = 200;
const LIVELLO_BATTERIA_CRITICO = 10;
```

Usare nomi descrittivi è cruciale. Un nome dovrebbe dire chiaramente cosa fa una classe o un metodo. Confrontate questi due esempi:

```javascript
// Poco chiaro
class X {
    y() {}
}

// Chiaro e descrittivo
class GestoreFile {
    salvaFile() {}
}
```

## 11.2 Principi SOLID applicati a Javascript

I principi SOLID sono linee guida fondamentali nella programmazione orientata agli oggetti. Vediamo come possiamo applicarli in Javascript:

1. Single Responsibility Principle (Principio di Responsabilità Singola): Una classe dovrebbe avere una sola ragione per cambiare. In altre parole, una classe dovrebbe fare una cosa sola e farla bene.

```javascript
// Non ottimale: questa classe fa troppe cose
class Utente {
    constructor(nome) {
        this.nome = nome;
    }

    salvasuDatabase() {}
    inviaEmail() {}
    generaReport() {}
}

// Meglio: separiamo le responsabilità
class Utente {
    constructor(nome) {
        this.nome = nome;
    }
}

class UtenteDatabase {
    salvaUtente(utente) {}
}

class EmailService {
    inviaEmail(utente, messaggio) {}
}

class ReportGenerator {
    generaReport(utente) {}
}
```

2. Open/Closed Principle (Principio Aperto/Chiuso): Le entità software dovrebbero essere aperte per l'estensione, ma chiuse per la modifica.

```javascript
class Forma {
    area() {
        throw new Error("Il metodo area deve essere implementato");
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
        return Math.PI * this.raggio ** 2;
    }
}

function calcolaAreaTotale(forme) {
    return forme.reduce((somma, forma) => somma + forma.area(), 0);
}
```

In questo esempio, possiamo aggiungere nuove forme senza modificare la funzione `calcolaAreaTotale`.

3. Liskov Substitution Principle (Principio di Sostituzione di Liskov): Gli oggetti di una superclasse dovrebbero essere sostituibili con oggetti delle sue sottoclassi senza alterare la correttezza del programma.

```javascript
class Uccello {
    vola() {
        return "Sto volando";
    }
}

class Pinguino extends Uccello {
    vola() {
        throw new Error("I pinguini non possono volare");
    }
}

// Questo viola il principio di Liskov
function faiVolare(uccello) {
    return uccello.vola();
}

// Meglio: ridefiniamo la gerarchia
class Animale {
    muovi() {
        return "Mi sto muovendo";
    }
}

class UccelloVolante extends Animale {
    vola() {
        return "Sto volando";
    }
}

class Pinguino extends Animale {
    nuota() {
        return "Sto nuotando";
    }
}
```

4. Interface Segregation Principle (Principio di Segregazione dell'Interfaccia): Un client non dovrebbe essere forzato a dipendere da interfacce che non usa.

JavaScript non ha interfacce native, ma possiamo applicare questo principio usando classi astratte o semplicemente dividendo le nostre classi in parti più piccole e specifiche.

```javascript
// Non ottimale
class Stampante {
    stampa() {}
    scansiona() {}
    inviafax() {}
}

// Meglio
class Stampante {
    stampa() {}
}

class Scanner {
    scansiona() {}
}

class FaxMachine {
    inviafax() {}
}

class StampanteMultifunzione extends Stampante {
    scansiona() {}
    inviafax() {}
}
```

5. Dependency Inversion Principle (Principio di Inversione delle Dipendenze): I moduli di alto livello non dovrebbero dipendere da moduli di basso livello. Entrambi dovrebbero dipendere da astrazioni.

```javascript
// Non ottimale
class EmailService {
    inviaEmail(messaggio) {
        // logica per inviare email
    }
}

class Notificatore {
    constructor() {
        this.emailService = new EmailService();
    }

    inviaNotifica(messaggio) {
        this.emailService.inviaEmail(messaggio);
    }
}

// Meglio
class MessaggioService {
    invia(messaggio) {
        throw new Error("Il metodo invia deve essere implementato");
    }
}

class EmailService extends MessaggioService {
    invia(messaggio) {
        // logica per inviare email
    }
}

class SMSService extends MessaggioService {
    invia(messaggio) {
        // logica per inviare SMS
    }
}

class Notificatore {
    constructor(messaggioService) {
        this.messaggioService = messaggioService;
    }

    inviaNotifica(messaggio) {
        this.messaggioService.invia(messaggio);
    }
}

// Uso
const notificatoreEmail = new Notificatore(new EmailService());
const notificatoreSMS = new Notificatore(new SMSService());
```

Seguire queste best practices e convenzioni richiede un po' di pratica e riflessione, ma alla lunga rende il vostro codice molto più robusto, flessibile e facile da mantenere. Ricordate, scrivere codice non è solo farlo funzionare, ma farlo funzionare in modo che sia comprensibile e modificabile nel tempo.

Nel prossimo capitolo, metteremo in pratica tutto ciò che abbiamo imparato con alcuni esercizi e progetti pratici. Preparatevi a sporcarvi le mani con del codice reale!
