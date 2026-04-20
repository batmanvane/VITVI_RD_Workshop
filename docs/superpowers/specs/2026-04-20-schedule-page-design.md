# Design: Password-Protected Schedule Page & Presenter Assignment

**Date:** 2026-04-20
**Status:** Approved

## Summary

Create a detailed schedule page showing presenter assignments (names, topics, time slots) protected by StatiCrypt encryption. Update the public site with thematic block labels but no names. Produce an MD overview file for email communication with registrants.

## Decisions

- **Access control:** StatiCrypt (client-side AES encryption)
- **Source privacy:** Unencrypted source stays in `local_dont_commit_to_branch/` (gitignored, never in repo history)
- **CI:** No workflow changes needed — encrypted output committed directly to `website/`
- **Public site:** Show block themes, no names, link to protected page
- **MD file:** Local organizational file for email use

## Presenter Assignment

### Impulse Talks

| Slot | Speaker | Affiliation | Theme |
|------|---------|-------------|-------|
| Day 1, 10:30 | Robert Flassig | THB | Academia |
| Day 1, 14:00 | Dr. Stefan Harries | FRIENDSHIP SYSTEMS | Startup |
| Day 2, 09:00 | Peter Flassig | Rolls-Royce | Industry |
| Day 2, 11:30 | *open* | — | Deep Dive |

### PhD Pitches

**Block 1 (Day 1, 11:00–12:30): Root Cause & Explainability**

| # | Name | Affiliation | Track | Topic |
|---|------|-------------|-------|-------|
| 1 | Klaus Markgraf | THB | TBD | XAI / BIFI |
| 2 | Nedim Kovacevic | TU Berlin | Problem Pitch | ML for vibration, XAI |
| 3 | Alexander Köhler | BTU | TBD | PCA |

**Block 2 (Day 1, 14:30–16:00): Design Optimization & Structures**

| # | Name | Affiliation | Track | Topic |
|---|------|-------------|-------|-------|
| 4 | Hamun Bertram | THB | Breakthrough | ML aeromechanical optimization |
| 5 | Clara Henkel | BTU | TBD | ML fan-blisk design optimization |
| 6 | Akshatha Ramesh Patkar | BTU | Problem Pitch | ML for Structural Health Monitoring |

**Block 3 (Day 2, 09:30–11:00): Physics & Icing**

| # | Name | Affiliation | Track | Topic |
|---|------|-------------|-------|-------|
| 7 | Ravishankar Selvaraj | BTU | Problem Pitch | Particle interaction / hot surfaces |
| 8 | Zishan Naveed | BTU | Problem Pitch | *(topic TBD)* |
| 9 | Timm Gehrhardt | THB | TBD | Icing |

*Constraint: Naveed is Day 2 only.*

**Block 4 (Day 2, 12:00–13:30): Data-Driven Methods & Process**

| # | Name | Affiliation | Track | Topic |
|---|------|-------------|-------|-------|
| 10 | Dongsuk Kim | BTU | Breakthrough | *(topic TBD)* |
| 11 | Abhishek Dhiman | BTU | Problem Pitch | Incremental ML, data compression, VR |
| 12 | Iman Sonji | TU Berlin | TBD | Knowledge graphs, OOB/vibration |

*Constraint: Sonji requested Day 2.*

### Excluded from pitches

- **Katja Müller** (THB, Fan Icing) — excluded per organizer decision

## File Structure

```
local_dont_commit_to_branch/
  organization/
    schedule-source.html         # unencrypted HTML with full schedule (gitignored)
    schedule-overview.md         # MD overview for email communication

website/
  index.html                     # updated: block themes, no names, link to schedule.html
  schedule.html                  # StatiCrypt-encrypted output (committed)
```

## Implementation Details

### 1. Protected schedule page (`schedule-source.html`)

- Reuses `website/css/style.css` for consistent look
- Shows full timetable: impulse talks + all 4 PhD blocks with names, affiliations, tracks, topics
- Same nav as main site, linking back to `index.html`
- No registration form or interactive elements

### 2. StatiCrypt encryption

Encrypt locally and commit the output:

```bash
npx staticrypt local_dont_commit_to_branch/organization/schedule-source.html \
  -p "<password>" \
  -o website/schedule.html \
  --title "VITVI Workshop Schedule" \
  --remember 30
```

`--remember 30` caches the password in the visitor's browser for 30 days.

### 3. Public `index.html` updates

Replace the generic "3 PhD students" block descriptions with themed labels:

- Block 1: "Root Cause & Explainability"
- Block 2: "Design Optimization & Structures"
- Block 3: "Physics & Icing"
- Block 4: "Data-Driven Methods & Process"

Add a link/button below or within the schedule section:
> "View full schedule with presenters" → `schedule.html`

Keep all other schedule content (times, impulse talk labels, logistics) as-is.

### 4. README.md update

Add a section documenting the encrypt workflow:

```markdown
## Updating the Protected Schedule Page

The detailed schedule (with presenter names) is password-protected using
[StatiCrypt](https://github.com/robinmoisson/staticrypt).

The unencrypted source lives in `local_dont_commit_to_branch/organization/schedule-source.html`
(gitignored — never committed).

To update:

1. Edit the source file
2. Encrypt and output to the website directory:
   ```bash
   npx staticrypt local_dont_commit_to_branch/organization/schedule-source.html \
     -p "<password>" \
     -o website/schedule.html \
     --title "VITVI Workshop Schedule" \
     --remember 30
   ```
3. Commit and push `website/schedule.html`
```

### 5. MD overview file (`schedule-overview.md`)

Contains:
- Full schedule (same content as the HTML page)
- Password for the protected web page
- Reminder to book hotel room (keyword "VITVI")
- Note for "maybe" presenters to confirm their track choice (Problem or Breakthrough)
- Note for presenters with unknown topics (Kim, Naveed) to share their topic

## Open Items

- [ ] Impulse Talk 4 (Deep Dive) — no speaker assigned
- [ ] Dongsuk Kim — topic unknown
- [ ] Zishan Naveed — topic unknown
- [ ] Akshatha Ramesh Patkar — registered as "Masters Student", confirm this is fine
- [ ] Choose a password for StatiCrypt
- [ ] 6 "maybe" presenters need to confirm track (Problem or Breakthrough)
