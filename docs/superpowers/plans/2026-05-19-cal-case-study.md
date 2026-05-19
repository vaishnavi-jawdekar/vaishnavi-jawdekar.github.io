# Cal Case Study Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a Cal case study section to `index.html` between `#work` and `#about`, using a parallel two-column narrative layout with screenshots, inline CSS, and the portfolio's existing design tokens.

**Architecture:** Single-file portfolio — all HTML, CSS, and JS live in `index.html`. The new `#cal` section follows the same container/section pattern as existing sections. No new files except screenshots dropped into the project root. Reveal animations reuse the existing IntersectionObserver already wired up in the page.

**Tech Stack:** HTML/CSS inline in `index.html` · Satoshi + DM Serif Display (already loaded) · existing `.reveal` / `.reveal.in` animation system

---

## File Map

| File | Action | Purpose |
|------|--------|---------|
| `index.html` | Modify | Add `#cal` CSS block + HTML section |
| `cal-add-food.png` | Create (drop in root) | Screenshot of Add Food screen |
| `cal-today.png` | Create (drop in root) | Screenshot of Today view with logged meal |

---

## Task 1: Add Cal section CSS to `index.html`

**Files:**
- Modify: `index.html` — add CSS inside the existing `<style>` block, after the `/* ─── WORK ───` block

- [ ] **Step 1: Find the insertion point for CSS**

Search for this line in `index.html`:
```
/* ─── ABOUT ───
```
The new CSS block goes immediately before this comment.

- [ ] **Step 2: Insert the Cal CSS block**

Add this block before the `/* ─── ABOUT ───` comment:

```css
/* ─── CAL CASE STUDY ─────────────────────────────── */
#cal { background: var(--bg); }

.cal-header {
  margin-bottom: 4rem;
}
.cal-title {
  font-family: 'Satoshi', sans-serif;
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  color: var(--ink);
  letter-spacing: -0.02em;
  margin-bottom: 0.75rem;
  line-height: 1;
}
.cal-tagline {
  font-family: 'DM Serif Display', serif;
  font-style: italic;
  font-size: clamp(1rem, 1.8vw, 1.25rem);
  color: var(--ink);
  margin-bottom: 0.75rem;
  max-width: 600px;
}
.cal-label {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--ink-muted);
}

.cal-body {
  display: grid;
  grid-template-columns: 1fr 1px 1fr;
  gap: 0 3rem;
  margin-bottom: 4rem;
}
.cal-divider {
  background: var(--ink);
  opacity: 0.1;
  align-self: stretch;
}
.cal-col-header {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--ink-muted);
  margin-bottom: 2.5rem;
}

.cal-beat {
  margin-bottom: 3rem;
}
.cal-beat:last-child { margin-bottom: 0; }

.cal-screenshot {
  width: 200px;
  border-radius: 20px;
  box-shadow: 0 8px 32px rgba(10,10,10,0.12);
  display: block;
  margin-bottom: 1.25rem;
}

.cal-beat-text {
  font-family: 'Satoshi', sans-serif;
  font-size: 0.975rem;
  line-height: 1.65;
  color: var(--ink);
}
.cal-beat-personal {
  font-family: 'DM Serif Display', serif;
  font-style: italic;
  font-size: 1.05rem;
  line-height: 1.6;
  color: var(--ink);
  padding-top: 0.25rem;
}
.cal-beat-personal em {
  font-style: normal;
  color: var(--accent);
}

.cal-closing {
  border-top: 1px solid rgba(10,10,10,0.1);
  padding-top: 3rem;
  max-width: 680px;
}
.cal-closing-text {
  font-family: 'Satoshi', sans-serif;
  font-size: 1.05rem;
  line-height: 1.7;
  color: var(--ink);
  margin-bottom: 1rem;
}
.cal-closing-kicker {
  font-family: 'DM Serif Display', serif;
  font-style: italic;
  font-size: 0.975rem;
  color: var(--ink-muted);
}

/* Mobile */
@media (max-width: 768px) {
  .cal-body {
    grid-template-columns: 1fr;
    gap: 0;
  }
  .cal-divider { display: none; }
  .cal-col + .cal-col { margin-top: 2.5rem; }
  .cal-screenshot { width: 160px; }
}
```

- [ ] **Step 3: Verify the CSS was inserted correctly**

Search `index.html` for `.cal-title` — it should exist once and be inside the `<style>` block.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add Cal case study section CSS"
```

---

## Task 2: Add Cal section HTML to `index.html`

**Files:**
- Modify: `index.html` — insert the `#cal` section between `</section>` (end of `#work`) and `<section id="about">`

- [ ] **Step 1: Find the insertion point**

Search for this exact line in `index.html`:
```html
<section id="about">
```
The new HTML goes immediately before this line.

- [ ] **Step 2: Insert the section HTML**

```html
<section id="cal">
  <div class="container">

    <!-- Header -->
    <div class="cal-header reveal">
      <h2 class="cal-title">Cal</h2>
      <p class="cal-tagline">"A calorie counter I built for myself because every other one made me feel bad."</p>
      <span class="cal-label">Side Project · Vibe Coded</span>
    </div>

    <!-- Parallel body -->
    <div class="cal-body reveal">

      <!-- Left: Product -->
      <div class="cal-col">
        <p class="cal-col-header">The Product</p>

        <!-- Beat 1 -->
        <div class="cal-beat">
          <p class="cal-beat-text">Every calorie app I tried had a goal. A deficit. A warning. I didn't want to be managed. I wanted to remember what I ate.</p>
        </div>

        <!-- Beat 2 -->
        <div class="cal-beat">
          <img src="cal-add-food.png" alt="Cal Add Food screen" class="cal-screenshot">
          <p class="cal-beat-text">Cal uses Indian portion units — katori, vati — because that's how I actually think about food. There's no calorie goal, no streak, no warning if you go over. The empty state reads "You haven't eaten yet&nbsp;:)" — not a nudge, just a fact.</p>
        </div>

        <!-- Beat 3 -->
        <div class="cal-beat">
          <img src="cal-today.png" alt="Cal Today view" class="cal-screenshot">
          <p class="cal-beat-text">Cal uses the Gemini API to look up calories automatically. Type a food name and quantity, it returns a number. No database to maintain, no manual lookup.</p>
        </div>
      </div>

      <!-- Divider -->
      <div class="cal-divider"></div>

      <!-- Right: Personal -->
      <div class="cal-col">
        <p class="cal-col-header">What Was Actually Happening</p>

        <!-- Beat 1 -->
        <div class="cal-beat">
          <p class="cal-beat-personal">I had never written a line of code. I opened Claude and typed: <em>build me a calorie tracking app.</em></p>
        </div>

        <!-- Beat 2 -->
        <div class="cal-beat">
          <p class="cal-beat-personal">I didn't realise I was making design decisions. I thought I was just telling it what I wanted.</p>
        </div>

        <!-- Beat 3 -->
        <div class="cal-beat">
          <p class="cal-beat-personal">The first time the API worked — <em>1 katori upma → 180 kcal</em> — I actually screamed. That was the moment I understood what building feels like.</p>
        </div>
      </div>

    </div><!-- /.cal-body -->

    <!-- Closing -->
    <div class="cal-closing reveal">
      <p class="cal-closing-text">Cal is just for me. It lives on my phone, it knows my units, it doesn't judge me. Building it taught me that good product thinking and good code come from the same place — knowing exactly who you're designing for.</p>
      <p class="cal-closing-kicker">First API integration. First shipped app. Won't be the last.</p>
    </div>

  </div>
</section>
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Cal case study section HTML"
```

---

## Task 3: Add screenshots

**Files:**
- Create: `cal-add-food.png` in project root
- Create: `cal-today.png` in project root

- [ ] **Step 1: Export screenshots from iPhone**

Take two screenshots from the Cal app on your iPhone:
1. `cal-add-food.png` — the Add Food sheet (ideally with "1 katori upma" typed in)
2. `cal-today.png` — the Today view with at least one meal logged

AirDrop or cable-transfer them to the project root: `/Users/vaishnavijawdekar/Claude_Projects/vaishnavi-portfolio/`

- [ ] **Step 2: Verify files exist**

```bash
ls /Users/vaishnavijawdekar/Claude_Projects/vaishnavi-portfolio/cal-*.png
```
Expected output: two `.png` paths.

- [ ] **Step 3: Commit**

```bash
git add cal-add-food.png cal-today.png
git commit -m "feat: add Cal app screenshots"
```

---

## Task 4: Verify in browser

**Files:**
- No changes — verification only

- [ ] **Step 1: Start the dev server (if not already running)**

```bash
cd /Users/vaishnavijawdekar/Claude_Projects/vaishnavi-portfolio
python3 -m http.server 8743
```

- [ ] **Step 2: Open in browser and check the section**

Use the `/browse` skill to open `http://localhost:8743` and scroll to the Cal section. Verify:
- Header renders: title, tagline, label
- Two columns appear side by side with divider
- Screenshots load (or placeholder space if not yet added)
- Personal column text is in DM Serif italic
- Closing block appears below with border-top
- Resize to mobile: columns stack vertically, divider disappears

- [ ] **Step 3: Check reveal animations**

Scroll past the section and back — `.cal-header`, `.cal-body`, `.cal-closing` should each fade+slide in via `.reveal.in`.

- [ ] **Step 4: Deploy if everything looks good**

```bash
git add .
git commit -m "feat: Cal case study section complete"
git push
```

---

## Self-Review Notes

- **Spec coverage:** Header ✓ · Three beats ✓ · Screenshots ✓ · Closing + kicker ✓ · Placement after #work ✓ · Mobile stacking ✓
- **Placeholders:** None — all CSS values, HTML structure, and copy are explicit
- **Type consistency:** `.cal-beat-personal em` targets the `<em>` inside beat 3 personal copy for accent colour — consistent with how the portfolio uses `var(--accent)` elsewhere
- **CSS variable assumption:** Uses `var(--bg)`, `var(--ink)`, `var(--ink-muted)`, `var(--accent)` — these are defined in the portfolio's `:root` block and are already used throughout `index.html`
