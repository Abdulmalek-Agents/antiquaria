# 🛠 Technical Architecture — Antiquaria

> Unity **6 LTS (6000.4.4f1)** + URP-2D. Single-player. Offline. No networking. No procedural generation.

## 1. Tech stack

| Layer | Choice | Reason |
|---|---|---|
| Engine | Unity 6 LTS 6000.4.4f1 | Stable, current portfolio standard |
| Render | URP-2D | 2D pipeline; low GPU cost |
| Language | C# 10 | Standard |
| Data | ScriptableObjects + JSON for save | Designer-friendly, no DB |
| Save | Custom JSON in `Application.persistentDataPath` | No cloud required (Steam Cloud opt-in) |
| Networking | **None** | Single-player |
| Procgen | **None** | Hand-authored cases |
| Localisation | Unity Localization Package | EN at launch; ES/DE/FR/JP post-launch |
| Input | New Input System | Controller + KB+M from Day 1 |

## 2. Core architecture

### Service Locator pattern (matches portfolio standard)

```
GameBootstrap (entry scene)
  └─ ServiceLocator
       ├─ MissionService  (current Act, current Case)
       ├─ SaveService     (JSON to disk + Steam Cloud)
       ├─ AudioService    (music + SFX + ambience layers)
       ├─ DialogueService (Pixel Crushers wrapper, scripted)
       ├─ ReputationService (3 factions, ±100 each)
       ├─ PinboardService (drag-drop + red-string state)
       └─ HintService     (coins, escalation tiers)
```

### Data layer (ScriptableObjects)

- `ActDataSO` — title, cases, customer roster, music cues
- `CaseDataSO` — object, true provenance, valid verdicts, evidence pieces, hints
- `EvidencePieceSO` — text, image, source, reveals-on-trigger
- `CustomerSO` — portrait, voice guide, faction, dialogue root
- `BookSO` — title, pages, unlock condition
- `DialogueNodeSO` — branching scripted dialogue (no LLM)
- `LineBankSO` — quip variants for recurring customer greetings

## 3. Gameplay systems

### Examination system
- `ObjectInspectable` MonoBehaviour holds 1–N `HotspotSO` zones.
- Magnifier hover within a hotspot for >250ms triggers reveal event.
- Reveal posts an `EvidenceFoundEvent` to the EventBus → Pinboard auto-adds the clue card.

### Pinboard system
- 4 columns (cases / customers / factions / Marguerite). Each is a snap-to-grid.
- Clue cards are `PinCard` prefabs (Image + 3-line summary).
- Connections are line-renderer segments stored as `(cardId_a, cardId_b, noteText)`.
- Annotations: double-click on segment → player-typed one-line note (saved with case state).

### Verdict system
- Three buttons: **Authenticate / Refer / Refuse**.
- Each CaseDataSO declares its `validVerdict` and `acceptableVerdicts` (sometimes Refer is also OK).
- On click: reputation deltas applied, ledger updated, customer dialogue branches to outcome.

### Hint system (Cycle 2 required change)
- `HintService.RequestHint(caseId)` returns the next tier (nudge → point → solve).
- Each tier costs 1 hint coin.
- Cycle protects against grind: hints unlocked per case, max 3 per case.

## 4. Save schema (simplified)

```json
{
  "version": 1,
  "actId": "act_1_day_one",
  "caseProgress": [{"caseId":"c1_halloway_watch","verdict":"Authenticate","hintCoinsUsed":0}],
  "reputation": {"royal":12,"provenance":3,"black":0},
  "hintCoins": 3,
  "booksUnlocked": ["book_breguet","book_hallmarks_uk"],
  "marguerite_letters": ["letter_01"],
  "customersMet": ["halloway","dunne"],
  "pinboard": {"cards":[...],"connections":[...]}
}
```

## 5. Scenes

- `Bootstrap.unity` — service locator, loads MainMenu
- `MainMenu.unity` — title, continue, new game, settings, credits
- `Act_01_DayOne.unity` through `Act_06_CuratorsAtlas.unity` — one scene per Act
- `Credits.unity`

## 6. Performance budget

- Memory: <500 MB at peak (2D atlas + audio).
- CPU: 60 fps on integrated GPU (no GPU dependence).
- Build size: <500 MB compressed (Steam download).

## 7. AI in development (NOT runtime)

Claude Code & Claude Agents are used during development for:
- Drafting customer dialogue first-pass (writer rewrites)
- C# scaffolding (review by lead programmer)
- Case-generator prototypes (final cases are hand-authored)
- Test-case generation for the case-verification harness

**Shipping game contains zero runtime LLM calls.** No proxy server, no API key, no internet config required to run.
