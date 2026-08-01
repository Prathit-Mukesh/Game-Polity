# MCN Quest — Gamified Polity Trainer

A phone-first, offline-capable revision game built on the MCN (Mains Concise Notes) Indian Polity syllabus.

**87 chapters · 1,061 questions · 261 facts · 11 section tests**

---

## What it does

- **Candy-Crush-style progression** — a winding map of chapter nodes across 11 sections. Each chapter unlocks only when the one before it is cleared; each section unlocks only when the previous section's revision test is passed.
- **8-minute study timer** on the note, with an *I'm ready* button that banks a speed bonus if you start the quiz early.
- **Five questions per chapter, all five must be right.** Retries draw a fresh set from a bank of 10–12, so answers can't be memorised by position.
- **Six UPSC question formats** — statement-based, standard MCQ, assertion–reason, match the following, odd-one-out, and chronological sequencing.
- **Three trivia facts** after each clear, collected permanently into the Fact Vault.
- **Section revision tests** — 15 questions mixed across the section plus cross-chapter synthesis, 12 minutes, 80% to pass.
- **Weak Deck** — every missed question enters a Leitner spaced-repetition deck (boxes at 0, 1, 3 and 7 days; four clean recalls retires it).
- **Search** across every case name, article and keyword in all 87 notes.
- **Hearts, XP, ranks, stars, badges and a daily-streak calendar.**
- **Six interface colours** (including a full light mode) and **six backgrounds** (including an animated aurora).
- Progress is saved to `localStorage` with an export/import backup code.

---

## Deploying to Vercel

1. Push this folder to a GitHub repository.
2. In Vercel, **Add New → Project**, import the repo.
3. Framework preset: **Other**. Leave the build command and output directory **empty** — this is a static site with no build step.
4. Deploy.

`vercel.json` sets JSON caching for the content folders; `.vercelignore` keeps the source PDFs and the older reader out of the deployment.

To run it locally you need a static server (the app fetches JSON, so `file://` will not work):

```bash
npx serve .
```

Then open the printed address.

---

## Installing it as a phone app

Open the deployed URL on your phone.

- **Android / Chrome** — ⋮ menu → *Install app* (or *Add to Home screen*).
- **iPhone / Safari** — Share → *Add to Home Screen*.

It then launches full-screen with no browser chrome, using `manifest.webmanifest` and the bundled icons. Progress lives on that device; use **Copy backup** in Stats to move it to another phone.

---

## Files

```
index.html                  the app (deployable entry point)
MCN Quest.dc.html           the same app as an editable design component
support.js                  component runtime
manifest.webmanifest        PWA manifest
icon-192.png / icon-512.png app icons
vercel.json                 caching headers
_ds/industry-…/             Industry design system (stylesheet + bundle)
notes/mcn01–87.json         the note content, one file per chapter
quest/q01–q87.json          question banks and trivia facts, one file per chapter
quest/s1–s11.json           section-test synthesis banks
quest/index.json            prebuilt search index
MCN 2.0 Study Site.dc.html  the earlier plain reader, linked from Stats
```

`index.html` is a copy of `MCN Quest.dc.html`. Edit the `.dc.html`, then copy it over `index.html` before deploying.

---

## Content model

Every chapter's questions live in `quest/qNN.json`:

```jsonc
{
  "num": "01",
  "title": "Govt of India Act, 1935",
  "facts": [ { "t": "headline", "d": "the fact" } ],   // exactly 3
  "bank": [
    { "k": "mcq",   "q": "...", "o": ["a","b","c","d"], "a": 1, "e": "why", "d": 2 },
    { "k": "stmt",  "q": "...", "s": ["s1","s2","s3"], "o": [...], "a": 1, "e": "...", "d": 2 },
    { "k": "not",   "q": "...", "o": [...], "a": 2, "e": "...", "d": 3 },
    { "k": "ar",    "as": "assertion", "rs": "reason", "a": 0, "e": "...", "d": 2 },
    { "k": "match", "q": "...", "pairs": [["A. x","1. y"]], "o": [...], "a": 0, "e": "...", "d": 3 },
    { "k": "order", "q": "...", "items": [...], "seq": [1,3,0,2], "e": "...", "d": 2 }
  ]
}
```

`a` is the index of the correct option, `e` the explanation shown after answering, `d` the difficulty from 1 to 3. For `order`, `seq` lists the indices of `items` in correct order.

To add or edit questions, change the JSON — no code changes are needed. To add a chapter to a section, extend that section's range in the `WORLDS` array inside the app.
