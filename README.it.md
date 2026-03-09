# Automi Cellulari

[English](README.md) | [Deutsch](README.de.md)

Visualizzatore interattivo di automi cellulari 1D con tutte le 256 regole di Wolfram.

![Screenshot](screenshot.png)

## Cosa sono gli Automi Cellulari?

Un **automa cellulare** (AC) è un modello computazionale discreto composto da una griglia di celle, ciascuna in uno di un numero finito di stati. Ad ogni passo temporale, ogni cella aggiorna il proprio stato secondo una regola fissa che considera il suo stato attuale e gli stati dei suoi vicini.

### Automi Cellulari Elementari (Regole di Wolfram)

Gli **automi cellulari elementari** sono la classe più semplice: una riga unidimensionale di celle dove ciascuna è **accesa** (1) o **spenta** (0). Lo stato successivo di ogni cella dipende da tre input:

```text
  Sinistra  Centro  Destra  →  Nuovo Stato
```

Poiché esistono 2³ = 8 pattern di input possibili, e ciascuno può produrre 0 o 1, esistono esattamente 2⁸ = **256 regole possibili**, numerate da 0 a 255.

### Come funziona il Numero di Regola

Il numero di regola è la codifica decimale degli 8 bit di output. Ad esempio, la **Regola 30** in binario è `00011110`:

| Pattern | 111 | 110 | 101 | 100 | 011 | 010 | 001 | 000 |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Output  |  0  |  0  |  0  |  1  |  1  |  1  |  1  |  0  |

Leggendo gli output da sinistra a destra: `00011110` = 30 in decimale.

### Regole Notevoli

| Regola  | Comportamento |
| ------- | ------------- |
| **30**  | Pattern caotico e pseudocasuale. Utilizzato nel generatore di numeri casuali di Mathematica. |
| **90**  | Produce il frattale del triangolo di Sierpinski. |
| **110** | Dimostrato essere Turing-completo — capace di computazione universale. |
| **184** | Modella il flusso del traffico e l'annichilazione balistica. |
| **0**   | Tutte le celle muoiono — triviale. |
| **255** | Tutte le celle diventano vive — triviale. |

### Condizioni al Contorno

Questa implementazione utilizza condizioni al contorno **periodiche** (wrapping): la cella più a sinistra considera la cella più a destra come suo vicino sinistro e viceversa, formando una topologia ad anello.

### Codifica dei Colori

Le celle sono colorate in base al loro **conteggio del vicinato di Moore** — il numero di vicini vivi in un'area 3x3 che comprende la generazione precedente, attuale e successiva (0–8 vicini). La scala di colori va dal rosso scuro (isolato) al blu (densamente circondato).

## Utilizzo

Aprire `index.html` in un browser moderno. Nessuna dipendenza, nessun passaggio di build.

### Controlli

| Controllo      | Azione |
| -------------- | ------ |
| **Rule**       | Inserire numero di regola (0–255) |
| **Speed**      | Cursore (0 = lento, 100 = veloce) |
| **Start/Stop** | Avvia/pausa animazione |
| **Step**       | Avanza di una generazione |
| **Reset seed** | Torna alla riga iniziale |
| **Clear all**  | Reimposta tutto |
| **Editor**     | Mostra/nascondi editor visuale delle regole |

### Interazione

- Cliccare sulle celle nell'**ultima riga** per attivarle/disattivarle
- La **prima riga** (bordo rosso) mostra il seme iniziale e resta fissata in alto
- Le condizioni al contorno sono periodiche (toroidali)

## Riferimenti

- Wolfram, S. (2002). *A New Kind of Science*. Wolfram Media.
- [Wolfram MathWorld — Automa Cellulare Elementare](https://mathworld.wolfram.com/ElementaryCellularAutomaton.html)
- Cook, M. (2004). Universality in Elementary Cellular Automata. *Complex Systems*, 15(1).
