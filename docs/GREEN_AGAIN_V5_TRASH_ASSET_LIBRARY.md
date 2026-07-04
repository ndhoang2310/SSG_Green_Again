# Green Again V5 - Trash Asset Library

Date: 2026-07-04

Purpose: ghi lại cấu trúc `game.Workspace.Trash` sau khi các model rác mới được đưa vào Studio. Folder này là thư viện asset để runtime clone hoặc map sang gameplay sau này; không phải runtime quest folder.

## 1. Vai trò

`Workspace.Trash` hiện là source asset library cho rác, thùng rác và scene dressing.

Không dùng folder này như nơi chứa rác quest đang active. Runtime gameplay hiện vẫn dùng:

```text
Workspace.GreenAgainV5_StoryRuntime
```

Quy tắc chính:

- Asset trong `Workspace.Trash` là template hoặc scene placement.
- Template phải giữ `Interactable=false`.
- Runtime clone mới được set `Interactable=true`, `InteractId`, `StoryQuestId`, `Collected`, `TrashCategory` theo quest.
- Không cho template tự chạy script khi Play.
- Không quét toàn bộ `Workspace.Trash` mỗi frame. Nếu cần dùng asset library, cache một lần khi server init hoặc lúc spawn quest props.
- `StoryRuntimeMVP` hiện đã clone cleanup trash và sorting bin visuals từ thư viện này vào `Workspace.GreenAgainV5_StoryRuntime`.

## 2. Cấu trúc hiện tại

```text
Workspace.Trash
+-- Collectibles
|   +-- Plastic
|   +-- Metal
|   +-- PaperCardboard
|   +-- Mixed
|   +-- Organic
|   +-- Hazardous
+-- Props
|   +-- Bins
|   +-- Piles
|   +-- LargeDebris
+-- ScenePlacements
|   +-- LegacyTrashScene_CongArea
+-- _Unsorted
+-- README_TrashLibrary
```

Current counts after restructuring:

| Folder | Count | Notes |
|---|---:|---|
| `Collectibles.Plastic` | 6 | bottles, cup, wrappers, plastic bag |
| `Collectibles.Metal` | 1 | crushed can |
| `Collectibles.PaperCardboard` | 5 | paper and cardboard boxes |
| `Collectibles.Mixed` | 7 | trash bags, milk carton, takeout containers |
| `Collectibles.Organic` | 1 | banana peel |
| `Collectibles.Hazardous` | 3 | battery, broken bulb, chemical bottle |
| `Props.Bins` | 1 | trash can prop/template |
| `Props.Piles` | 2 | trash pile props |
| `Props.LargeDebris` | 1 | shoe/debris prop |
| `ScenePlacements` | 1 | old placed trash scene kept, not deleted |
| `_Unsorted` | 0 | should stay empty after cleanup |

## 3. Template Attributes

Root attributes on `Workspace.Trash`:

| Attribute | Value |
|---|---|
| `GreenAgainV5` | `true` |
| `AssetLibrary` | `true` |
| `LibraryVersion` | `V5_TrashLibrary_2026_07_03` |
| `Purpose` | `Source trash models for Green Again runtime cloning and scene dressing` |
| `UpdatedBy` | `Codex` |

Common attributes on asset templates:

| Attribute | Purpose |
|---|---|
| `GreenAgainV5=true` | Marks asset as part of V5 tooling |
| `GreenAgainAssetRole="Template"` | Source object for cloning |
| `GreenAgainKind` | `Trash`, `SortingBin`, or `Decoration` |
| `TrashCategory` | `Plastic`, `Metal`, `Paper`, `Mixed`, `Organic`, or `Hazardous` |
| `ObjectName` | Vietnamese display name for prompt/marker if cloned |
| `Action` | Suggested prompt action, e.g. `Nhat`, `Phan loai vao`, `Kiem tra` |
| `Interactable=false` | Prevents client prompt/runtime cache from treating templates as live quest objects |
| `OriginalName` | Original imported asset name before cleanup |

Important distinction:

- `PaperCardboard` folder maps to runtime `TrashCategory="Paper"`.
- `Organic` and `Hazardous` are supported by the sorting minigame/server mapping, but current main quest cleanup mappings do not yet place those categories in the player bag.

## 4. Asset Names

### Plastic

```text
CandyWrapper
PlasticBottle_Tool
PlasticCup_RedSolo
PlasticBottle_03
SnackWrapper_Lays
PlasticBag_Crumpled
```

### Metal

```text
MetalCan_Crushed
```

### PaperCardboard

```text
CardboardBox_Carton
CardboardBox_Accessory
PaperSheet
CardboardBox_LootedC
Paper_Crumpled
```

### Mixed

```text
TrashBag_Garbage01
Carton_Milk
TrashBag_BlackSmall
TakeoutContainer_Tool
TrashBag_Mesh
TakeoutCarton_01
TrashBag_Part
```

### Organic

```text
BananaPeel
```

### Hazardous

```text
ChemicalBottle_Small
Battery_Old
LightBulb_Broken
```

### Props

```text
Props.Bins.TrashCan_P7
Props.Piles.TrashPile_Part
Props.Piles.TrashPile_Model
Props.LargeDebris.Shoe_Debris01
```

## 5. Runtime Usage Pattern

`StoryRuntimeMVP` now uses real asset templates for cleanup trash and sorting bins.

1. Find template from `Workspace.Trash.Collectibles.<Category>` or `Workspace.Trash.Props`.
2. Clone it into `Workspace.GreenAgainV5_StoryRuntime`.
3. Pivot the clone to the quest's grounded gameplay position.
4. Measure the clone bounding box and shift it so the model bottom sits exactly on the spawn Y coordinate.
5. Set clone attributes:

```text
GreenAgainV5 = true
GreenAgainKind = "Trash"
GreenAgainAssetRole = "RuntimeClone"
Interactable = true
InteractId = "trash_<QuestId>_<Index>"
ObjectName = <Vietnamese display name>
Action = "Nhat"
StoryQuestId = <QuestId>
TrashCategory = "Plastic" | "Metal" | "Paper" | "Mixed"
Collected = false
```

6. On pickup, record the category into the player's runtime bag, then hide/destroy the clone according to the existing cleanup flow.

Do not enable `Interactable=true` on the source template.

Sorting bins use:

```text
Workspace.Trash.Props.Bins.TrashCan_P7
```

Runtime bin clones are recolored by minigame bin and use the same grounded-bottom placement rule.
World bin interaction now opens the sorting minigame; the bins no longer auto-sort a whole category directly.
Sorting minigame items also use this library visually: `StoryRuntimeMVP` sends each picked item's `templatePath`, and `StoryClientMVP` resolves that path under `Workspace.Trash` to render a 3D `ViewportFrame` card.

Sorting minigame bin mapping:

| Runtime trash category | Correct bin id | UI label |
|---|---|---|
| `Plastic` | `Recycle` | Tái chế |
| `Metal` | `Recycle` | Tái chế |
| `Paper` | `Recycle` | Tái chế |
| `Mixed` | `Mixed` | Còn lại |
| `Organic` | `Organic` | Hữu cơ |
| `Hazardous` | `Hazardous` | Nguy hiểm |

## 6. Current Quest Asset Mapping

Current cleanup quest visual mapping in `StoryRuntimeMVP`:

| Quest | Index | Template | Runtime category | Display name |
|---|---:|---|---|---|
| `Q1_03_CleanEntrance` | 1 | `Collectibles.Mixed.TrashBag_BlackSmall` | `Mixed` | Túi rác lẫn |
| `Q1_03_CleanEntrance` | 2 | `Collectibles.Plastic.PlasticBottle_03` | `Plastic` | Chai nhựa |
| `Q1_03_CleanEntrance` | 3 | `Collectibles.Metal.MetalCan_Crushed` | `Metal` | Lon nước |
| `Q2_03_CleanGrocery` | 1 | `Collectibles.Plastic.PlasticBag_Crumpled` | `Plastic` | Túi nilon vò |
| `Q2_03_CleanGrocery` | 2 | `Collectibles.Plastic.SnackWrapper_Lays` | `Plastic` | Vỏ snack |
| `Q2_03_CleanGrocery` | 3 | `Collectibles.PaperCardboard.Paper_Crumpled` | `Paper` | Giấy vò |
| `Q3_03_CleanField` | 1 | `Collectibles.Plastic.PlasticBottle_03` | `Plastic` | Chai nhựa |
| `Q3_03_CleanField` | 2 | `Collectibles.Plastic.PlasticCup_RedSolo` | `Plastic` | Ly nhựa |
| `Q3_03_CleanField` | 3 | `Collectibles.Plastic.SnackWrapper_Lays` | `Plastic` | Vỏ snack |
| `Q3_03_CleanField` | 4 | `Collectibles.Metal.MetalCan_Crushed` | `Metal` | Lon nước |
| `Q4_02_FollowRiverTrash` | 1 | `Collectibles.Mixed.TrashBag_Garbage01` | `Mixed` | Túi rác mắc bờ sông |
| `Q4_02_FollowRiverTrash` | 2 | `Collectibles.Plastic.PlasticBottle_03` | `Plastic` | Chai nhựa trôi dạt |
| `Q4_02_FollowRiverTrash` | 3 | `Collectibles.PaperCardboard.Paper_Crumpled` | `Paper` | Giấy ướt |
| `Q5_02_ClearDrain` | 1 | `Collectibles.Mixed.TrashBag_BlackSmall` | `Mixed` | Túi rác kẹt cống |
| `Q5_02_ClearDrain` | 2 | `Collectibles.Plastic.PlasticBottle_03` | `Plastic` | Chai nhựa kẹt cống |
| `Q5_02_ClearDrain` | 3 | `Collectibles.Metal.MetalCan_Crushed` | `Metal` | Lon nước kẹt cống |

If changing which model appears in a quest, update `TRASH_ASSET_VARIANTS` in:

```text
game.ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP
```

## 7. Safety Notes

- There used to be two root instances named `Workspace.Trash`: one `Model` and one `Folder`.
- The old scene model was preserved under:

```text
Workspace.Trash.ScenePlacements.LegacyTrashScene_CongArea
```

- After restructuring, there should be exactly one root `Workspace.Trash`, and it should be a `Folder`.
- Imported asset scripts inside the library were disabled so they do not run during Play. They were kept for reference, not deleted.
- Final verification at restructure time:
  - root `Workspace.Trash` count: `1`
  - active scripts inside `Workspace.Trash`: `0`
  - descendants with `Interactable=true`: `0`
- Runtime replacement verification on 2026-07-04:
  - Play mode spawned `16` cleanup trash clones from `Workspace.Trash` into `Workspace.GreenAgainV5_StoryRuntime`.
  - Every cleanup clone had `SourceTrashTemplate` set to a real template path.
  - Clone bottom Y matched the quest spawn Y for Q1, Q2, Q3, Q4, and Q5 cleanup positions.
  - Automated Q1 flow reached `Q1_04_SortFirstTrash` and spawned `4` sorting bin clones from `Props/Bins/TrashCan_P7`.
  - Sorting bin bottom Y matched `TrashSite` spawn Y `58.450`.
  - Source templates remained `Interactable=false`.
- Sorting minigame verification on 2026-07-04:
  - Q1 sorting interaction opened `StoryClientMVP.SortingMinigame` with `3` bag items and `4` bins.
  - All `3` Q1 bag items rendered visual `ViewportFrame` cards with `WorldModel` previews from the picked templates.
  - Verified visual item template paths: `Collectibles/Mixed/TrashBag_BlackSmall`, `Collectibles/Plastic/PlasticBottle_03`, `Collectibles/Metal/MetalCan_Crushed`.
  - Wrong submit `Plastic -> Mixed` kept the sorting quest active and showed retry text.
  - Correct submits `Plastic -> Recycle`, `Metal -> Recycle`, `Mixed -> Mixed` completed sorting and advanced to Chị Lan.

## 8. When Adding New Trash Assets

Add new assets to the matching folder:

| Asset type | Folder |
|---|---|
| Bottle, cup, wrapper, plastic bag | `Collectibles.Plastic` |
| Can, metal scrap | `Collectibles.Metal` |
| Paper, cardboard, box | `Collectibles.PaperCardboard` |
| Trash bag, food carton, mixed packaging | `Collectibles.Mixed` |
| Food waste | `Collectibles.Organic` |
| Battery, bulb, chemical container | `Collectibles.Hazardous` |
| Trash cans/bins | `Props.Bins` |
| Static trash piles | `Props.Piles` |
| Large non-sorting debris | `Props.LargeDebris` |

For every new template:

- Rename it to a stable English technical name.
- Set `GreenAgainV5=true`.
- Set `GreenAgainAssetRole="Template"`.
- Set `Interactable=false`.
- Set `ObjectName` to Vietnamese display text.
- Set `GreenAgainKind` and `TrashCategory` or `PropType`.
- Disable any imported `Script` or `LocalScript` unless it is intentionally part of a future, documented gameplay system.
