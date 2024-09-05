# 10. Pattern di progettazione orientati agli oggetti in Javascript

Immaginate di essere un architetto. Quando progettate una casa, non partite sempre da zero. Avete un repertorio di soluzioni consolidate per problemi comuni: come progettare una cucina funzionale, come organizzare gli spazi, come gestire l'illuminazione. Allo stesso modo, nella programmazione orientata agli oggetti, abbiamo dei "progetti" collaudati per risolvere problemi ricorrenti. Questi sono i pattern di progettazione.

I pattern di progettazione sono soluzioni generali a problemi comuni nello sviluppo del software. Non sono codice pronto all'uso, ma piuttosto linee guida su come affrontare certi problemi. In questa sezione, esploreremo tre pattern di progettazione molto utilizzati in Javascript: Singleton, Factory e Observer.

## 10.1 Singleton

Il pattern Singleton garantisce che una classe abbia una sola istanza e fornisce un punto di accesso globale a questa istanza. È utile quando vogliamo avere un'unica copia di un oggetto in tutta la nostra applicazione.

Immaginate di avere un'applicazione con un unico database di configurazione. Non volete creare multiple istanze di questo database, ma volete assicurarvi che tutti i componenti dell'applicazione stiano accedendo alla stessa configurazione.

Ecco come potremmo implementare un Singleton in Javascript:

```javascript
class ConfigDatabase {
    constructor() {
        if (ConfigDatabase.instance) {
            return ConfigDatabase.instance;
        }
        this.config = {};
        ConfigDatabase.instance = this;
    }

    setConfig(key, value) {
        this.config[key] = value;
    }

    getConfig(key) {
        return this.config[key];
    }
}

// Uso
const config1 = new ConfigDatabase();
config1.setConfig('theme', 'dark');

const config2 = new ConfigDatabase();
console.log(config2.getConfig('theme'));  // Output: 'dark'

console.log(config1 === config2);  // Output: true
```

In questo esempio, non importa quante volte creiamo una nuova istanza di `ConfigDatabase`, otterremo sempre la stessa istanza. Questo ci assicura che tutte le parti della nostra applicazione stiano lavorando con la stessa configurazione.

## 10.2 Factory

Il pattern Factory ci fornisce un modo per creare oggetti senza specificare esattamente la classe dell'oggetto che verrà creato. È utile quando la creazione di un oggetto è complessa o quando la decisione su quale tipo di oggetto creare dipende da qualche condizione.

Immaginate di avere un'applicazione che lavora con diversi tipi di veicoli. A seconda dell'input dell'utente, potremmo dover creare un'auto, una moto o una bicicletta.

Ecco come potremmo implementare un Factory in Javascript:

```javascript
class Auto {
    guidare() {
        console.log("Sto guidando un'auto");
    }
}

class Moto {
    guidare() {
        console.log("Sto guidando una moto");
    }
}

class Bicicletta {
    guidare() {
        console.log("Sto pedalando una bicicletta");
    }
}

class VeicoloFactory {
    creaVeicolo(tipo) {
        switch(tipo) {
            case 'auto':
                return new Auto();
            case 'moto':
                return new Moto();
            case 'bicicletta':
                return new Bicicletta();
            default:
                throw new Error('Tipo di veicolo non supportato');
        }
    }
}

// Uso
const factory = new VeicoloFactory();
const auto = factory.creaVeicolo('auto');
const moto = factory.creaVeicolo('moto');

auto.guidare();  // Output: Sto guidando un'auto
moto.guidare();  // Output: Sto guidando una moto
```

In questo esempio, `VeicoloFactory` si occupa di creare l'oggetto appropriato basandosi sul tipo fornito. Il codice che usa la factory non deve preoccuparsi dei dettagli di come vengono creati i diversi tipi di veicoli.

## 10.3 Observer

Il pattern Observer definisce una dipendenza uno-a-molti tra oggetti, in modo che quando un oggetto cambia stato, tutti i suoi dipendenti vengono notificati e aggiornati automaticamente. È molto utile quando abbiamo un oggetto che deve comunicare cambiamenti a molti altri oggetti.

Immaginate un'app meteo dove molti componenti dell'interfaccia utente devono essere aggiornati quando cambiano i dati meteorologici.

Ecco come potremmo implementare un Observer in Javascript:

```javascript
class WeatherStation {
    constructor() {
        this.observers = [];
        this.temperature = 0;
    }

    addObserver(observer) {
        this.observers.push(observer);
    }

    removeObserver(observer) {
        const index = this.observers.indexOf(observer);
        if (index > -1) {
            this.observers.splice(index, 1);
        }
    }

    setTemperature(temp) {
        console.log('WeatherStation: nuova temperatura misurata: ' + temp);
        this.temperature = temp;
        this.notifyObservers();
    }

    notifyObservers() {
        for (let observer of this.observers) {
            observer.update(this.temperature);
        }
    }
}

class TemperatureDisplay {
    constructor(name) {
        this.name = name;
    }

    update(temperature) {
        console.log(`${this.name}: La temperatura è ${temperature}°C`);
    }
}

// Uso
const weatherStation = new WeatherStation();

const display1 = new TemperatureDisplay('Display 1');
const display2 = new TemperatureDisplay('Display 2');

weatherStation.addObserver(display1);
weatherStation.addObserver(display2);

weatherStation.setTemperature(25);
// Output:
// WeatherStation: nuova temperatura misurata: 25
// Display 1: La temperatura è 25°C
// Display 2: La temperatura è 25°C
```

In questo esempio, `WeatherStation` è l'oggetto osservato, e i `TemperatureDisplay` sono gli osservatori. Quando la temperatura cambia, tutti i display vengono automaticamente aggiornati.

Questi pattern di progettazione sono strumenti potenti nel vostro arsenale di sviluppatori. Vi aiutano a strutturare il vostro codice in modi che sono stati provati e testati da molti sviluppatori nel corso degli anni. Tuttavia, ricordate che non sono soluzioni universali. Usateli quando hanno senso per il vostro specifico problema, non forzateli in ogni situazione.

Nel prossimo capitolo, esploreremo alcune best practices e convenzioni nella programmazione orientata agli oggetti in Javascript. Queste linee guida vi aiuteranno a scrivere codice più pulito, più leggibile e più manutenibile!
