# 🛠 Unity Setup Guide — Antiquaria

## 1. Prerequisites

- Unity Hub installed
- Unity **6 LTS (6000.4.4f1)** installed via Unity Hub
- Git installed
- 4 GB free disk for project + cache

## 2. Clone & open

```bash
git clone https://github.com/Abdulmalek-Agents/antiquaria.git
cd antiquaria
```

In Unity Hub: **Add → Open existing project → select `antiquaria/`**. Unity will prompt to install 6000.4.4f1 if not already present.

## 3. Set render pipeline (2D-URP)

Project Settings → Graphics → Scriptable Render Pipeline → assign `URP-2D` asset (located at `Assets/_Project/Settings/URP_2D.asset`).

## 4. Import Asset Store packs

Log into the Unity Asset Store with the Inventix account that owns the packs. From Package Manager → My Assets, import:

| Pack | Folder destination |
|---|---|
| Pixel Crushers Dialogue System | `Assets/_ThirdParty/PixelCrushers` |
| Bamao Pack Fantasy GUI | `Assets/_ThirdParty/Bamao` |
| Heat Complete Modern UI | `Assets/_ThirdParty/Heat` |
| Game UI & Puzzle SFX Pack | `Assets/_ThirdParty/GameUISFX` |
| Eyes Animator | `Assets/_ThirdParty/EyesAnimator` |
| Cutscene Engine | `Assets/_ThirdParty/CutsceneEngine` |
| Lumen Stylized Light FX 2 | `Assets/_ThirdParty/LumenFX2` |

> Note: `Assets/_ThirdParty/` is in `.gitignore` per Asset Store EULA.

## 5. Must-buy: 2D pen-and-ink atlas

Buy one of:
- Asset Store "Hand-Drawn Mystery Kit" (~$25), OR
- Commission frames from your illustrator (preferred for style coherence)

Place in `Assets/_ThirdParty/MysteryAtlas/`.

## 6. Wire prefabs

1. Open `Scenes/Bootstrap.unity`. Press Play — you should see the title card.
2. Open `Scenes/Act_01_DayOne.unity`. Drag `Prefabs/UI/Pinboard.prefab` into the scene.
3. Drag `Prefabs/Character/Player_Counter.prefab` into the scene.
4. Drag `Prefabs/Customer/Mr_Halloway.prefab` into the customer queue object.
5. Press Play. Mr. Halloway should arrive at the counter within 5 seconds.

## 7. Author your first case

In the Project window: `Data/Cases/` → right-click → Create → Antiquaria → CaseDataSO. Name it `case_halloway_pocketwatch`. Fill in:

- **Object sprite**: assign from `Art/Objects/Watch_Breguet.png`
- **True provenance**: "1820s Breguet, Paris"
- **Valid verdict**: Authenticate
- **Acceptable verdicts**: Authenticate, Refer
- **Evidence pieces**: drag 3 HotspotSO assets (hallmark, date stamp, foxing)
- **Hint tiers**: 3 strings, escalating

Press Play. The new case should appear on Mr. Halloway's counter.

## 8. Build target

- File → Build Settings → Switch Platform → Windows + Linux + Mac
- IL2CPP scripting backend recommended for release
- Compression: LZ4HC for release

## 9. No proxy server, no API key, no internet required

The shipping game is fully offline. There is no runtime LLM call. No environment variables or network configuration are needed.

## 10. Troubleshooting

| Symptom | Fix |
|---|---|
| Pink materials | Project not on URP-2D — re-assign in Graphics settings |
| Dialogue not appearing | Pixel Crushers package may need Database asset re-linked in scene |
| Missing fonts | Import TextMeshPro Essential Resources |
| First-run save error | Delete `%APPDATA%/InventixGames/Antiquaria/save.json` and re-launch |
