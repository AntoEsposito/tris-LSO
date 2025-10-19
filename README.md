# 🎮 Tris Multiplayer - Tic-Tac-Toe Online

![C](https://img.shields.io/badge/language-C-blue.svg)
![Docker](https://img.shields.io/badge/docker-enabled-brightgreen.svg)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20macOS%20%7C%20Windows-lightgrey.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

> Un'implementazione completa e robusta del classico gioco del **Tris** (Tic-Tac-Toe) con architettura **client-server**, sviluppata in C per il corso di Laboratorio di Sistemi Operativi.

## 📋 Descrizione

Questo progetto implementa un sistema di gioco multiplayer dove più giocatori possono:
- 🏠 **Creare partite** e invitare altri giocatori
- 🎯 **Unirsi a partite** esistenti tramite una lobby interattiva
- ⚔️ **Sfidare avversari** in tempo reale
- 🔄 **Richiedere rivincite** immediate
- 👥 **Gestire più giocatori** contemporaneamente

### ✨ Caratteristiche Principali

- **Architettura Client-Server**: Comunicazione basata su socket TCP/IP
- **Multi-threading**: Gestione concorrente di più partite simultanee
- **Containerizzazione**: Deploy semplificato tramite Docker
- **Signal Handling**: Gestione robusta dei segnali per sincronizzazione e terminazione
- **Cross-platform**: Supporto completo per Linux, macOS e Windows
- **Mutex & Thread Safety**: Sincronizzazione sicura delle risorse condivise

## 🏗️ Architettura

```
┌─────────────────┐         ┌─────────────────┐
│   Client 1      │         │   Client 2      │
│  (Container)    │◄────┐   │  (Container)    │
└─────────────────┘     │   └─────────────────┘
                        │
                        ▼
                ┌───────────────┐
                │    Server     │
                │  (Container)  │
                │   Port 8080   │
                └───────────────┘
                        │
                        ▼
            Multi-threaded Handler
            - Lobby Management
            - Game Logic
            - Signal Coordination
```

## 🚀 Quick Start

### Prerequisiti

- 🐳 **Docker** installato e in esecuzione ([Download Docker](https://www.docker.com/get-started))
- 🖥️ **Terminal**: PowerShell per Windows, qualsiasi terminal per Unix-like

### Installazione

1. **Clona la repository**
   ```bash
   git clone https://github.com/tuousername/tris-lso.git
   cd tris-lso
   ```

2. **Assicurati che la cartella si chiami esattamente `tris-lso`**

3. **(Solo Unix-like)** Aggiungi il tuo utente al gruppo Docker:
   ```bash
   sudo usermod -aG docker $USER
   ```

4. **(Solo Unix-like)** Dai i permessi di esecuzione:
   ```bash
   chmod +x ./avviounix.sh
   ```

### Avvio del Gioco

#### 🪟 Windows
```powershell
.\avviowindows.ps1
```

#### 🐧 Linux / 🍎 macOS
```bash
./avviounix.sh
```

Lo script ti chiederà quanti client vuoi avviare e aprirà automaticamente una finestra terminale per ciascuno!

### 🛠️ Risoluzione Problemi

#### Errore di Execution Policy (Windows)
```powershell
powershell -ExecutionPolicy Bypass -File "./avviowindows.ps1"
```

#### Attributo di Quarantena (macOS)
```bash
xattr -d com.apple.quarantine ./avviounix.sh
```

#### Avvio Manuale
Se gli script non funzionano, puoi avviare manualmente:
```bash
# Avvia server e N client
docker-compose up --build --scale client=N

# In terminali separati, collega ogni client
docker attach tris-lso-client-1
docker attach tris-lso-client-2
# ... etc
```

## 🎯 Come Giocare

1. **Registrazione**: Al primo avvio, inserisci il tuo nickname
2. **Lobby**: Visualizza le partite disponibili o crea la tua
3. **Crea Partita**: Diventi il proprietario e attendi un avversario
4. **Unisciti**: Richiedi di unirti a una partita esistente
5. **Gioca**: A turno, scegli dove posizionare il tuo simbolo (1-9)
6. **Rivincita**: Al termine, richiedi una rivincita immediata!

### Esempio di Griglia

```
 1 | 2 | 3
-----------
 4 | 5 | 6
-----------
 7 | 8 | 9
```

## 📁 Struttura del Progetto

```
tris-LSO/
├── 📄 docker-compose.yml      # Orchestrazione container
├── 🚀 avviounix.sh            # Script avvio Unix-like
├── 🚀 avviowindows.ps1        # Script avvio Windows
├── 📖 README.md               # Questo file
│
├── 👤 Client/
│   ├── Dockerfile
│   ├── main.c                 # Entry point client
│   ├── funzioni.c             # Logica client
│   ├── funzioni.h             # Header client
│   ├── strutturedati.h        # Strutture dati
│   └── Makefile
│
└── 🖥️ Server/
    ├── Dockerfile
    ├── main.c                 # Entry point server
    ├── funzioni.c             # Logica server
    ├── funzioni.h             # Header server
    ├── strutturedati.h        # Strutture dati
    └── Makefile
```

## 🔧 Tecnologie Utilizzate

- **Linguaggio**: C (C99)
- **Networking**: Socket TCP/IP
- **Concorrenza**: POSIX Threads (pthread)
- **Sincronizzazione**: Mutex, Signal Handling (SIGUSR1, SIGUSR2, SIGALRM)
- **Containerizzazione**: Docker & Docker Compose
- **Build System**: Make

## 🧪 Testing

Il progetto è stato testato su:
- ✅ Ubuntu 20.04/22.04
- ✅ macOS (Intel & Apple Silicon)
- ✅ Windows 10/11 (PowerShell)

## 📝 Licenza

Questo progetto è stato sviluppato per scopi didattici nell'ambito del corso di **Laboratorio di Sistemi Operativi**.
