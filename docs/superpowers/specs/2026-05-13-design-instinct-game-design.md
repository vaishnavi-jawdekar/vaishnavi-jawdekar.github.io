# Design Instinct — Hidden Game

**Portfolio:** vaishnavi-portfolio (`index.html`)
**Date:** 2026-05-13

---

## What it is

A hidden easter egg game embedded in the portfolio. Long-pressing the passport reveals a 6-question rapid taste quiz. No right answers. At the end: one of 4 designer archetypes, based purely on aesthetic instinct.

Goals:
- **Feels clever** — reward for finding it, not a test
- **Reveals something** — acts as a mirror, not a scorecard
- **Works on mobile and desktop** — no keyboard required

---

## Trigger

**Long-press the passport for 2 seconds.**

- Implemented via `pointerdown` + timeout (700ms feels right, 2000ms is too long)
- A subtle progress ring or fill animation on the passport signals "keep holding"
- On release before threshold: nothing happens
- On threshold: game modal opens with entrance animation
- Works identically on mobile (touch) and desktop (mouse)

---

## Game flow

```
Long-press passport
  → Intro screen ("You found it.")
  → Q1 of 6
  → Q2 of 6
  → ...
  → Q6 of 6
  → Result screen (archetype)
```

---

## UI mechanic

- **Modal overlay** — dark backdrop with blur, slides up on open, dismissible with ✕ or Escape
- **Progress bar** — 6 dots at the top, fills left to right
- **Each question:** prompt text + two side-by-side visual cards
- **Tap/click either card** → advances instantly, no confirm button
- **No back button** — instinct, not deliberation
- **Result screen** — archetype name, 2-line description, trait tags

---

## The 6 questions

Each question is a binary visual choice. Questions 1–3 score the **Minimal ↔ Rich** axis. Questions 4–6 score the **Structured ↔ Expressive** axis.

| # | Prompt | A (left) | B (right) | Axis |
|---|--------|----------|-----------|------|
| 1 | Pick an art movement. | Bauhaus — geometry, primary colours, function | Memphis — clashing colour, squiggles, chaos | Minimal ↔ Rich |
| 2 | Which room would you live in? | Minimal Japanese — one perfect object, stillness | Floor-to-ceiling bookshelves, plants everywhere | Minimal ↔ Rich |
| 3 | Pick a city at night. | Copenhagen — cobblestones, amber light, quiet | Tokyo — neon, dense, electric | Minimal ↔ Rich |
| 4 | Pick a decade to design in. | 70s — warm tones, analog texture, handcrafted | 90s — digital grids, early web, system fonts | Structured ↔ Expressive |
| 5 | Pick a poster. | Swiss International — grid, Helvetica, red block | Psychedelic — layered, glowing, no rules | Structured ↔ Expressive |
| 6 | Pick a texture. | Graph paper — precise, ordered, gridded | Linen — warm, organic, imperfect | Structured ↔ Expressive |

**Scoring:** A = 0 points, B = 1 point. Sum Q1–3 for axis 1 (0–3), sum Q4–6 for axis 2 (0–3). Threshold at 2: ≥2 = Rich / Expressive, <2 = Minimal / Structured.

---

## The 4 archetypes

| Name | Axis 1 | Axis 2 | Description |
|------|--------|--------|-------------|
| **The Surgeon** | Minimal | Structured | Cuts everything that doesn't belong. Precision over decoration. Your work is clean because you know exactly what to remove. |
| **The Poet** | Minimal | Expressive | Makes space do the work. Restraint is your superpower — what you leave out says more than what you put in. |
| **The Architect** | Rich | Structured | Builds systems that hold. Every detail earns its place. Your designs feel considered because they are. |
| **The Collector** | Rich | Expressive | Finds beauty in abundance. Texture, warmth, detail — you believe design should feel lived-in and full of life. |

---

## Visual design

Light mode, arcade-esque. Feels like a hidden mini-game that lives inside the portfolio world — not a separate dark universe. Pixelated touches, chunky borders, retro energy — but still clean and on-brand.

- **Modal backdrop:** `rgba(10,10,10,0.5)` + `backdrop-filter: blur(8px)`
- **Modal card:** `#F7F7F5` background, `border: 3px solid #0A0A0A`, chunky `border-radius: 12px`, slight drop shadow — feels like an arcade cabinet screen
- **Typography:** mix of Satoshi (body) + monospace for scores/labels — gives a retro readout feel
- **Question cards:** thick black borders, flat colour fills, bold labels — like arcade selection tiles
- **Selected state:** fat `3px solid #4B4EFC` border + a slight scale up — satisfying tap feedback
- **Progress:** 6 chunky square dots (not pills) — like lives or level indicators in a game
- **Result screen:** big bold archetype name, pixel-adjacent styling, a "PLAY AGAIN" button
- **Transitions:** snappy — cards snap in rather than fade. Fast feel, not floaty.

---

## Implementation notes

- Lives entirely in `index.html` — no new files
- Long-press: `pointerdown` starts a `setTimeout(700)`. `pointerup` / `pointermove` (beyond threshold) cancels it. Visual feedback via CSS animation on the passport scene.
- Scoring: `answers` array of 6 booleans. At end, `axis1 = answers.slice(0,3).filter(Boolean).length`, `axis2 = answers.slice(3).filter(Boolean).length`. Map to archetype.
- Modal state: a single `game-modal` div with `.open` class, same pattern as the book suggestion modal already in the page.
- Question visuals: CSS-only (same approach as the brainstorm mockups — shapes, gradients, SVG inline).
