# Schedule Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a password-protected schedule page with presenter assignments, update the public site with themed block labels, and produce an MD overview for email communication.

**Architecture:** Static HTML encrypted with StatiCrypt. Source stays in gitignored `local_dont_commit_to_branch/`. Encrypted output committed to `website/`. No CI changes.

**Tech Stack:** HTML, CSS (existing `style.css`), StatiCrypt (npx), Markdown

---

### Task 1: Create the schedule source HTML

**Files:**
- Create: `local_dont_commit_to_branch/organization/schedule-source.html`

- [ ] **Step 1: Create the unencrypted schedule page**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Schedule — VITVI R&D Workshop 2026</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

<!-- Nav -->
<nav>
  <div class="container">
    <a href="index.html" class="logo"><span class="prompt">&gt;</span> <span class="logo-text">vitvi_workshop</span><span class="cursor cursor--hidden"></span></a>
    <button class="menu-toggle" aria-label="Menu" onclick="document.querySelector('.nav-links').classList.toggle('open')">&#9776;</button>
    <ul class="nav-links">
      <li><a href="index.html#about">About</a></li>
      <li><a href="index.html#format">Format</a></li>
      <li><a href="index.html#schedule">Schedule</a></li>
    </ul>
  </div>
</nav>

<main class="container" style="padding-top:6rem;padding-bottom:4rem;">
  <span class="label">Detailed Schedule</span>
  <h1>Presenter Assignments</h1>
  <p style="color:var(--text-2);margin-bottom:2.5rem;">VITVI R&D Workshop — May 6&ndash;7, 2026, Klosterhotel Lehnin</p>

  <!-- Day 1 -->
  <div class="schedule-day">
    <h3>Day 1 — Laying the Groundwork</h3>

    <div class="schedule-item">
      <div class="schedule-time">10:00</div>
      <div class="schedule-content">
        <strong>Welcome &amp; Intro</strong>
        <p>Coffee, settling in, and setting the "Radical Candor" ground rules.</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">10:30</div>
      <div class="schedule-content">
        <strong>Impulse Talk 1: Academia</strong>
        <p><em>Robert Flassig</em> (TH Brandenburg)</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">11:00 – 12:30</div>
      <div class="schedule-content">
        <strong>PhD Block 1: Root Cause &amp; Explainability</strong>
        <table style="width:100%;margin-top:.5rem;">
          <thead><tr><th style="text-align:left;">Time</th><th style="text-align:left;">Presenter</th><th style="text-align:left;">Track</th><th style="text-align:left;">Topic</th></tr></thead>
          <tbody>
            <tr><td>11:00</td><td>Klaus Markgraf (THB)</td><td>TBD</td><td>XAI / BIFI</td></tr>
            <tr><td>11:30</td><td>Nedim Kovacevic (TU Berlin)</td><td>Problem Pitch</td><td>ML for vibration analysis, XAI</td></tr>
            <tr><td>12:00</td><td>Alexander K&ouml;hler (BTU)</td><td>TBD</td><td>PCA</td></tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">12:30 – 14:00</div>
      <div class="schedule-content">
        <strong>Lunch &amp; Hotel Check-in</strong>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">14:00</div>
      <div class="schedule-content">
        <strong>Impulse Talk 2: Startup</strong>
        <p><em>Dr. Stefan Harries</em> (FRIENDSHIP SYSTEMS)</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">14:30 – 16:00</div>
      <div class="schedule-content">
        <strong>PhD Block 2: Design Optimization &amp; Structures</strong>
        <table style="width:100%;margin-top:.5rem;">
          <thead><tr><th style="text-align:left;">Time</th><th style="text-align:left;">Presenter</th><th style="text-align:left;">Track</th><th style="text-align:left;">Topic</th></tr></thead>
          <tbody>
            <tr><td>14:30</td><td>Hamun Bertram (THB)</td><td>Breakthrough Pitch</td><td>ML aeromechanical optimization</td></tr>
            <tr><td>15:00</td><td>Clara Henkel (BTU)</td><td>TBD</td><td>ML fan-blisk design optimization</td></tr>
            <tr><td>15:30</td><td>Akshatha Ramesh Patkar (BTU)</td><td>Problem Pitch</td><td>ML for Structural Health Monitoring</td></tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">16:00 – 16:30</div>
      <div class="schedule-content">
        <strong>Coffee Break</strong>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">16:30 – 17:30</div>
      <div class="schedule-content">
        <strong>Open Discussions</strong>
        <p>Unstructured time for 1-on-1s, whiteboarding, or catching up.</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">18:30+</div>
      <div class="schedule-content">
        <strong>Workshop Dinner</strong>
        <p>Casual networking. No formal agenda.</p>
      </div>
    </div>
  </div>

  <!-- Day 2 -->
  <div class="schedule-day">
    <h3>Day 2 — Deep Dives &amp; Synthesis</h3>

    <div class="schedule-item">
      <div class="schedule-time">09:00</div>
      <div class="schedule-content">
        <strong>Impulse Talk 3: Industry</strong>
        <p><em>Peter Flassig</em> (Rolls-Royce Deutschland)</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">09:30 – 11:00</div>
      <div class="schedule-content">
        <strong>PhD Block 3: Physics &amp; Icing</strong>
        <table style="width:100%;margin-top:.5rem;">
          <thead><tr><th style="text-align:left;">Time</th><th style="text-align:left;">Presenter</th><th style="text-align:left;">Track</th><th style="text-align:left;">Topic</th></tr></thead>
          <tbody>
            <tr><td>09:30</td><td>Ravishankar Selvaraj (BTU)</td><td>Problem Pitch</td><td>Particle interaction with hot surfaces</td></tr>
            <tr><td>10:00</td><td>Zishan Naveed (BTU)</td><td>Problem Pitch</td><td>TBD</td></tr>
            <tr><td>10:30</td><td>Timm Gehrhardt (THB)</td><td>TBD</td><td>Icing</td></tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">11:00 – 11:30</div>
      <div class="schedule-content">
        <strong>Coffee Break</strong>
        <p>Room checkout for those who need it.</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">11:30</div>
      <div class="schedule-content">
        <strong>Impulse Talk 4: Deep Dive</strong>
        <p><em>Speaker TBD</em></p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">12:00 – 13:30</div>
      <div class="schedule-content">
        <strong>PhD Block 4: Data-Driven Methods &amp; Process</strong>
        <table style="width:100%;margin-top:.5rem;">
          <thead><tr><th style="text-align:left;">Time</th><th style="text-align:left;">Presenter</th><th style="text-align:left;">Track</th><th style="text-align:left;">Topic</th></tr></thead>
          <tbody>
            <tr><td>12:00</td><td>Dongsuk Kim (BTU)</td><td>Breakthrough Pitch</td><td>TBD</td></tr>
            <tr><td>12:30</td><td>Abhishek Dhiman (BTU)</td><td>Problem Pitch</td><td>Incremental ML, data compression, VR</td></tr>
            <tr><td>13:00</td><td>Iman Sonji (TU Berlin)</td><td>TBD</td><td>Knowledge graphs, OOB/vibration</td></tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">13:30 – 14:30</div>
      <div class="schedule-content">
        <strong>Lunch</strong>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">14:30 – 15:30</div>
      <div class="schedule-content">
        <strong>The Synthesis Session</strong>
        <p>Group discussion: recurring roadblocks, new methods, and collaboration opportunities.</p>
      </div>
    </div>

    <div class="schedule-item">
      <div class="schedule-time">15:30 – 16:00</div>
      <div class="schedule-content">
        <strong>Wrap-up &amp; Departure</strong>
        <p>Safe travels home!</p>
      </div>
    </div>
  </div>
</main>

<footer>
  <div class="container">
    <p>
      VITVI R&D Workshop 2026 &middot;
      Built by <strong>Robert Flassig</strong> &middot;
      <a href="legal.html">Legal Notice</a> &middot;
      <a href="privacy.html">Privacy Policy</a>
    </p>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Verify the file renders locally**

Run: Open `local_dont_commit_to_branch/organization/schedule-source.html` in browser.
Expected: Page renders with dark theme, tables show presenter names and times.

---

### Task 2: Create the MD overview file

**Files:**
- Create: `local_dont_commit_to_branch/organization/schedule-overview.md`

- [ ] **Step 1: Write the MD overview**

```markdown
# VITVI R&D Workshop 2026 — Schedule Overview

**May 6–7, 2026 · Klosterhotel Lehnin, Brandenburg**

Online schedule (password-protected): https://batmanvane.github.io/VITVI_RD_Workshop/schedule.html
Password: `<TO BE SET>`

---

## Impulse Talks

| Slot | Time | Speaker | Affiliation | Theme |
|------|------|---------|-------------|-------|
| 1 | Day 1, 10:30 | Robert Flassig | TH Brandenburg | Academia |
| 2 | Day 1, 14:00 | Dr. Stefan Harries | FRIENDSHIP SYSTEMS | Startup |
| 3 | Day 2, 09:00 | Peter Flassig | Rolls-Royce Deutschland | Industry |
| 4 | Day 2, 11:30 | *TBD* | — | Deep Dive |

---

## Day 1 — May 6, 2026

### Block 1 (11:00–12:30): Root Cause & Explainability

| Time | Presenter | Affiliation | Track | Topic |
|------|-----------|-------------|-------|-------|
| 11:00 | Klaus Markgraf | THB | TBD | XAI / BIFI |
| 11:30 | Nedim Kovacevic | TU Berlin | Problem Pitch | ML for vibration analysis, XAI |
| 12:00 | Alexander Köhler | BTU | TBD | PCA |

### Block 2 (14:30–16:00): Design Optimization & Structures

| Time | Presenter | Affiliation | Track | Topic |
|------|-----------|-------------|-------|-------|
| 14:30 | Hamun Bertram | THB | Breakthrough Pitch | ML aeromechanical optimization |
| 15:00 | Clara Henkel | BTU | TBD | ML fan-blisk design optimization |
| 15:30 | Akshatha Ramesh Patkar | BTU | Problem Pitch | ML for Structural Health Monitoring |

---

## Day 2 — May 7, 2026

### Block 3 (09:30–11:00): Physics & Icing

| Time | Presenter | Affiliation | Track | Topic |
|------|-----------|-------------|-------|-------|
| 09:30 | Ravishankar Selvaraj | BTU | Problem Pitch | Particle interaction with hot surfaces |
| 10:00 | Zishan Naveed | BTU | Problem Pitch | TBD |
| 10:30 | Timm Gehrhardt | THB | TBD | Icing |

### Block 4 (12:00–13:30): Data-Driven Methods & Process

| Time | Presenter | Affiliation | Track | Topic |
|------|-----------|-------------|-------|-------|
| 12:00 | Dongsuk Kim | BTU | Breakthrough Pitch | TBD |
| 12:30 | Abhishek Dhiman | BTU | Problem Pitch | Incremental ML, data compression, VR |
| 13:00 | Iman Sonji | TU Berlin | TBD | Knowledge graphs, OOB/vibration |

---

## Reminders

- **Book your hotel room** at Klosterhotel Lehnin with keyword "VITVI" for 15% off (105 EUR/night incl. breakfast): https://www.diakonissenhaus.de/klosterhotel-lehnin
- **Presenters marked TBD:** Please confirm your track — Problem Pitch (roadblock) or Breakthrough Pitch (finding) — by replying to this email.
- **Dongsuk Kim & Zishan Naveed:** Please share your presentation topic.

---

## Full Timetable

| Time | Day 1 (May 6) | Day 2 (May 7) |
|------|---------------|---------------|
| 09:00 | — | Impulse Talk 3: Industry |
| 09:30–11:00 | — | PhD Block 3: Physics & Icing |
| 10:00 | Welcome & Intro | — |
| 10:30 | Impulse Talk 1: Academia | — |
| 11:00–11:30 | — | Coffee Break |
| 11:00–12:30 | PhD Block 1: Root Cause & Explainability | — |
| 11:30 | — | Impulse Talk 4: Deep Dive |
| 12:00–13:30 | — | PhD Block 4: Data-Driven Methods & Process |
| 12:30–14:00 | Lunch & Hotel Check-in | — |
| 13:30–14:30 | — | Lunch |
| 14:00 | Impulse Talk 2: Startup | — |
| 14:30–15:30 | — | Synthesis Session |
| 14:30–16:00 | PhD Block 2: Design Optimization & Structures | — |
| 15:30–16:00 | — | Wrap-up & Departure |
| 16:00–16:30 | Coffee Break | — |
| 16:30–17:30 | Open Discussions | — |
| 18:30+ | Workshop Dinner | — |
```

- [ ] **Step 2: Commit is not needed** — file is in gitignored directory.

---

### Task 3: Update `index.html` schedule section

**Files:**
- Modify: `website/index.html:469-495` (Block 1 and Block 2 descriptions)
- Modify: `website/index.html:530-553` (Block 3 and Block 4 descriptions)
- Add: link to protected schedule page after schedule section heading

- [ ] **Step 1: Update Block 1 description**

Replace line 472-474:
```html
        <div class="schedule-content">
          <strong>PhD Sessions — Block 1</strong>
          <p>3 PhD students: 10 min pitch + 20 min group session each (Problem Pitches &amp; Breakthrough Pitches).</p>
```
With:
```html
        <div class="schedule-content">
          <strong>PhD Block 1: Root Cause &amp; Explainability</strong>
          <p>3 pitches exploring XAI, feature importance, and data-driven diagnostics.</p>
```

- [ ] **Step 2: Update Block 2 description**

Replace line 492-494:
```html
        <div class="schedule-content">
          <strong>PhD Sessions — Block 2</strong>
          <p>3 PhD students: 10 min pitch + 20 min group session each (Problem Pitches &amp; Breakthrough Pitches).</p>
```
With:
```html
        <div class="schedule-content">
          <strong>PhD Block 2: Design Optimization &amp; Structures</strong>
          <p>3 pitches on ML-driven blade design, multi-objective optimization, and structural monitoring.</p>
```

- [ ] **Step 3: Update Block 3 description**

Replace line 532-534:
```html
        <div class="schedule-content">
          <strong>PhD Sessions — Block 3</strong>
          <p>3 PhD students: 10 min pitch + 20 min group session each (Problem Pitches &amp; Breakthrough Pitches).</p>
```
With:
```html
        <div class="schedule-content">
          <strong>PhD Block 3: Physics &amp; Icing</strong>
          <p>3 pitches on particle dynamics, surface interactions, and ice accretion simulation.</p>
```

- [ ] **Step 4: Update Block 4 description**

Replace line 552-554:
```html
        <div class="schedule-content">
          <strong>PhD Sessions — Block 4</strong>
          <p>3 PhD students: final batch of pitches.</p>
```
With:
```html
        <div class="schedule-content">
          <strong>PhD Block 4: Data-Driven Methods &amp; Process</strong>
          <p>3 pitches on incremental learning, knowledge graphs, and data-driven process modeling.</p>
```

- [ ] **Step 5: Add link to protected schedule after the heading**

After line 450 (`<h2>Two Days of Deep Work</h2>`), insert:
```html
    <p style="margin-bottom:1.5rem;"><a href="schedule.html" class="btn btn-secondary" style="font-size:.8rem;padding:.4rem .8rem;">View full schedule with presenters &rarr;</a></p>
```

- [ ] **Step 6: Verify locally**

Open `website/index.html` in browser. Confirm:
- Block labels show themed names
- Link to schedule.html appears
- No presenter names visible on public page

- [ ] **Step 7: Commit**

```bash
git add website/index.html
git commit -m "Update schedule with themed block labels and link to detailed page"
```

---

### Task 4: Encrypt with StatiCrypt

- [ ] **Step 1: Install StatiCrypt (if not present)**

Run: `npx staticrypt --help`
Expected: StatiCrypt help output. If prompted to install, accept.

- [ ] **Step 2: Choose password and encrypt**

Run:
```bash
npx staticrypt \
  local_dont_commit_to_branch/organization/schedule-source.html \
  -p "<PASSWORD>" \
  -o website/schedule.html \
  --title "VITVI Workshop Schedule" \
  --remember 30
```

Replace `<PASSWORD>` with the chosen password.
Expected: `website/schedule.html` is created (encrypted).

- [ ] **Step 3: Test the encrypted page**

Open `website/schedule.html` in browser.
Expected: Password prompt appears. Entering correct password reveals the full schedule.

- [ ] **Step 4: Commit**

```bash
git add website/schedule.html
git commit -m "Add password-protected schedule page (StatiCrypt)"
```

---

### Task 5: Update README.md

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Add section after "Registration Backend"**

Insert before the "Forking this for your own workshop" section:

```markdown
## Protected Schedule Page

The detailed schedule (with presenter names) is password-protected using
[StatiCrypt](https://github.com/robinmoisson/staticrypt). The encryption
happens client-side — the HTML file contains AES-encrypted content that
decrypts in the browser when the correct password is entered.

**Source file:** `local_dont_commit_to_branch/organization/schedule-source.html` (gitignored)

**To update the schedule:**

1. Edit the source HTML file
2. Encrypt and output to the website directory:
   ```bash
   npx staticrypt \
     local_dont_commit_to_branch/organization/schedule-source.html \
     -p "<password>" \
     -o website/schedule.html \
     --title "VITVI Workshop Schedule" \
     --remember 30
   ```
3. Commit and push `website/schedule.html`

The `--remember 30` flag stores the password in the visitor's browser for 30 days.
```

- [ ] **Step 2: Update the file tree in README**

Add `schedule.html` to the website tree listing:
```
website/
├── index.html          # Landing page (schedule, format, examples)
├── register.html       # Registration form with domain whitelist
├── schedule.html       # Encrypted schedule page (StatiCrypt)
├── legal.html          # Legal notice (German TMG)
├── privacy.html        # Privacy policy (GDPR)
├── config.example.js   # Template for form endpoint config
└── css/
    └── style.css       # Dark minimal theme
```

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "Document StatiCrypt workflow for protected schedule page"
```

---

### Task 6: Update .gitignore (if needed)

**Files:**
- Modify: `.gitignore`

- [ ] **Step 1: Verify `local_dont_commit_to_branch/` is already gitignored**

Check `.gitignore` for `local_dont_commit_to_branch/`.
Expected: Already present (confirmed from earlier reading).

- [ ] **Step 2: No action needed** — directory is already gitignored.
