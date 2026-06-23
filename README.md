# Negozio Online - Sistema di Gestione E-Commerce

Un'applicazione Console in C# per la gestione di un piccolo negozio online, sviluppata come progetto d'esame SENA ADSO.

## 🎯 Descrizione del Progetto

Questo sistema simula un negozio online completo con due modalità di accesso:
- **Modalità Utente**: navigazione catalogo, gestione carrello, conferma acquisti, storico ordini
- **Modalità Amministratore**: gestione prodotti, analisi vendite, report quantità

Il progetto dimostra l'applicazione di principi solidi di programmazione orientata agli oggetti (OOP), gestione di eccezioni, validazione input e architettura software pulita.

## ✨ Funzionalità

### Ruolo Utente
- ✅ Visualizzare catalogo completo con prezzi e disponibilità
- ✅ Aggiungere prodotti al carrello con controllo quantità disponibile
- ✅ Modificare quantità nel carrello
- ✅ Rimuovere singoli prodotti dal carrello
- ✅ Svuotare completamente il carrello
- ✅ Confermare acquisto con aggiornamento automatico magazzino
- ✅ Visualizzare storico personale degli acquisti effettuati

### Ruolo Amministratore
- ✅ Visualizzare catalogo completo
- ✅ Aggiungere nuovi prodotti al catalogo
- ✅ Eliminare prodotti dal catalogo
- ✅ Modificare prezzo di un prodotto
- ✅ Aumentare/diminuire quantità disponibile in magazzino
- ✅ Visualizzare tutti gli acquisti effettuati
- ✅ Visualizzare report: quantità iniziale, venduta e disponibile per ogni prodotto

## 🏗️ Architettura e Struttura

### Classi Principali

```
Program
├── ApplicazioneNegozio (orchestrazione interfaccia console)
│   ├── CatalogoProdotti (gestione magazzino)
│   ├── CarrelloUtente (gestione carrello)
│   ├── StoricoAcquisti (storico ordini)
│   └── ServizioNegozio (logica di business)
│
├── Modelli Dati
│   ├── Utente
│   ├── Prodotto
│   ├── ElementoCarrello
│   ├── Acquisto
│   ├── ElementoAcquistato
│   └── ReportProdotto
│
└── Interfacce
    ├── IGestioneCatalogo
    ├── IGestioneCarrello
    └── IGestioneAcquisti
```

### Flusso Logico Principale

1. **Avvio**: l'utente sceglie tra "utente", "amministratore" o "esci"
2. **Menu Utente**: navigazione carrello e acquisti
3. **Conferma Acquisto**: controllo disponibilità → scalamento magazzino → registrazione storico
4. **Menu Amministratore**: gestione prodotti e report

## 🛠️ Tecnologie Utilizzate

- **Linguaggio**: C# (.NET 6.0+)
- **Architettura**: Console Application
- **Pattern**: MVC-like separation with Service Layer
- **Gestione Dati**: In-memory (List<T>)
- **Validazione**: Custom validation + exception handling

## 📋 Requisiti di Sistema

- .NET 6.0 o superiore
- Terminal/Command Prompt
- Editor o IDE (consigliato: Visual Studio, Visual Studio Code)

## 🚀 Come Eseguire

### 1. Clonare il Repository
```bash
git clone https://github.com/TuoUsername/Esame-NegozioOnline.git
cd Esame-NegozioOnline
```

### 2. Compilare il Progetto
```bash
dotnet build
```

### 3. Eseguire l'Applicazione
```bash
dotnet run
```

### 4. Eseguire i Test
```bash
# Nel Main() commentare applicazione.Avvia() e decommentare TestNegozioOnline.EseguiTuttiITest()
dotnet run
```

## 📦 Struttura File

```
NegozioOnlineTemplate/
├── Program.cs                      # Tutto il codice (un unico file)
├── TestNegozioOnline.cs            # Test manuali senza framework esterno
├── NegozioOnlineTemplate.csproj    # File di progetto
├── README.md                       # Questo file
└── .gitignore
```

## 🔧 Logica di Validazione

### Carrello
- ❌ Rifiuta quantità ≤ 0
- ❌ Rifiuta quantità > disponibilità magazzino
- ✅ Aggiorna quantità se prodotto già nel carrello
- ✅ Calcola totale dinamicamente

### Acquisto
- ❌ Rifiuta acquisto con carrello vuoto
- ❌ Ricontrolla disponibilità al momento della conferma
- ✅ Scala automaticamente il magazzino
- ✅ Registra l'acquisto nello storico
- ✅ Svuota il carrello post-acquisto

### Magazzino
- ❌ Non scende sotto zero
- ✅ Traccia quantità iniziale e venduta
- ✅ Calcola disponibilità in tempo reale

## 💡 Punti Salienti dell'Implementazione

### Pattern Implementati
1. **Service Layer**: `ServizioNegozio` coordina le operazioni
2. **Repository Pattern**: `CatalogoProdotti`, `StoricoAcquisti`
3. **Interfaces**: `IGestioneCatalogo`, `IGestioneCarrello`, `IGestioneAcquisti`
4. **Exception Handling**: Gestione controllata di errori e casi limite

### Best Practice Applicate
- ✅ Separazione responsabilità (SRP)
- ✅ Input validation con loop di richiesta
- ✅ Case-insensitive string comparison (`OrdinalIgnoreCase`)
- ✅ Null safety con nullable reference types (`?`)
- ✅ LINQ per query su collection
- ✅ Protezione dati con `private` e copie delle liste

## 📊 Esempio di Utilizzo

### Flusso Utente
```
=== BENVENUTO AL NEGOZIO ONLINE ===

Scegli il ruolo (utente/amministratore/esci): utente

=== MENU UTENTE ===
1. Visualizza catalogo
2. Aggiungi prodotto al carrello
...

Scelta: 1

=== CATALOGO PRODOTTI ===
P001 - Tastiera meccanica - 79.90 euro - Disponibili: 10
P002 - Mouse wireless - 24.50 euro - Disponibili: 25
...
```

## 🧪 Test

Il progetto include una suite di test manuale in `TestNegozioOnline.cs` che verifica:
- Aggiunta/rimozione prodotti dal catalogo
- Operazioni su carrello
- Conferma acquisto con validazioni
- Storico acquisti

Esecuzione test:
```csharp
TestNegozioOnline.EseguiTuttiITest();
```

Output atteso: `[PASS]` per tutti i test completati.

## 📝 Note Importanti

- **Dati Persistenti**: I dati rimangono in memoria durante l'esecuzione. Non sono salvati su file o database.
- **Un Unico File**: Tutto il codice è in `Program.cs` come richiesto dal template (no namespace, no moduli separati).
- **Input da Console**: Tutte le interazioni avvengono tramite input/output console con validazione robusta.

## 🎓 Uso dell'IA

Questo progetto è stato sviluppato con assistenza di Claude (AI) per:
- Progettazione dell'architettura
- Correzione di errori specifici
- Miglioramento di leggibilità e organizzazione del codice
- Validazione della logica implementata

La trascrizione della conversazione è disponibile nel file `AI_CONVERSATION.md`.

## 📄 Licenza

Progetto educativo sviluppato per il corso SENA ADSO.

## ✍️ Autore

**[Nome e Cognome]**  
[Data di completamento]  
Progetto d'esame - C# Console Application

---

## 📞 Contatti e Feedback

Per domande o suggerimenti su questo progetto, aprire una GitHub Issue o contattare direttamente.

---

**Ultimo aggiornamento**: [Data odierna]
