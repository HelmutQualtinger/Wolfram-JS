# Cellular Automata

[Deutsch](README.de.md) | [Italiano](README.it.md)

Interactive 1D cellular automaton visualizer implementing all 256 Wolfram rules.

![Screenshot](screenshot.png)

<img src="Stephen-Wolfram-1.jpg" alt="Stephen Wolfram" width="150" align="right" style="border-radius: 50%; margin-left: 20px;">

## What are Cellular Automata?

A **cellular automaton** (CA) is a discrete computational model consisting of a grid of cells, each in one of a finite number of states. At each time step, every cell updates its state based on a fixed rule that considers its current state and the states of its neighbors.

### Elementary Cellular Automata (Wolfram Rules)

**Elementary cellular automata** are the simplest class: a one-dimensional row of cells where each cell is either **on** (1) or **off** (0). Each cell's next state depends on three inputs:

```
  Left  Center  Right  →  New State
```

Since there are 2³ = 8 possible input patterns, and each can produce 0 or 1, there are exactly 2⁸ = **256 possible rules**, numbered 0–255.

### How the Rule Number Works

The rule number is the decimal encoding of the 8 output bits. For example, **Rule 30** in binary is `00011110`:

| Pattern | 111 | 110 | 101 | 100 | 011 | 010 | 001 | 000 |
|---------|-----|-----|-----|-----|-----|-----|-----|-----|
| Output  |  0  |  0  |  0  |  1  |  1  |  1  |  1  |  0  |

Reading the outputs left to right: `00011110` = 30 in decimal.

### Notable Rules

| Rule | Behavior |
|------|----------|
| **30** | Chaotic, pseudo-random pattern. Used in Mathematica's random number generator. |
| **90** | Produces the Sierpinski triangle fractal. |
| **110** | Proven to be Turing-complete — capable of universal computation. |
| **184** | Models traffic flow and ballistic annihilation. |
| **0** | All cells die — trivial. |
| **255** | All cells become alive — trivial. |

### Boundary Conditions

This implementation uses **wrapping** (periodic) boundaries: the leftmost cell treats the rightmost cell as its left neighbor and vice versa, forming a ring topology.

### Color Coding

Cells are colored by their **Moore neighborhood count** — the number of alive neighbors in a 3x3 area spanning the previous, current, and next generation (0–8 neighbors). The color scale goes from dark red (isolated) to blue (densely surrounded).

## Usage

Open `index.html` in any modern browser. No dependencies, no build step.

### Controls

| Control | Action |
|---------|--------|
| **Rule** | Enter rule number (0–255) |
| **Speed** | Drag slider (0 = slow, 100 = fast) |
| **Start/Stop** | Run/pause animation |
| **Step** | Advance one generation |
| **Reset seed** | Return to initial seed row |
| **Clear all** | Reset everything |
| **Editor** | Toggle visual rule editor |

### Interaction

- Click cells in the **bottom row** to set/unset them
- The **top row** (red border) shows the initial seed and stays pinned
- Boundary conditions wrap around (toroidal)

## References

- Wolfram, S. (2002). *A New Kind of Science*. Wolfram Media.
- [Wolfram MathWorld — Elementary Cellular Automaton](https://mathworld.wolfram.com/ElementaryCellularAutomaton.html)
- Cook, M. (2004). Universality in Elementary Cellular Automata. *Complex Systems*, 15(1).
