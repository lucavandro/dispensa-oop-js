# 12. Esercizi e progetti pratici

Ora che abbiamo esplorato i concetti fondamentali della programmazione orientata agli oggetti in Javascript, è tempo di mettere in pratica ciò che abbiamo imparato. Come si dice, la pratica rende perfetti! In questa sezione, affronteremo alcuni esercizi e progetti pratici che vi aiuteranno a consolidare la vostra comprensione e a sviluppare le vostre capacità di programmazione orientata agli oggetti.

## 12.1 Creazione di una semplice gerarchia di classi

Per il nostro primo esercizio, creeremo una semplice gerarchia di classi per un sistema di gestione di una biblioteca. Questo ci permetterà di mettere in pratica i concetti di ereditarietà e polimorfismo.

```javascript
class MediaItem {
    constructor(titolo, anno) {
        this.titolo = titolo;
        this.anno = anno;
        this.prestato = false;
    }

    presta() {
        if (this.prestato) {
            console.log(`${this.titolo} è già in prestito.`);
        } else {
            this.prestato = true;
            console.log(`${this.titolo} è stato prestato.`);
        }
    }

    restituisci() {
        if (this.prestato) {
            this.prestato = false;
            console.log(`${this.titolo} è stato restituito.`);
        } else {
            console.log(`${this.titolo} non era in prestito.`);
        }
    }

    mostraInfo() {
        console.log(`Titolo: ${this.titolo}, Anno: ${this.anno}, In prestito: ${this.prestato}`);
    }
}

class Libro extends MediaItem {
    constructor(titolo, anno, autore, numeroPagine) {
        super(titolo, anno);
        this.autore = autore;
        this.numeroPagine = numeroPagine;
    }

    mostraInfo() {
        super.mostraInfo();
        console.log(`Autore: ${this.autore}, Pagine: ${this.numeroPagine}`);
    }
}

class DVD extends MediaItem {
    constructor(titolo, anno, regista, durata) {
        super(titolo, anno);
        this.regista = regista;
        this.durata = durata;
    }

    mostraInfo() {
        super.mostraInfo();
        console.log(`Regista: ${this.regista}, Durata: ${this.durata} minuti`);
    }
}

// Uso
const libro1 = new Libro("Il Signore degli Anelli", 1954, "J.R.R. Tolkien", 1178);
const dvd1 = new DVD("Inception", 2010, "Christopher Nolan", 148);

libro1.mostraInfo();
libro1.presta();
libro1.presta();
libro1.restituisci();

dvd1.mostraInfo();
dvd1.presta();
dvd1.restituisci();
```

In questo esercizio, abbiamo creato una classe base `MediaItem` e due classi derivate `Libro` e `DVD`. Questo ci permette di gestire diversi tipi di media in modo uniforme, dimostrando i principi di ereditarietà e polimorfismo.

## 12.2 Implementazione di un sistema di gestione studenti

Per il nostro secondo esercizio, implementeremo un semplice sistema di gestione studenti. Questo ci permetterà di mettere in pratica l'incapsulamento e l'uso dei getter e setter.

```javascript
class Studente {
    #nome;
    #cognome;
    #voti;

    constructor(nome, cognome) {
        this.#nome = nome;
        this.#cognome = cognome;
        this.#voti = [];
    }

    get nomeCompleto() {
        return `${this.#nome} ${this.#cognome}`;
    }

    aggiungiVoto(voto) {
        if (voto >= 0 && voto <= 30) {
            this.#voti.push(voto);
        } else {
            console.log("Voto non valido. Deve essere compreso tra 0 e 30.");
        }
    }

    get mediaVoti() {
        if (this.#voti.length === 0) return 0;
        const somma = this.#voti.reduce((acc, voto) => acc + voto, 0);
        return somma / this.#voti.length;
    }

    mostraInfo() {
        console.log(`Studente: ${this.nomeCompleto}`);
        console.log(`Media voti: ${this.mediaVoti.toFixed(2)}`);
    }
}

class Corso {
    constructor(nome) {
        this.nome = nome;
        this.studenti = [];
    }

    aggiungiStudente(studente) {
        this.studenti.push(studente);
    }

    mostraInfoCorso() {
        console.log(`Corso: ${this.nome}`);
        console.log(`Numero di studenti: ${this.studenti.length}`);
        this.studenti.forEach(studente => studente.mostraInfo());
    }
}

// Uso
const studente1 = new Studente("Mario", "Rossi");
studente1.aggiungiVoto(28);
studente1.aggiungiVoto(30);
studente1.aggiungiVoto(26);

const studente2 = new Studente("Laura", "Bianchi");
studente2.aggiungiVoto(29);
studente2.aggiungiVoto(27);
studente2.aggiungiVoto(30);

const corso = new Corso("Programmazione Avanzata");
corso.aggiungiStudente(studente1);
corso.aggiungiStudente(studente2);

corso.mostraInfoCorso();
```

In questo esercizio, abbiamo creato una classe `Studente` che usa proprietà private (indicate dal simbolo #) per incapsulare i dati dello studente. Abbiamo anche implementato getter per accedere in modo controllato a questi dati. La classe `Corso` dimostra come possiamo lavorare con una collezione di oggetti `Studente`.

## 12.3 Sviluppo di un gioco semplice orientato agli oggetti

Per il nostro ultimo progetto, svilupperemo un semplice gioco di carte. Questo ci permetterà di mettere in pratica molti dei concetti che abbiamo imparato, inclusi l'uso di classi, l'incapsulamento, e la composizione.

```javascript
class Carta {
    constructor(seme, valore) {
        this.seme = seme;
        this.valore = valore;
    }

    toString() {
        return `${this.valore} di ${this.seme}`;
    }
}

class Mazzo {
    constructor() {
        this.carte = [];
        const semi = ['Cuori', 'Quadri', 'Fiori', 'Picche'];
        const valori = ['Asso', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Regina', 'Re'];

        for (let seme of semi) {
            for (let valore of valori) {
                this.carte.push(new Carta(seme, valore));
            }
        }
    }

    mescola() {
        for (let i = this.carte.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [this.carte[i], this.carte[j]] = [this.carte[j], this.carte[i]];
        }
    }

    pescaCarta() {
        return this.carte.pop();
    }
}

class Giocatore {
    constructor(nome) {
        this.nome = nome;
        this.mano = [];
    }

    pescaCarta(mazzo) {
        const carta = mazzo.pescaCarta();
        this.mano.push(carta);
        return carta;
    }

    mostraMano() {
        console.log(`${this.nome} ha in mano:`);
        this.mano.forEach(carta => console.log(carta.toString()));
    }
}

class GiocoCarte {
    constructor() {
        this.mazzo = new Mazzo();
        this.giocatori = [];
    }

    aggiungiGiocatore(nome) {
        this.giocatori.push(new Giocatore(nome));
    }

    iniziaGioco(numeroCarte) {
        this.mazzo.mescola();
        for (let i = 0; i < numeroCarte; i++) {
            for (let giocatore of this.giocatori) {
                giocatore.pescaCarta(this.mazzo);
            }
        }
    }

    mostraManoDiTutti() {
        for (let giocatore of this.giocatori) {
            giocatore.mostraMano();
            console.log('--------------------');
        }
    }
}

// Uso del gioco
const gioco = new GiocoCarte();
gioco.aggiungiGiocatore("Alice");
gioco.aggiungiGiocatore("Bob");
gioco.iniziaGioco(5);
gioco.mostraManoDiTutti();
```

In questo progetto, abbiamo creato diverse classi (`Carta`, `Mazzo`, `Giocatore`, `GiocoCarte`) che lavorano insieme per implementare un semplice gioco di carte. Questo esempio dimostra l'uso della composizione (la classe `GiocoCarte` contiene un `Mazzo` e dei `Giocatore`), l'incapsulamento (ogni classe gestisce il proprio stato interno), e come diversi oggetti possono interagire tra loro in un sistema più complesso.

Questi esercizi e progetti vi danno l'opportunità di mettere in pratica i concetti che abbiamo discusso nei capitoli precedenti. Vi incoraggiamo a sperimentare con questi esempi: provate a estenderli, aggiungere nuove funzionalità, o persino a creare i vostri progetti basati su questi concetti. Ricordate, la programmazione è una competenza che si affina con la pratica, quindi più codice scrivete, migliori diventerete!
