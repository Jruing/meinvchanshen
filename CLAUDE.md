# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

"美女缠身" (Meinv Chanshan) — a classic Henan poker drinking card game. Players take turns drawing cards and placing them on table cards. The relationship between the drawn card and target card determines drink penalties.

## Architecture

**Single-file application.** All HTML, CSS, and JavaScript live in `index.html` (~1189 lines):
- Lines 1–663: CSS (dark theme, card rendering, animations, responsive layout)
- Lines 664–815: HTML (setup screen, game board with 3-column grid, modals)
- Lines 816–1188: JavaScript (game logic, state management, DOM manipulation)

No frameworks, no dependencies, no build step. Vanilla HTML/CSS/JS only.

## How to Run

Open `index.html` directly in a browser. No server or build process required.

## Game State & Flow

All state lives in a single `gameState` object. The game has two phases:
- **`draw` phase**: player clicks the deck to draw a card
- **`place` phase**: player clicks a table card to place the drawn card on

Key functions: `createDeck()`, `shuffleDeck()`, `startGame()`, `drawCard()`, `placeCard(tableIndex)`, `checkRelation(card1, card2)`, `nextPlayer()`, `updateUI()`.

## Core Game Rules (checkRelation logic)

- Same rank or Joker pairing → 4 drinks
- Same suit + sequential (rank diff ≤ 2) → 3 drinks
- Same suit, non-sequential → 2 drinks
- Different suit + sequential (rank diff ≤ 2) → 1 drink
- No relationship → pass (0 drinks)

Ace = 1, King = 13. No wrap-around (K→A is not sequential). Jokers always trigger 4 drinks against any card.

## UI Notes

- All text is in Simplified Chinese
- Responsive: 3-column layout above 900px, single-column below
- Drawn cards display face-down ("?") until placed for gameplay suspense
- `database.sqlite` and `index.zip` are unused artifacts
