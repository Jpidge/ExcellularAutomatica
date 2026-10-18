# Excellular Automatica

**A cellular automata lab where Excel logic becomes a computer.**

An interactive lab that proves you can build a full calculator — adder, subtractor, multiplier, divider — using only `=AND()`, `=OR()`, `=NOT()` in Excel. No math, just automaton logic. Then wraps it in a 1970s red VFD calculator.

Live: https://jpidge.github.io/ExcellularAutomatica/

## What's Inside

This is a single self-contained `index.html` — no backend, no dependencies, runs in any browser. Five labs in one:

### 1. 1D Elementary Automata
30 rules including Rule 110 (Turing-complete). Adjustable steps, random seed, single-cell start.

### 2. 2D Game of Life
Conway's Life with editable board, speed control, classic patterns.

### 3. Excel Logic Layer
The bridge: Shows how Rule 110 is built from 5 AND gates → 1 OR gate in pure Excel formulas:
```
=IF(OR(AND(L=1,C=1,R=0),AND(L=1,C=0,R=1),AND(L=0,C=1,R=1),AND(L=0,C=1,R=0),AND(L=0,C=0,R=1)),1,0)
```
5 ANDs = universal computer.

### 4. ALU Calculator
An 8-bit Arithmetic Logic Unit built from the same gates, with a clock you can step:
- **ADD:** Ripple-carry, 8 Full Adders chained. `Cout = OR(AND(A,B), AND(Cin, XOR))`
- **SUB:** Two's complement — `A - B = A + NOT(B) + 1` via NOT gates + adder
- **MUL:** Shift-and-add. `Partial = AND(A, B_i)`, 8 clock ticks
- **DIV:** Restoring division, 8 ticks
- **Bin ↔ Dec Converter:** Shows binary switches → decimal via adder logic. `Dec = Σ(bit_i * 2^i)` where `*` is AND, `+` is adder.
- **Clock:** Step / Run / Reset — carry ripples one bit per tick, just like CA generations.

### 5. Vintage VFD Calculator
A skeuomorphic 1970s desktop calculator with glowing red 7-segment VFD (`#ff2222` bloom), amber binary LEDs, chunky keys, and a red rocker power switch.

Power-on sequence: 60Hz hum + relay thunk + cathode warm-up flicker. All math still runs on the AND/OR logic underneath.

## Excel Files

- `Cellular_Automata_Logic_Gates.xlsx` — Rule 30/90/110 as pure logic, logic gate truth tables
- `8Bit_Adder_Automaton_Logic.xlsx` — 8-bit ripple-carry adder built from `AND/OR/NOT` only, with decimal check and Full Adder truth table

Core gate library used everywhere:
```
XOR(A,B) = OR(AND(A,NOT B), AND(NOT A,B))
Sum      = XOR(XOR(A,B), Cin)
Cout     = OR(AND(A,B), AND(Cin, XOR(A,B)))
```

## Why This Exists

Cellular automata like Rule 110 can build logic gates. Logic gates can build an adder. An adder can build an ALU. An ALU is a computer. Therefore, a cellular automaton — and an Excel sheet full of `=AND()` — is Turing-complete.

This repo is that proof you can click.

## Run Locally

```bash
git clone https://github.com/Jpidge/ExcellularAutomatica.git
# Just open it
open index.html
```

## Deploy

It's static. For GitHub Pages:
Settings → Pages → Deploy from branch → main / (root)

Or drag to Netlify Drop.

## Stack

Vanilla JS + React (CDN) + Canvas for CA rendering. No build step.

Built with Meta AI for John Page — Sioux Falls, SD.
