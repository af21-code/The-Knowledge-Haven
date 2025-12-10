# 📚 The Knowledge Haven - Database Project

> Progetto di Basi di Dati 2024/25 - Università degli Studi di Salerno "Hippocratica Civitas"

**The Knowledge Haven** è un sistema di gestione per una biblioteca scientifica moderna che integra la gestione delle risorse fisiche (libri, scaffali, posti) con una piattaforma digitale per la fruizione di eventi e contenuti multimediali.

## 👥 Team di Sviluppo
* **Angelo Fusco**
* **Gabriele Di Palma**
* **Giovanni De Simone**

---

## 📖 Descrizione del Progetto
L'obiettivo del progetto è modellare e implementare una base di dati per una biblioteca scientifica che funge da hub di conoscenza. Il sistema gestisce:
* **Risorse Fisiche:** Catalogazione di libri scientifici, manuali e dispositivi multimediali organizzati in scaffali.
* **Spazi:** Gestione e prenotazione dei posti a sedere nelle sale lettura e conferenze.
* **Piattaforma Digitale:** Un sistema per la gestione di account utenti, streaming di eventi, workshop interattivi e un sistema di moderazione con "super-utenti".
* **Amministrazione:** Gestione del personale, fornitori, fatturazione e sponsorizzazioni.

## ⚙️ Funzionalità Principali
Il database supporta le seguenti operazioni chiave:
1.  **Gestione Utenti:** Registrazione e profilazione di Utenti, Clienti (con Fidelity Card) e Personale.
2.  **Streaming ed Eventi:** Gestione di dirette, salvataggio clip (max 5 min), chat in tempo reale e sponsorizzazioni.
3.  **Moderazione:** Sistema di valutazione dei moderatori (punteggio 1-5) basato sui feedback dei relatori.
4.  **Logistica:** Tracciamento della posizione dei libri (Scaffale/Altezza) e conteggio automatico degli articoli.
5.  **Contabilità:** Gestione di fatture, fornitori ed emittenti.

## 🗂️ Progettazione del Database

### 1. Modello Concettuale (EER)
Il diagramma Entità-Relazione esteso include entità principali come `Sede Centrale`, `Persona`, `Articolo` (specializzato in `Libro` e `Dispositivo Multimediale`), `Fattura` e `Sito Web`.
* *Nota sulle Gerarchie:* Le generalizzazioni "Persona" e "Articolo" sono state ristrutturate nella fase logica utilizzando relazioni e entità deboli per ottimizzare la struttura.

### 2. Analisi delle Ridondanze
Durante la progettazione logica è stata effettuata un'analisi prestazionale sull'attributo `NumeroDiArticoli` nell'entità `Scaffale`.
* **Decisione:** Il dato ridondante è stato **mantenuto**.
* **Motivazione:** L'analisi degli accessi ha mostrato che le operazioni di lettura (visualizzazione scaffali) sono molto più frequenti (70/gg) rispetto agli aggiornamenti, rendendo conveniente sacrificare spazio per guadagnare in prestazioni.

### 3. Schema Relazionale (Normalizzato)
Il database è progettato in **Terza Forma Normale (3NF)**:
* **SedeCentrale:** `(Identificativo)`
* **Posti:** `(ID_Posto, Descrizione)`
* **Persona:** `(CF, Nome, Cognome, DataDiNascita, LuogoDiNascita)`
* **Utente/Cliente/Personale:** Tabelle collegate via foreign key a Persona.
* **Articolo:** `(CodiceArticolo, Quantità)`
* **Scaffale:** `(CodiceIdentificativo, Altezza, NumeroDiArticoli)`
* **Libro:** `(ISBN, CasaEditrice, Autore, Edizione)`

---

## 🛠️ Tech Stack
* **DBMS:** MySQL
* **Linguaggio:** SQL (DDL, DML)

## 🚀 Installazione e Utilizzo

1.  **Clona la repository:**
    ```bash
    git clone [https://github.com/tuo-username/KnowHaven.git](https://github.com/tuo-username/KnowHaven.git)
    ```
2.  **Importa il Database:**
    Esegui lo script SQL fornito (es. `database.sql`) nel tuo client MySQL (Workbench, phpMyAdmin, o da riga di comando):
    ```sql
    source /path/to/knowhaven.sql;
    ```
3.  **Esempi di Query:**
    Il progetto include diverse procedure predefinite. Ecco alcuni esempi:

    * *Inserimento nuovo utente:*
        ```sql
        INSERT INTO Persona VALUES ('CF123...', 'Mario', 'Rossi', ...);
        INSERT INTO Utente VALUES ('CF123...', 'Roma');
        ```
    * *Visualizzazione scaffali:*
        ```sql
        SELECT * FROM Scaffale;
        ```
    * *Ricerca libri per autore:*
        ```sql
        SELECT * FROM Libro WHERE Autore = 'Italo Calvino';
        ```

## 📊 Test Suite
Il progetto include una suite di test per verificare:
* La creazione corretta delle tabelle e dei vincoli di integrità.
* Il popolamento iniziale (INSERT) di tutte le entità.
* L'esecuzione delle query operative (Update eventi, Insert valutazioni, ecc.).

---
*Progetto realizzato per l'esame di Basi di Dati, Prof. Di Biasi L., Tortora G. A.A. 2024/2025.*
