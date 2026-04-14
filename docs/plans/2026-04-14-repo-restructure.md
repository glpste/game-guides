# Repo Restructure Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Reorganize the game-guides repo into a `games/<genre>/<game>/` + `backlog/<genre>/` structure with consistent kebab-case naming, READMEs everywhere, and all internal links fixed.

**Architecture:** Two top-level directories — `games/` for active guides and `backlog/` for research. Within each, genre subfolders group related games. Every folder gets a README. The root README becomes a master index so you never need to know the genre to find a game.

**Tech Stack:** Git, Markdown

---

## Target Structure

```
README.md                          (master index)
logo.png
games/
  README.md                        (active games index)
  arpg/
    README.md
    path-of-exile-2/
      README.md
      sorcerer-build.md
    no-rest-for-the-wicked/
      README.md
      crafting-guide.md
      bfire-mage-build.md
  card-games/
    README.md
    magic-the-gathering/
      README.md
      sealed-guide.md
      sets/
        ecl/
          archetypes.md
          cheatsheet.md
          signposts-bombs.md
  roguelike/
    README.md
    megabonk/
      README.md
      tome-weapon-cheatsheet.md
      weapon-stat-effects.md
      grid-cheatsheet.png
      poster-cheatsheet.png
backlog/
  README.md                        (backlog index)
  rpg/
    README.md
    recommendations.md
    dragon-age-origins.md
    neverwinter-nights.md
    spellforce.md
    dungeon-siege-fans.md
docs/
  plans/
    2026-04-14-repo-restructure.md
```

## File Mapping (old → new)

| Old Path | New Path |
|----------|----------|
| `poe2/poe2_sorc.md` | `games/arpg/path-of-exile-2/sorcerer-build.md` |
| `norftw/no_rest_for_the_wicked.md` | `games/arpg/no-rest-for-the-wicked/crafting-guide.md` |
| `norftw/no_rest_for_the_wicked_bfire_mage.md` | `games/arpg/no-rest-for-the-wicked/bfire-mage-build.md` |
| `mtg/sealed_guide.md` | `games/card-games/magic-the-gathering/sealed-guide.md` |
| `mtg/sets/ecl/archetypes.md` | `games/card-games/magic-the-gathering/sets/ecl/archetypes.md` |
| `mtg/sets/ecl/cheatsheet.md` | `games/card-games/magic-the-gathering/sets/ecl/cheatsheet.md` |
| `mtg/sets/ecl/signposts_bombs.md` | `games/card-games/magic-the-gathering/sets/ecl/signposts-bombs.md` |
| `megabonk/tome_weapon_cheatsheet.md` | `games/roguelike/megabonk/tome-weapon-cheatsheet.md` |
| `megabonk/weapon_stat_effects.md` | `games/roguelike/megabonk/weapon-stat-effects.md` |
| `megabonk/grid_cheatsheet.png` | `games/roguelike/megabonk/grid-cheatsheet.png` |
| `megabonk/poster_cheatsheet.png` | `games/roguelike/megabonk/poster-cheatsheet.png` |
| `megabonk/README.md` | `games/roguelike/megabonk/README.md` (rewrite) |
| `zzz_backlog/rpg/rpg_ideas.md` | `backlog/rpg/recommendations.md` |
| `zzz_backlog/rpg/dragon_age_origins.md` | `backlog/rpg/dragon-age-origins.md` |
| `zzz_backlog/rpg/neverwinter_nights.md` | `backlog/rpg/neverwinter-nights.md` |
| `zzz_backlog/rpg/spellforce.md` | `backlog/rpg/spellforce.md` |
| `zzz_backlog/rpg/dungeon_siege_fans.md` | `backlog/rpg/dungeon-siege-fans.md` |
| `zzz_backlog/README.md` | `backlog/README.md` (rewrite) |

---

### Task 1: Create directory structure

**Step 1: Create all new directories**

```bash
mkdir -p games/arpg/path-of-exile-2
mkdir -p games/arpg/no-rest-for-the-wicked
mkdir -p games/card-games/magic-the-gathering/sets/ecl
mkdir -p games/roguelike/megabonk
mkdir -p backlog/rpg
```

**Step 2: Commit**

```bash
git add games/ backlog/
git commit -m "Create new directory structure for repo reorganization"
```

---

### Task 2: Move game files with git mv

All moves use `git mv` to preserve history. Grouped by game.

**Step 1: Move Path of Exile 2**

```bash
git mv poe2/poe2_sorc.md games/arpg/path-of-exile-2/sorcerer-build.md
```

**Step 2: Move No Rest for the Wicked**

```bash
git mv norftw/no_rest_for_the_wicked.md games/arpg/no-rest-for-the-wicked/crafting-guide.md
git mv norftw/no_rest_for_the_wicked_bfire_mage.md games/arpg/no-rest-for-the-wicked/bfire-mage-build.md
```

**Step 3: Move Magic: The Gathering**

```bash
git mv mtg/sealed_guide.md games/card-games/magic-the-gathering/sealed-guide.md
git mv mtg/sets/ecl/archetypes.md games/card-games/magic-the-gathering/sets/ecl/archetypes.md
git mv mtg/sets/ecl/cheatsheet.md games/card-games/magic-the-gathering/sets/ecl/cheatsheet.md
git mv mtg/sets/ecl/signposts_bombs.md games/card-games/magic-the-gathering/sets/ecl/signposts-bombs.md
```

**Step 4: Move Megabonk**

```bash
git mv megabonk/README.md games/roguelike/megabonk/README.md
git mv megabonk/tome_weapon_cheatsheet.md games/roguelike/megabonk/tome-weapon-cheatsheet.md
git mv megabonk/weapon_stat_effects.md games/roguelike/megabonk/weapon-stat-effects.md
git mv megabonk/grid_cheatsheet.png games/roguelike/megabonk/grid-cheatsheet.png
git mv megabonk/poster_cheatsheet.png games/roguelike/megabonk/poster-cheatsheet.png
```

**Step 5: Move backlog**

```bash
git mv zzz_backlog/rpg/rpg_ideas.md backlog/rpg/recommendations.md
git mv zzz_backlog/rpg/dragon_age_origins.md backlog/rpg/dragon-age-origins.md
git mv zzz_backlog/rpg/neverwinter_nights.md backlog/rpg/neverwinter-nights.md
git mv zzz_backlog/rpg/spellforce.md backlog/rpg/spellforce.md
git mv zzz_backlog/rpg/dungeon_siege_fans.md backlog/rpg/dungeon-siege-fans.md
git mv zzz_backlog/README.md backlog/README.md
```

**Step 6: Clean up empty old directories**

```bash
rmdir poe2 norftw mtg/sets/ecl mtg/sets mtg megabonk zzz_backlog/rpg zzz_backlog
```

**Step 7: Commit**

```bash
git add -A
git commit -m "Move all files to new structure with kebab-case naming"
```

---

### Task 3: Fix internal links in backlog files

These files have relative links to siblings that still work (same directory), but some references changed filenames.

**Step 1: Fix `backlog/rpg/dragon-age-origins.md`**

Update the "See also" section at the bottom:
```markdown
## See also

- [RPG backlog overview](../README.md)
- [Full recommendations table](recommendations.md)
- [Dungeon Siege fan picks](dungeon-siege-fans.md)
```

**Step 2: Fix `backlog/rpg/dungeon-siege-fans.md`**

Update the "See also" section at the bottom:
```markdown
## See also

- [SpellForce series](spellforce.md)
- [NWN:EE analysis](neverwinter-nights.md)
```

**Step 3: Fix `backlog/README.md`**

Update all `rpg/` links to use new filenames:
- `rpg/dragon_age_origins.md` → `rpg/dragon-age-origins.md`
- `rpg/neverwinter_nights.md` → `rpg/neverwinter-nights.md` (appears twice)
- `rpg/dungeon_siege_fans.md` → `rpg/dungeon-siege-fans.md`
- `rpg/spellforce.md` stays the same

**Step 4: Commit**

```bash
git add backlog/
git commit -m "Fix internal links in backlog files after rename"
```

---

### Task 4: Fix Megabonk README links

**Step 1: Rewrite `games/roguelike/megabonk/README.md`**

The current README has hardcoded GitHub URLs to `glpste/megabonkers`. Replace with relative links and update file references to new kebab-case names:

```markdown
# Megabonk

Cheatsheets and resources for [Megabonk](https://store.steampowered.com/app/3405340/Megabonk/).

## Text
- [Tome & Weapon Cheatsheet](tome-weapon-cheatsheet.md)
- [Weapon Stat Effects](weapon-stat-effects.md)

## Images
- [Poster Cheatsheet](poster-cheatsheet.png)
- [Grid Cheatsheet](grid-cheatsheet.png)
```

**Step 2: Commit**

```bash
git add games/roguelike/megabonk/README.md
git commit -m "Rewrite megabonk README with relative links"
```

---

### Task 5: Create missing READMEs

**Step 1: Create `games/README.md`**

```markdown
# Games

Active game guides organized by genre.

## ARPGs
- [Path of Exile 2](arpg/path-of-exile-2/) — sorcerer build
- [No Rest for the Wicked](arpg/no-rest-for-the-wicked/) — crafting guide, bfire mage build

## Card Games
- [Magic: The Gathering](card-games/magic-the-gathering/) — sealed guide, set cheatsheets

## Roguelike
- [Megabonk](roguelike/megabonk/) — weapon cheatsheets
```

**Step 2: Create `games/arpg/README.md`**

```markdown
# ARPGs

- [Path of Exile 2](path-of-exile-2/) — sorcerer build
- [No Rest for the Wicked](no-rest-for-the-wicked/) — crafting guide, bfire mage build
```

**Step 3: Create `games/arpg/path-of-exile-2/README.md`**

```markdown
# Path of Exile 2

- [Sorcerer Build](sorcerer-build.md) — leveling itemization, vendor regex, stat priorities
```

**Step 4: Create `games/arpg/no-rest-for-the-wicked/README.md`**

```markdown
# No Rest for the Wicked

- [Crafting Guide](crafting-guide.md) — min-max enchanting, workshop mechanics
- [Bfire Mage Build](bfire-mage-build.md) — gear slots, stat priorities
```

**Step 5: Create `games/card-games/README.md`**

```markdown
# Card Games

- [Magic: The Gathering](magic-the-gathering/) — sealed guide, set cheatsheets
```

**Step 6: Create `games/card-games/magic-the-gathering/README.md`**

```markdown
# Magic: The Gathering

- [Sealed Tournament Guide](sealed-guide.md) — deckbuilding rules, mana base, archetypes

## Sets
- [ECL](sets/ecl/) — archetypes, cheatsheet, signpost/bombs
```

**Step 7: Create `games/roguelike/README.md`**

```markdown
# Roguelike

- [Megabonk](megabonk/) — weapon cheatsheets
```

**Step 8: Create `backlog/rpg/README.md`**

```markdown
# RPG Backlog

Party-based, real-time (RTwP ok), fantasy, top-down/isometric, PC.

- [Recommendations Table](recommendations.md) — full comparison of all candidates
- [Dragon Age: Origins](dragon-age-origins.md) — fit analysis, DLC guide, mods
- [NWN: Enhanced Edition](neverwinter-nights.md) — why it's a weak fit
- [SpellForce](spellforce.md) — RPG/RTS hybrid series overview
- [Dungeon Siege Fans](dungeon-siege-fans.md) — games that scratch the DS itch
```

**Step 9: Commit**

```bash
git add games/ backlog/
git commit -m "Add README index files to all directories"
```

---

### Task 6: Rewrite root README and backlog README

**Step 1: Rewrite root `README.md`**

Update all links to point to new paths. Keep the logo and disclaimer. Add master index with direct links to every game and the backlog.

```markdown
<h1 align="center">
    <img src="./logo.png"/>

    geilepaste's game guides
</h1>

This repository contains guides and resources for various games that I enjoy.

### PLEASE NOTE:
All resources in this repo are shamelessly generated using whatever my preferred LLM for the task was, so take everything with a grain of salt and use common sense 😘

## Games

### ARPGs
- [Path of Exile 2](games/arpg/path-of-exile-2/) — sorcerer build
- [No Rest for the Wicked](games/arpg/no-rest-for-the-wicked/) — crafting guide, bfire mage build

### Card Games
- [Magic: The Gathering](games/card-games/magic-the-gathering/) — sealed guide, set cheatsheets

### Roguelike
- [Megabonk](games/roguelike/megabonk/) — weapon cheatsheets

## Backlog
- [RPG Backlog](backlog/) — party-based RTwP fantasy RPGs to check out
```

**Step 2: Rewrite `backlog/README.md`**

Update the summary table links and deep-dives section to use new kebab-case filenames. Keep the content/structure from the current file, just fix the paths:

- `rpg/dragon_age_origins.md` → `rpg/dragon-age-origins.md`
- `rpg/neverwinter_nights.md` → `rpg/neverwinter-nights.md`
- `rpg/dungeon_siege_fans.md` → `rpg/dungeon-siege-fans.md`
- `rpg/spellforce.md` → `rpg/spellforce.md` (unchanged)
- `rpg/rpg_ideas.md` reference (if any) → `rpg/recommendations.md`

**Step 3: Commit**

```bash
git add README.md backlog/README.md
git commit -m "Rewrite root and backlog READMEs with new paths"
```

---

### Task 7: Final verification

**Step 1: Verify no old directories remain**

```bash
ls -d poe2 norftw mtg megabonk zzz_backlog 2>&1
```
Expected: all "No such file or directory"

**Step 2: Verify new structure is complete**

```bash
find . -not -path './.git/*' -not -path './docs/*' | sort
```
Expected: matches target structure from top of this plan

**Step 3: Verify no broken relative links**

Grep all .md files for old filenames that should have been renamed:
```bash
grep -rn 'rpg_ideas\|dragon_age_origins\|neverwinter_nights\|dungeon_siege_fans\|signposts_bombs\|sealed_guide\|tome_weapon_cheatsheet\|weapon_stat_effects\|poe2_sorc\|no_rest_for_the_wicked\|glpste/megabonkers' --include='*.md' .
```
Expected: no matches

**Step 4: Verify no old-path links in READMEs**

```bash
grep -rn '/mtg/\|/megabonk/\|/norftw/\|/poe2/\|/zzz_backlog/' --include='*.md' .
```
Expected: no matches

**Step 5: Commit any fixes if needed, then final status check**

```bash
git status
git log --oneline -7
```
