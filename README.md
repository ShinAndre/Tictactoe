# ⭕❌ Tris

Un semplice gioco del **Tris** (Tic-Tac-Toe) per due giocatori, realizzato con **Vue 3**, **TypeScript** e la Composition API (`<script setup>`).

## ✨ Funzionalità

- Partita a due giocatori sullo stesso dispositivo (X inizia sempre)
- Rilevamento automatico di vittoria e pareggio
- Evidenziazione della linea vincente
- Punteggio persistente durante la sessione (vittorie X, vittorie O, pareggi)
- Pulsante **Nuova partita** per ricominciare senza azzerare il punteggio
- Tema scuro con colori ispirati a [Catppuccin](https://github.com/catppuccin/catppuccin)

## 🛠️ Tecnologie

- [Vue 3](https://vuejs.org/) (Composition API, `<script setup>`)
- [TypeScript](https://www.typescriptlang.org/)
- CSS scoped

## 🚀 Come iniziare

### Prerequisiti

- [Node.js](https://nodejs.org/) 18 o superiore
- npm (oppure pnpm / yarn)

### Installazione

```bash
# Clona il repository
git clone https://github.com/<tuo-utente>/<nome-repo>.git
cd <nome-repo>

# Installa le dipendenze
npm install

# Avvia il server di sviluppo
npm run dev
```

Poi apri l'indirizzo mostrato nel terminale (di solito `http://localhost:5173`).

### Build di produzione

```bash
npm run build
npm run preview
```

## 🎮 Come si gioca

1. Il giocatore **X** inizia sempre.
2. Clicca su una cella vuota per piazzare il tuo simbolo.
3. Vince chi allinea tre simboli in orizzontale, verticale o diagonale.
4. Se tutte le celle sono piene senza vincitore, la partita finisce in **pareggio**.
5. Premi **Nuova partita** per giocare di nuovo: il punteggio viene mantenuto.

## 🧠 Come funziona

Tutta la logica è contenuta in `App.vue`:

| Elemento | Descrizione |
|---|---|
| `board` | Array di 9 celle (`'X'`, `'O'` o `null`) |
| `LINES` | Le 8 combinazioni vincenti |
| `winLine` | Computed che trova la combinazione vincente, se presente |
| `winner` / `isDraw` | Computed derivati dallo stato della board |
| `status` | Testo mostrato sopra la griglia (turno, vittoria o pareggio) |
| `play(i)` | Gestisce la mossa, aggiorna il punteggio e cambia turno |
| `reset()` | Svuota la griglia e riporta il turno a X |

## 📁 Struttura

```
src/
└── App.vue    # Componente principale: template, logica e stili
```

## 💡 Idee per sviluppi futuri

- [ ] Modalità contro il computer (con algoritmo minimax)
- [ ] Salvataggio del punteggio in `localStorage`
- [ ] Alternanza del giocatore che inizia
- [ ] Animazioni e suoni
- [ ] Possibilità di personalizzare i nomi dei giocatori

## 📄 Licenza

Distribuito con licenza [MIT](LICENSE). Sentiti libero di usare e modificare il progetto.
