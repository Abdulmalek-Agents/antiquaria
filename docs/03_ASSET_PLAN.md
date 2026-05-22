# 🎨 Asset Plan — Antiquaria

> Net coverage from Inventix existing inventory: **~70%**. Must-buy gap is small.

## 1. Existing inventory used

| Asset | Used for | Critical |
|---|---|---|
| **Pixel Crushers Dialogue System** ($75) | All customer & faction dialogue trees | 🔴 Yes |
| **Bamao Pack Fantasy GUI** ($25) | In-game UI panels (re-skinned to parchment) | 🔴 Yes |
| **Heat Complete Modern UI** ($69.99) | Main menu, settings, results (skinned) | 🔴 Yes |
| **Game UI & Puzzle SFX Pack** ($99) | UI clicks, page turns, chimes, magnifier scratch | 🔴 Yes |
| **Eyes Animator** ($11.99) | Customer portrait eye warmth on close-up | 🟡 Helpful |
| **Cutscene Engine** ($35) | First lit lamp, dusk fades, Act intros, Marguerite letters | 🔴 Yes |
| **Lumen Stylized Light FX 2** ($35) | Gas-lamp glow, candle flicker, fireplace embers | 🟡 Helpful |
| **Hierarchy Designer** ($30) | Editor productivity (organising 6 Acts) | 🟢 Optional |

**Inventory value applied: ~$380.** All packs already owned.

## 2. Gap analysis — must-buy

| Gap | Suggested | Cost |
|---|---|---|
| 2D pen-and-ink environmental atlas | Asset Store "Hand-Drawn Mystery Kit" OR commission key art frames | $25–$120 |
| 22 customer portraits (hand-drawn, 3 expression variants each) | Commission illustrator (Fiverr / Behance / itch) | $400 |
| ~80 unique object/clue illustrations | Commission illustrator (same person — style coherence) | $600 |
| OST (5 tracks: piano + cello + bass + room tone + finale) | Commission composer | $300 |
| Voice acting (~30 short customer lines, optional) | VA hire | $200 |
| Bespoke diegetic SFX (clock, floor, rain, gaslight) | Commission sound designer OR good free packs | $0–150 |

**Must-buy total — Mission 1 only:** **~$60** (just the atlas to render the shop).
**Must-buy total — full game ship:** **~$1,500** (illustrator + composer + VA).

Well within the $25–40k team-budget envelope.

## 3. Visual coherence rule (Elena's Cycle 3 ask)

**One illustrator for portraits + objects + environments.** The single biggest perception multiplier in a hand-drawn 2D game is style coherence. Multiple illustrators = obvious style breaks. Budget for one person at ~$1,000 total over 4 months of part-time work.

## 4. Folder organisation

```
Assets/_Project/
├── Art/{Portraits,Objects,Environments,UI}
├── Audio/{Music,SFX,Ambient,Voice}
├── Materials/
├── Prefabs/{UI,Pinboard,Customer,Object}
├── Scenes/
├── Data/{Acts,Cases,Customers,Books,Verdicts,LineBanks,Hints}
└── Scripts/{Core,Pinboard,Examination,Dialogue,UI,Save}
```

## 5. Performance tweaks

- 2D atlas-packed sprites; one texture per Act-environment.
- Object pool for clue-pins and red-string segments.
- Audio: OGG @ 96kbps for ambient; WAV for short hit-SFX.
- Cutscene Engine timelines pre-compiled per Act, not on-demand.

## 6. Licence audit ✅

Unity Asset Store EULA covers all listed packs (Inventix holds licences). Commissioned art will be work-for-hire with explicit commercial-use buyout. **Asset binaries are NOT redistributed in this repo.**

## 7. Post-purchase checklist

- [ ] Import every Asset Store pack per §1
- [ ] Skin Heat UI + Bamao to parchment palette
- [ ] Commission illustrator (1 person, full project)
- [ ] Commission composer (5 tracks)
- [ ] Optional: commission voice actor for top 6 recurring customers
- [ ] Author 6 ActDataSO + 36 CaseDataSO
- [ ] Author 22 CustomerSO + 18 BookSO
- [ ] Build Pinboard.prefab with drag-drop + red-string LineRenderer
- [ ] Build MagnifierController + reveal-hotspot system
- [ ] Wire 6 Act scenes
