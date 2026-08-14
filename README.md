# Il nostro diario di viaggio 🌊

Sito del diario di viaggio di Ema & Viti.
Online su **https://deltadidirac30.github.io/diario-croazia/**

Tutto sta in un unico file (`index.html`): nessuna piattaforma, nessun account da
pagare, nessuna dipendenza esterna (anche i font sono dentro la cartella `fonts/`).
Finché avete questi file, avete il sito.

---

## Come funziona adesso

Il sito ha **due schermate**:

- la **home**, con una card per ogni viaggio;
- il **diario di un viaggio**, con la barra dei giorni in alto, le statistiche,
  e poi giorno per giorno: foto grandi (cliccabili a tutto schermo), il racconto
  della giornata e le schede di voto.

C'è anche il **selettore IT / EN** in alto a destra: ogni testo esiste in due
versioni, italiana e inglese.

La cosa importante: **non si modifica più l'HTML a mano.** Tutti i contenuti
stanno in una sola lista dentro `index.html`, nella sezione
`1. CONTENUTI` (cercate `const TRIPS`). Si aggiungono giorni e viaggi
scrivendo lì dentro, e il sito si ridisegna da solo.

---

## Aggiungere un nuovo giorno

Aprite `index.html` su GitHub (matita ✏️ in alto a destra), cercate `const TRIPS`
e, dentro `days: [ ... ]`, copiate l'ultimo blocco giorno e incollatelo subito
dopo, cambiando i valori:

```js
{
  n: 14,                                        // numero del giorno
  date:  {it:"14 agosto", en:"14 August"},
  short: {it:"14 ago",    en:"14 Aug"},         // etichetta nella barra in alto
  place: {it:"Vis, Croazia", en:"Vis, Croatia"},
  photos: [],                                    // vedi sotto
  journal: {
    it:"Due righe sulla giornata.",
    en:"A couple of lines about the day."
  },
  cards: [
    { kind:"food", name:"NOME RISTORANTE", rows:[
      {k:"location",   ema:0, viti:0},
      {k:"menuOffer",  ema:0, viti:0},
      {k:"menuChoice", ema:0, viti:0},
      {k:"service",    ema:0, viti:0},
      {k:"bill",       ema:0, viti:0}
    ]},
    { kind:"beach", name:"NOME SPIAGGIA", rows:[
      {k:"road",       ema:0, viti:0},
      {k:"sea",        ema:0, viti:0},
      {k:"landscape",  ema:0, viti:0},
      {k:"people",     ema:0, viti:0},
      {k:"facilities", ema:0, viti:0}
    ]}
  ]
}
```

Ricordate la **virgola** tra un giorno e l'altro.
La barra dei giorni, le medie e le statistiche si aggiornano da sole: non c'è
nient'altro da toccare.

**Voti con la virgola** si scrivono con il punto: `7.75`, non `7,75`.

**Se non c'è il diario** di quel giorno, scrivete `journal: null`.

### Le etichette dei voti

Le sigle (`location`, `road`, `sea`…) sono definite poco sopra, in `const L`.
Le potete usare tutte, in qualsiasi ordine. Per aggiungerne una nuova, basta
aggiungerla lì:

```js
tramonto: {it:"Tramonto", en:"Sunset"},
```

e poi usarla: `{k:"tramonto", ema:9, viti:10}`.

### Un commento sul posto

Un pensiero breve su tutta la scheda (ristorante o spiaggia), che compare in un
riquadro colorato sotto ai voti:

```js
{ kind:"beach", name:"Nome", rows:[ ... ],
  comment:{it:"Due righe in prima persona.", en:"A line or two, first person."}
}
```

### Una nota su un singolo voto

```js
{k:"road", ema:7, viti:7, note:{it:"strada bellissima", en:"gorgeous road"}},
```

### Una scheda libera (gelateria, museo, gita…)

Senza voti, solo testo:

```js
{ kind:"treat",
  label:{it:"Pausa gelato", en:"Gelato break"},
  name:"Nome del posto",
  body:{it:"Il racconto.", en:"The story."},
  foot:{it:"Nota piccola facoltativa.", en:"Optional small note."}
}
```

---

## Aggiungere le foto

1. Nel repository, entrate in `assets/photos/` → **Add file → Upload files** →
   caricate le foto (nomi tipo `giorno14-1.jpg`) → **Commit changes**.
2. In `index.html`, nel giorno giusto, scrivete:

```js
photos: [
  {src:"assets/photos/giorno14-1.jpg", cap:{it:"Didascalia", en:"Caption"}},
  {src:"assets/photos/giorno14-2.jpg", cap:{it:"Un'altra", en:"Another one"}}
],
```

Le foto si dispongono da sole: una sola occupa tutta la larghezza, due stanno
affiancate, tre mettono la prima in grande. Cliccandole si aprono a tutto
schermo (frecce ← → per scorrerle, Esc per chiudere).

Se un giorno non ha foto, lasciate `photos: []` e la galleria semplicemente non
compare.

> Consiglio: prima di caricarle, ridimensionate le foto a circa 2000 px di lato
> lungo, così il sito resta veloce anche da telefono.

---

## Aggiungere un nuovo viaggio

Sempre in `const TRIPS`, aggiungete un blocco accanto a quello della Croazia:

```js
{
  id: "grecia-2027",                                  // finisce nell'indirizzo
  cover: "assets/photos/grecia-cover.jpg",            // foto di copertina
  coverAlt: {it:"Descrizione foto", en:"Photo description"},
  title: {it:"Grecia",       en:"Greece"},
  place: {it:"Isola di Naxos", en:"Island of Naxos"},
  dates: {it:"1 – 8 luglio 2027", en:"1 – 8 July 2027"},
  lede:  {it:"Frase di presentazione.", en:"Intro line."},
  days: [ ... ]
}
```

Comparirà da solo nella home. L'indirizzo diretto sarà
`.../diario-croazia/#/it/grecia-2027`.

---

## Indirizzi utili

| Pagina | Indirizzo |
|---|---|
| Home (italiano) | `#/it` |
| Home (inglese) | `#/en` |
| Viaggio Croazia | `#/it/croazia-2026` |
| Viaggio Croazia in inglese | `#/en/croazia-2026` |

---

## Struttura dei file

```
diario-vis/
├── index.html          → tutto il sito: contenuti, stile, funzionamento
├── README.md           → questo file
├── fonts/              → i tre font, inclusi nel repository
└── assets/photos/      → le foto
```

---

## Se qualcosa si rompe

Il file è JavaScript: se sbagliate una virgola o una virgoletta, la pagina resta
bianca. Non è grave — su GitHub andate su **History** (in alto nella pagina del
file), aprite l'ultima versione funzionante e usate **Revert**. Non si perde
niente.
