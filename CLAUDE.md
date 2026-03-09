# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive 1D cellular automaton visualizer (Wolfram rules 0–255). Single-file app: `index.html` — no build step, no dependencies.

## Running

Open `index.html` in a browser (`open index.html` on macOS).

## Architecture

Single HTML file with inline CSS and JS. Key sections:

- **CSS** (lines 7–315): Dark theme using Tailwind-inspired slate palette (`#0f172a`, `#1e293b`, `#334155`). Fullscreen flex layout: header → controls → optional rule editor → canvas → info bar.
- **Canvas rendering** (JS): Grid of `cellSize=12` px cells. First row (seed) is always pinned at top with red highlight; remaining generations scroll below. Cells colored by Moore neighborhood count (8 neighbors across prev/current/next generation) using a red-to-blue 9-stop palette.
- **CA engine**: `rules` object maps 3-bit patterns (e.g. `"010"`) to 0/1 output. `nextGeneration()` computes next row with wrapping boundary conditions.
- **Rule editor**: Togglable 8-pattern visual editor; clicking a pattern flips its output bit and recomputes the rule number.
- **Cell editing**: Only the last (bottom) visible generation row is click-editable.

## Design Conventions

- Dark theme: backgrounds `#0f172a`/`#1e293b`, text `#e2e8f0`/`#cbd5e1`, accent `#60a5fa`
- Compact UI: 11px fonts, minimal padding, all controls in one row
- Speed slider 0–100 maps linearly to delay: `delay = 100 - speed * 0.9` (0=10fps slowest, 100=fastest)
- Color palette array is duplicated in `getColorByNeighbors()` and `generateLegend()` — keep them in sync
