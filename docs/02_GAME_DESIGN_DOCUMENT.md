# 📜 Game Design Document — Antiquaria

> **GDD v1.1** — approved by Creative Director after 14-expert Cycle 2 review (11/14 clean, 3 approved-with-notes, 4 required changes applied).

## 1. High-concept

You are **Elspeth Marlowe**, summoned from a respectable but dull cataloguing job at the British Museum to take over your great-aunt Marguerite's curio shop in 1890s Edinburgh's Old Town. Marguerite has vanished without a will. The shop is overstocked with strange objects. Customers begin to arrive — some bringing treasures, others bringing trouble. Authenticate, refuse, or investigate. Your reputation in the antiquarian community is the score.

**Player fantasy:** *I am the curious antiquarian who can read the secret history of objects.*

**Emotional journey:** Bewilderment (overstocked shop) → competence (first authentication) → curiosity (Marguerite's notes) → conviction (taking a stance against the Black Auction) → revelation (the Curator's Atlas).

**Pillars (do not violate):**
1. **The pinboard is the game** — all deduction is visible and tactile.
2. **Provenance is a real puzzle, not a guess** — every authenticated case has exactly one logically correct verdict.
3. **Customers are characters, not transactions** — recurring relationships shape the world.
4. **Cozy framing, real stakes** — the pace stays warm; wrong calls have lasting reputation cost but never punish the player out of the game.
5. **Audio carries atmosphere** — ticking clock, creaking floor, rain on window. Never silent.

## 2. Core game loop

`Morning open shop → Customer arrives with object → Examine (magnifier) → Research (archive shelf) → Pin clues → Compare with ledger → Authenticate / refuse / refer → Reputation updates → Day ends at dusk → New ledger entry unlocks → Next morning`

## 3. Player verbs

| Verb | Input | Notes |
|---|---|---|
| Inspect close | Click object | Smooth zoom to inspection view |
| Magnify | Hold RMB and move | Reveals hidden marks, hallmarks, foxing, tool-marks |
| Open book | Click archive shelf | One book at a time; pages flip with arrow keys |
| Pin clue | Drag from clue-tray onto pinboard | Snaps to nearest column |
| Connect | Drag from pin to pin | Draws red string |
| Annotate | Double-click string | Add a one-line note (player text input) |
| Greet customer | Click customer | Opens branching dialogue (`DialogueNodeSO`) |
| Authenticate / Refuse / Refer | Three buttons in counter UI | Locks the verdict; updates ledger |
| Ask for hint | Click bell on counter | Costs 1 hint coin |
| End day | Click clock at dusk | Saves; cinematic sundown |

## 4. Progression

| System | M1 reveal | Late-game ceiling |
|---|---|---|
| Reputation (per faction) | 1 of 3 factions | 3 factions @ ±100 each |
| Books in archive | 2 (one open) | 18 books (each unlocks a category) |
| Authentication tools | Magnifier | + UV lamp + chemical test + provenance ledger lookup |
| Hint coins | 3 | 10 max (earned from clean weeks) |
| Customers known | 1 | 22 (with relationship arcs) |
| Marguerite's letters found | 1 (intro) | 14 (one per Act + hidden) |
| Pinboard columns | 1 | 4 (cases / customers / factions / Marguerite) |

## 5. Mission structure — 6 Acts (~10–14h main)

| Act | Title | Duration | New mechanic | Case difficulty |
|---|---|---|---|---|
| **1** | *Day One* | 2–3 h | Magnifier, single column pinboard, 1 faction | ◐◯◯◯◯ |
| 2 | *The Gentleman's Trust* | 2 h | UV lamp, faction reputation | ◐◐◯◯◯ |
| 3 | *The Provenance Society* | 2 h | Multi-customer concurrent cases | ◐◐◐◯◯ |
| 4 | *The Black Auction* | 2 h | Moral choice: forge or refuse | ◐◐◐◐◯ |
| 5 | *The Cursed Letter* | 2 h | Marguerite mystery primary | ◐◐◐◐◐ |
| 6 | *The Curator's Atlas* | 2–3 h | All systems converge; finale | ◐◐◐◐◐ |

Difficulty curve was a Cycle 2 required change (Yusuf + Layla). Acts 4–6 introduce *no new mechanics* — only deeper application of existing ones. Prevents late-game frustration.

## 6. Mission 1 — *Day One* (scene-by-scene)

**Goal:** Onboard the player into examination, pinboard, ledger, and customer trust. **Duration:** 2–3 h (player-paced).

**Cinematic moment (Marcus's Cycle 2 ask):** the *first lit lamp* — Elspeth strikes a match, the gaslight catches, the title card fades in. One held frame. The trailer's opening shot.

**Flow:**
1. **Cottage Above the Shop** — letter from Marguerite's solicitor; player reads; gas lamp scene.
2. **The Shop, Dust Sheets On** — player removes 3 dust sheets via click. Counter and pinboard are revealed.
3. **First Customer — Mr. Halloway** — a polite gentleman with a pocket watch. He wants to know if it's genuine 1820s Breguet. Easy case (one hidden hallmark, one date stamp).
4. **Examination** — tutorial spotlights the magnifier and the archive. The player finds the hallmark, looks up the year, makes the call.
5. **Verdict** — *Authenticate*. Halloway thanks her, leaves a small tip, and asks if she'd be willing to look at "something else, next week." (Hook for Act 2.)
6. **Second Customer — Mrs. Dunne** — brings a locket. The case has a twist: it's beautiful, but the inscription doesn't match the era. The right call is *Refer to specialist* (Mrs. Dunne should keep it but not as a verified antique). Teaches that Refuse / Refer are not failure states.
7. **Dusk** — Elspeth opens Marguerite's first letter, recovered from a drawer. Plants the season-mystery.

**Objectives (in MissionDataSO):**
- `m1_read_letter` (1)
- `m1_remove_sheets` (3)
- `m1_examine_watch` (1)
- `m1_find_hallmark` (1)
- `m1_lookup_breguet` (1)
- `m1_authenticate_watch` (1, correct verdict)
- `m1_examine_locket` (1)
- `m1_refer_locket` (1, correct verdict — *refer* not *authenticate*)
- `m1_optional_drawer_letter` (1, optional — Marguerite hook)

**Checkpoints:** Auto-save after each customer + at dusk.

## 7. Hint coin system (Cycle 2 required change — Layla)

Every stuck player has a soft escape: ring the bell on the counter. The first hint nudges; the second points; the third effectively solves. Each hint costs **1 hint coin**. Player starts each Act with 3 coins; unused coins persist; clean week earns +1 bonus coin. No real-money purchase; no shame.

## 8. Customer / faction system

3 factions emerge across Acts: **The Royal Society of Antiquaries** (orthodox), **The Provenance Society** (collegial), **The Black Auction** (gray-market). Each customer is aligned to one. Verdicts shift reputation ±5 per faction. Reputation gates Act-final customers and Marguerite-mystery doors.

22 named customers; each appears in 2–4 Acts; relationship is one-line greeting variants.

## 9. Economy

- **Coin** — earned per correct verdict + tips. Spent on archive books, tool upgrades, and shop décor (cosmetic).
- **Reputation** — per faction (see §8).
- **Hint coins** — see §7.
- **Marguerite's letters** — 14 total; collectible.

## 10. UI

| Screen | Asset |
|---|---|
| Main menu | Heat UI custom skin (parchment + ink) |
| HUD | Bamao with parchment overlay |
| Pinboard | Custom Unity 2D drag-drop with red-string line renderer |
| Archive book | Pixel Crushers + custom page-flip shader |
| Dialogue | Pixel Crushers Dialogue System rendered with portrait panel |
| Counter UI | Three-button verdict + bell-for-hint |

## 11. Accessibility (Cycle 2 required change — Priya)

- Text size XL, OpenDyslexic font option.
- Colourblind clue palette (red-string → numbered + dashed alternatives).
- Subtitle opacity slider.
- Pinboard "snap-to-grid" for fine motor.
- Hold-to-toggle for magnifier RMB.
- Audio cue for every visual reveal (hallmark found = chime).
- One-handed control layout.

## 12. Audio (Hiroshi)

A bespoke audio identity is the single biggest perception multiplier in this game. **Commission a composer** for 5 tracks: piano + cello + lightly-bowed double-bass + ambient room tone. **Diegetic SFX** are 80% of the experience — ticking clock, creaking floor, rain on window, gaslight hum, page turn, magnifier glass, red-string tension. Game UI & Puzzle SFX Pack supplies the rest.

## 13. Visual identity (Elena)

Hand-drawn pen-and-ink with watercolor washes. Reference boards: Edward Gorey (line work), Beatrix Potter (color softness), Brian Selznick (page composition). Palette: bone, sepia, gas-flame amber, faded oxblood. **Single illustrator commission** for portraits + objects + environments keeps style coherent.

## 14. Cut-list (if scope slips)

1. UV lamp (defer to Act 3, never beyond).
2. Chemical test mini-game (cut entirely — described in lore but not played).
3. 4 of 22 customers (collapse 22 → 18).
4. Multiplayer pinboard sharing (was a stretch; cut).
5. Switch port (defer to post-launch).

**Never cut:** Magnifier, pinboard, Mr. Halloway, the first lit lamp.

✅ **Approved by Creative Director + 14-expert Cycle 2 (with 4 required changes applied).**
