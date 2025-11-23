# Template Esonero TCP - Corso di Reti di Calcolatori - ITPS A-L

Template repository per l'assegnazione della prima prova di esonero: client-server TCP.


## Descrizione

Questo repository contiene la struttura base per lo sviluppo di un'applicazione client-server TCP in linguaggio C, utilizzando la libreria standard delle socket. Il codice è progettato per essere portabile su sistemi operativi **Windows**, **Linux** e **macOS**.

## Struttura del Repository

Il repository è organizzato in due progetti Eclipse CDT separati:

```
.
├── client-project/         # Progetto Eclipse per il client
│   ├── .project            # Configurazione progetto Eclipse
│   ├── .cproject           # Configurazione Eclipse CDT
│   └── src/
│       ├── main.c          # File principale del client
│       └── protocol.h      # Header con definizioni e prototipi
│
└── server-project/         # Progetto Eclipse per il server
    ├── .project            # Configurazione progetto Eclipse
    ├── .cproject           # Configurazione Eclipse CDT
    └── src/
        ├── main.c          # File principale del server
        └── protocol.h      # Header con definizioni e prototipi
```

## Come Utilizzare il Template

### 1. Creare la propria copia del repository

1. Cliccare su "Use this template" in alto a destra su GitHub
2. Creare un nuovo repository personale
   - Rinominate il repository sostituendo la parola _template_ con il vostro _cognome_ seguito dalla _matricola_ (`template_esonero_tcp` -> `cognome_12345_esonero_tcp`)
   - Se l'esonero è svolto in coppia, il nome del repository sarà `cognome1_12345_cognome2_6789_esonero_tcp`
4. Clonare il repository sul proprio computer:
   ```bash
   git clone <url-del-tuo-repository>
   ```

### 2. Importare i progetti in Eclipse

1. Aprire **Eclipse CDT**
2. Selezionare `File → Import → General → Existing Projects into Workspace`
3. Selezionare la directory `client-project`
4. Ripetere i passi 2-3 per `server-project`

### 3. Configurare il progetto in Eclipse

Dopo aver importato i progetti, è necessario verificare e configurare le impostazioni del compilatore:

#### Verificare il Toolchain
Per ciascun progetto (client e server):
1. Click destro sul progetto → `Properties`
2. Andare in `C/C++ Build → Tool Chain Editor`
3. Verificare che il **Current toolchain** sia corretto per il proprio sistema operativo:
   - **Linux**: GCC
   - **macOS**: GCC
   - **Windows**: MinGW GCC (Assicurarsi di avere già installato MinGW o MinGW-w64)

#### Solo per Windows: Aggiungere libreria Winsock
Per compilare su Windows, è necessario linkare la libreria Winsock:
1. Click destro sul progetto → `Properties`
2. Andare in `C/C++ Build → Settings`
3. Selezionare `MinGW C Linker → Libraries`
4. In **Libraries (-l)**, cliccare su `Add` e inserire: `wsock32`
5. Applicare le modifiche e cliccare `OK`


## File Principali

### protocol.h
Contiene:
- **Costanti condivise**: numero di porta del server, dimensione buffer, ecc.
- **Prototipi delle funzioni**: inserire qui le firme di tutte le funzioni implementate

Esempio:
```c
#define SERVER_PORT 27015
#define BUFFER_SIZE 512

// Prototipo funzione esempio
int connect_to_server(const char* server_address);
```

### main.c (Client e Server)
Contiene:
- **Codice boilerplate** per la portabilità cross-platform
- **Inizializzazione Winsock** su Windows
- **Sezioni TODO** dove implementare la logica dell'applicazione

## Implementazione dell'Assegnazione

Gli studenti devono:

1. **Definire i parametri** nel file `protocol.h`:
   - Numero di porta dell'applicazione
   - Dimensione dei buffer
   - Altre costanti necessarie

2. **Implementare le funzioni** necessarie:
   - Aggiungere i prototipi nel file `protocol.h`
   - Implementare le funzioni nel file `main.c`

3. **Completare il codice** seguendo le sezioni TODO:
   - **Client**: creazione socket, connessione al server, invio/ricezione dati
   - **Server**: creazione socket, bind, listen, accept, gestione client

## Salvare e Caricare le Modifiche su GitHub

Dopo aver completato lo sviluppo in Eclipse, è necessario salvare le modifiche sul repository GitHub utilizzando Git da riga di comando.

### Workflow Git Completo

1. **Verificare lo stato del repository**

   Prima di tutto, aprire un terminale nella directory del progetto e controllare quali file sono stati modificati o creati:
   ```bash
   git status
   ```

   Questo comando mostra:
   - File modificati (in rosso se non ancora aggiunti)
   - Nuovi file non tracciati
   - File pronti per il commit (in verde)

2. **Aggiungere file allo staging area**

   Per aggiungere **tutti** i file modificati e i nuovi file:
   ```bash
   git add .
   ```

   Oppure, per aggiungere **file specifici**:
   ```bash
   git add client-project/src/main.c
   git add server-project/src/main.c
   git add client-project/src/protocol.h
   ```

3. **Committare le modifiche**

   Dopo aver aggiunto i file allo staging area, creare un commit con un messaggio descrittivo:
   ```bash
   git commit -m "Implementazione logica client-server TCP"
   ```

   Il messaggio del commit dovrebbe descrivere brevemente le modifiche apportate. Altri esempi:
   ```bash
   git commit -m "Aggiunta funzione di gestione connessioni"
   git commit -m "Implementazione protocollo comunicazione"
   git commit -m "Fix gestione errori socket"
   ```

4. **Pushare le modifiche su GitHub**

   Infine, caricare i commit sul repository remoto:
   ```bash
   git push
   ```

   Oppure, se è il primo push sul branch corrente:
   ```bash
   git push -u origin main
   ```

### Esempio Pratico Completo

Ecco un esempio del flusso completo dopo aver modificato i file in Eclipse:

```bash
# 1. Controllare lo stato
git status

# 2. Aggiungere tutti i file modificati
git add .

# 3. Verificare che i file siano nello staging area
git status

# 4. Creare il commit
git commit -m "Completamento implementazione client e server"

# 5. Caricare su GitHub
git push
```

### Suggerimenti

- **Committare frequentemente**: Non aspettare di completare tutto il progetto. Fate commit incrementali ogni volta che completate una funzionalità o risolvete un problema.
- **Messaggi descrittivi**: Usate messaggi di commit chiari che descrivano cosa avete fatto, non come lo avete fatto.
- **Controllare sempre**: Usate `git status` prima e dopo `git add` per verificare quali file state per committare.
- **Push regolari**: Fate push regolarmente su GitHub per avere un backup del vostro lavoro.

### In Caso di Problemi

Se avete modificato i file sia in Eclipse che altrove e ci sono conflitti:
```bash
# Scaricare le ultime modifiche dal repository
git pull

# Risolvere eventuali conflitti manualmente
# Poi aggiungere i file risolti e committare
git add .
git commit -m "Risoluzione conflitti"
git push
```

## Note Importanti

- Utilizzare le costanti definite in `protocol.h` invece di valori hardcoded

## Licenza

Vedere il file [LICENSE](LICENSE) per i dettagli.
