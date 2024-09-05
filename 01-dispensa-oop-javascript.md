# 1. Introduzione alla programmazione ad oggetti

## 1.1 Cos'è la programmazione ad oggetti?

La programmazione ad oggetti (OOP - Object-Oriented Programming) è un paradigma di programmazione basato sul concetto di "oggetti", che possono contenere dati e codice. I dati sono sotto forma di campi (spesso noti come attributi o proprietà), e il codice è sotto forma di procedure (spesso chiamate metodi).

Caratteristiche principali:
- Organizzazione del codice in unità chiamate oggetti
- Combinazione di dati e comportamenti
- Progettazione di programmi in termini di oggetti che interagiscono tra loro

## 1.2 Vantaggi della programmazione ad oggetti

1. Modularità: Il codice per un oggetto può essere scritto e mantenuto indipendentemente dal codice di altri oggetti.

2. Riusabilità: Gli oggetti possono essere riutilizzati in diversi programmi.

3. Scalabilità e manutenibilità: I sistemi OOP sono più facili da modificare e estendere.

4. Astrazione: L'OOP permette di nascondere i dettagli implementativi e mostrare solo le funzionalità all'utente.

5. Organizzazione: Fornisce un modo chiaro di organizzare il codice in progetti complessi.

## 1.3 Concetti fondamentali: oggetti e classi

### Oggetti

Un oggetto è un'istanza di una classe. Rappresenta un'entità del mondo reale e ha:
- Stato (attributi o proprietà)
- Comportamento (metodi o funzioni)

Esempio in JavaScript:
```javascript
let cane = {
    nome: "Fido",
    razza: "Labrador",
    abbaia: function() {
        console.log("Bau bau!");
    }
};
```

### Classi

Una classe è un "progetto" o un "modello" per creare oggetti. Definisce:
- Attributi: le caratteristiche dell'oggetto
- Metodi: le azioni che l'oggetto può compiere

Esempio di classe in JavaScript (ES6+):
```javascript
class Cane {
    constructor(nome, razza) {
        this.nome = nome;
        this.razza = razza;
    }

    abbaia() {
        console.log("Bau bau!");
    }
}

// Creazione di un'istanza
let mioCane = new Cane("Fido", "Labrador");
mioCane.abbaia(); // Output: Bau bau!
```

Questa introduzione fornisce le basi per comprendere la programmazione ad oggetti, preparando gli studenti per i concetti più avanzati che seguiranno nel resto della dispensa.
