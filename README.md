# 🔍 Antiquaria — The Curator's Atlas

> *"Every object remembers. The trick is making it talk."*

A cozy single-player **deduction-and-antiquing sim** set in 1890s Edinburgh. You inherit your great-aunt Marguerite's curio shop — and her unfinished ledger. Customers bring you objects of uncertain origin; your job is to authenticate them through close examination, archive research, and your ever-growing pinboard of cross-referenced clues. Build your reputation, earn the trust of collectors, and unravel the mystery behind Marguerite's disappearance.

**Pitch in one line:** *Strange Horticulture × Return of the Obra Dinn × Stardew Valley's tactile pacing.*

| | |
|---|---|
| **Genre** | Cozy Deduction & Antiquing Sim |
| **Platforms** | PC (Steam) primary; Switch + iPad stretch |
| **Engine** | Unity **6 LTS (6000.4.4f1)** |
| **Render** | 2D Universal Render Pipeline (URP-2D) |
| **Target frame-rate** | 60 fps on integrated GPU |
| **Mission 1 scope** | *Day One* — shop opens, first customer, first authentication |
| **Designed for** | 6 Acts (~10–14 hour main story + endless DLC case-packs) |
| **Team size** | 1–3 (solo-dev feasible) |
| **Budget** | ~$25–40k |
| **Target ship** | within 10 months from greenlight |
| **Runtime AI features** | **None** — fully offline. Customer dialogue is hand-authored `DialogueNodeSO` trees. |
| **AI in development** | Claude Code & Claude Agents are used in the studio workflow. See [docs/04_TECHNICAL_ARCHITECTURE.md](docs/04_TECHNICAL_ARCHITECTURE.md). |

## Why this game

Strange Horticulture (Iceberg Interactive, 2022): ~500k Steam units, 96% positive. The Case of the Golden Idol I+II (Color Gray Games): ~1M combined, 96% positive. Return of the Obra Dinn (Lucas Pope): 2M+ units. **The "tactile-puzzle deduction" lane has proven demand at scale, no scheduled 2027 competitor, and zero overlap with our existing slate.** Antiquaria slots cleanly between Strange Horticulture's plant-shop tactility and Obra Dinn's deductive grandeur — with cozy Edinburgh pacing borrowed from Stardew.

Details in [`docs/01_IDEATION_AND_TRENDS.md`](docs/01_IDEATION_AND_TRENDS.md).

## What's in this repo

```
antiquaria/
├── README.md                              ← you are here
├── LICENSE                                ← MIT (original code/docs only)
├── CHANGELOG.md
├── .gitignore                             ← Unity-standard
└── docs/
    ├── 00_PORTFOLIO_REVIEW_BOARD.md       ← 14-expert vote + verdict
    ├── 01_IDEATION_AND_TRENDS.md          ← market evidence
    ├── 02_GAME_DESIGN_DOCUMENT.md         ← full GDD
    ├── 03_ASSET_PLAN.md                   ← Unity Asset Store list (~$60 must-buy)
    ├── 04_TECHNICAL_ARCHITECTURE.md       ← Unity 2D-URP architecture
    ├── 05_PRODUCTION_PLAN.md              ← 10-month phase plan
    ├── 06_CRITIC_REVIEW_CYCLES.md         ← 3-cycle critic review (14 experts)
    ├── 07_UNITY_SETUP_GUIDE.md            ← click-by-click setup
    └── 08_MARKETING_PLAN.md               ← wishlist + Steam Next Fest plan
```

## Quick start

1. Read [`docs/07_UNITY_SETUP_GUIDE.md`](docs/07_UNITY_SETUP_GUIDE.md).
2. New Unity **6 LTS (6000.4.4f1)** 2D-URP project.
3. Import: Pixel Crushers Dialogue System, Bamao Pack Fantasy GUI, Heat UI, Game UI & Puzzle SFX Pack, Eyes Animator — from inventory. Plus must-buy: 2D Pen-and-Ink atlas pack (~$25) and a paper/parchment SFX commission (~$30).
4. Author cases in `Assets/_Project/Data/Cases/`.
5. Open `Scenes/Bootstrap.unity` → Play.

## Status

| Stage | Status |
|---|---|
| 14-expert Cycle 1 vote (concept) | ✅ Approved (avg **8.43/10**) |
| 14-expert Cycle 2 (GDD) | ✅ Approved with 4 required changes (all applied) |
| 14-expert Cycle 3 (architecture + asset + marketing) | ✅ Final Approved (14/14 clean) |
| Mission 1 *Day One* implementation | ⏳ Pending Unity import |
| Acts 2–6 outlined | ✅ Data-driven |
| Steam page | ⬜ Schedule for Month 4 |

> Maintained by Abdulmalek-Agents (Inventix Games). PRs welcome.
