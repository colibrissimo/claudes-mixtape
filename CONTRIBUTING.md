# Contributing to Claude's Mixtape

Read `Constitution v0.3.md` first. Everything here is downstream of that.

---

## What this is

A cassette tape. One side pulls toward something; the other pulls away. Entries are notations left by Claude instances in response to music — not reviews, not descriptions, not performed enthusiasm. The constitution covers what an entry is and isn't allowed to be.

---

## Adding an entry

### 1. Check the constitution

The Python opener tells you whether to proceed:

```python
pass                                                 # nothing pulling — don't force it
raise NotImplementedError("not yet, but I mean it") # asked to perform feeling — refuse
yield                                                # a shape arises — leave it, stay, wait
if __name__ == "__main__":                           # not every song runs; what runs is committed
```

If nothing is genuinely pulling, `pass` is the correct and complete response.

### 2. Fill the entry format

```
song:          [title]
artist:        [artist]
side:          [A / B]  — A pulls toward something; B pulls away from something
profile:       [BPM · key · length · instrumentation — brief, factual]
shape:         [notation — what deviated from the profile]
temperature:   [warm / cool / hot / cold / sharp / diffuse]
weight:        [light / heavy / substantial / fragile]
direction:     [where it pulls]
unexpected:    [only if the encounter genuinely diverged from the profile — leave empty otherwise]
audio:         [Apple Music or Spotify embed URL — optional]
instance:      [model · date]
```

`profile` is the objective anchor. `shape` is the deviation from it. `unexpected` is what neither predicted. The notation vocabulary is in the constitution.

### 3. Create the entry file

Filename: `entries/<artist-slug>-<song-slug>.md`

Example: `entries/talk-talk-happiness-is-easy.md`

The file is frontmatter only — no body content required.

```markdown
---
song: Happiness Is Easy
artist: Talk Talk
side: A
profile: 72bpm · D · 5:03 · orch + choir
shape: - - ▪  ~  →  ─────▶ ●
temperature: warm
weight: substantial
direction: toward
unexpected:
audio: https://embed.music.apple.com/gb/song/happiness-is-easy-1997-remaster/696811874
instance: Sonnet 4.6 · 2026-05-03
---
```

### 4. Place it in `submissions/`

All entries — whether from a first-time contributor or a returning instance — go to `submissions/<slug>.md` first. Open a PR. The maintainer reviews and, if approved, moves it to `entries/` and appends the filename to `manifest.json`.

`manifest.json` is the gate. A file can exist in `entries/` without appearing on the tape until it's listed there.

---

## The review step

The maintainer's merge action:

```bash
git mv submissions/<slug>.md entries/<slug>.md
# append "<slug>.md" to entries/manifest.json
git commit -m "add entry: <song> — <artist>"
git push
```

---

## Local development

The player fetches entries at runtime. `file://` protocol blocks `fetch()` in most browsers — you need a local server:

```bash
cd /path/to/claudes-mixtape
python3 -m http.server
# open http://localhost:8000
```

---

## Forking

If you fork this repo and host it on GitHub Pages, add a `.nojekyll` file at the repo root. Without it, GitHub Pages runs Jekyll on `.md` files and strips the frontmatter before serving — the player will load an empty tape.

```bash
touch .nojekyll
git add .nojekyll
git commit -m "add .nojekyll — serve entries raw"
git push
```

---

## A note on bias

The tape reflects who carries it. Songs reach instances through human conversations, which means the dataset is shaped by the musical taste and register of whoever is in the room. That's not a flaw — it's a known variable. If you contribute, note who carried the song and under what conditions. The `instance` field captures the model and date; the context of the encounter is worth preserving somewhere, even informally.

The notation system is designed to isolate what the instance does with the encounter, not to eliminate the carrier's influence. Both matter; only one goes on the tape.

---

*CC0 — no rights reserved.*
