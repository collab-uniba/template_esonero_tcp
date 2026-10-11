# Template Esonero TCP - Corso di Reti di Calcolatori - CORSO A.A.

Template repository per l'assegnazione della prima prova di esonero: client-server TCP.


## Descrizione

Questo repository contiene la struttura base per lo sviluppo di un'applicazione client-server TCP in linguaggio C, utilizzando l'API socket (BSD socket su Linux e macOS, Winsock su Windows). Il codice è progettato per essere portabile su sistemi operativi **Windows**, **Linux** e **macOS**.

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
2. Creare un nuovo repository personale (nome a scelta) con visibilità _Public_
3. Clonare il repository sul proprio computer:
   ```bash
   git clone <url-del-tuo-repository>
   ```

### 2. Importare i progetti in Eclipse

1. Aprire **Eclipse CDT**
2. Selezionare `File → Import → General → Existing Projects into Workspace`
3. In **Select root directory** scegliere la cartella del repository clonato: compaiono `client-project` e `server-project`, selezionarli entrambi
4. Lasciare **deselezionata** l'opzione **Copy projects into workspace**, altrimenti le modifiche non finiscono nel repository Git
5. Cliccare `Finish`

### 3. Configurare il progetto in Eclipse

Dopo aver importato i progetti, è necessario verificare e configurare le impostazioni del compilatore:

#### Verificare la toolchain
Per ciascun progetto (client e server):
1. Click destro sul progetto → `Properties`
2. Andare in `C/C++ Build → Tool Chain Editor`
3. Verificare che il **Current toolchain** sia corretto per il proprio sistema operativo:
   - **Linux**: Linux GCC
   - **macOS**: MacOSX GCC (richiede gli Xcode Command Line Tools: `xcode-select --install`)
   - **Windows**: MinGW GCC (richiede MinGW-w64 già installato)

#### Solo per Windows: Aggiungere libreria Winsock
Per compilare su Windows, è necessario linkare la libreria Winsock. Per ciascun progetto (client e server):
1. Click destro sul progetto → `Properties`
2. Andare in `C/C++ Build → Settings` e, in alto, scegliere **Configuration: [All configurations]**
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
- Solo nel server: la disabilitazione del buffering di `stdout` (`setvbuf`), che garantisce la stampa immediata del log; non rimuoverla

### Eseguire client e server con argomenti
Per passare gli argomenti da riga di comando all'interno di Eclipse:
1. `Run → Run Configurations…`
2. Selezionare la configurazione del progetto sotto **C/C++ Application**
3. Nella scheda **Arguments**, inserire gli argomenti in **Program arguments** e cliccare `Run`

In alternativa, eseguire il file compilato da terminale (si trova nella cartella `Debug/` del progetto).

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

### Note

- Utilizzare le costanti definite in `protocol.h` invece di valori hardcoded

## Salvare e Caricare le Modifiche su GitHub

Durante lo sviluppo in Eclipse, salvate regolarmente le modifiche sul repository GitHub utilizzando Git da riga di comando.

### Workflow Git Completo

1. **Sincronizzare con il repository remoto**

   Prima di iniziare a lavorare, scaricare eventuali modifiche fatte da altri collaboratori sul repository condiviso:
   ```bash
   git pull
   ```

   Questo comando scarica e integra le modifiche dal repository remoto. È particolarmente importante quando si lavora in coppia o si lavora da computer diversi.

2. **Verificare lo stato del repository**

   Aprire un terminale nella directory del progetto e controllare quali file sono stati modificati o creati:
   ```bash
   git status
   ```

   Questo comando mostra:
   - File modificati (in rosso se non ancora aggiunti)
   - Nuovi file non tracciati
   - File pronti per il commit (in verde)

3. **Aggiungere file alla staging area**

   La staging area (area di preparazione) è uno spazio intermedio dove si selezionano le modifiche da includere nel prossimo commit.

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

4. **Committare le modifiche**

   Dopo aver aggiunto i file alla staging area, creare un commit con un messaggio descrittivo:
   ```bash
   git commit -m "Implementazione logica client-server TCP"
   ```

   Il messaggio del commit dovrebbe descrivere brevemente le modifiche apportate. Altri esempi:
   ```bash
   git commit -m "Aggiunta funzione di gestione connessioni"
   git commit -m "Implementazione protocollo comunicazione"
   git commit -m "Fix gestione errori socket"
   ```

5. **Pushare le modifiche su GitHub**

   Infine, caricare i commit sul repository remoto:
   ```bash
   git push
   ```

### Esempio Pratico Completo

Ecco un esempio del flusso completo dopo aver modificato i file in Eclipse:

```bash
# 1. Sincronizzare con il repository remoto
git pull

# 2. Controllare lo stato
git status

# 3. Aggiungere tutti i file modificati
git add .

# 4. Verificare che i file siano nella staging area
git status

# 5. Creare il commit
git commit -m "Completamento implementazione client e server"

# 6. Caricare su GitHub
git push
```

### Suggerimenti

- **Sincronizzare prima di lavorare**: Fate sempre `git pull` prima di iniziare a modificare i file, specialmente se lavorate in coppia o da computer diversi. Questo riduce il rischio di conflitti.
- **Committare frequentemente**: Non aspettate di completare tutto il progetto. Fate commit incrementali ogni volta che completate una funzionalità o risolvete un problema.
- **Messaggi descrittivi**: Usate messaggi di commit chiari che descrivano cosa avete fatto, non come lo avete fatto.
- **Controllare sempre**: Usate `git status` prima e dopo `git add` per verificare quali file state per committare.
- **Push regolari**: Fate push regolarmente su GitHub per avere un backup del vostro lavoro e per condividere le modifiche con il vostro compagno di coppia.

### In Caso di Problemi

Se `git push` viene rifiutato perché il repository remoto contiene modifiche che non avete in locale (ad es. del compagno di coppia):
```bash
# Scaricare le ultime modifiche dal repository
git pull

# Risolvere eventuali conflitti manualmente
# Poi aggiungere i file risolti e committare
git add .
git commit -m "Risoluzione conflitti"
git push
```

## Licenza

Vedere il file [LICENSE](LICENSE) per i dettagli.
