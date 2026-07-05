# Green Again V6 - Roblox Code Structure

Date: 2026-07-05

Purpose: tai lieu nay mo ta cau truc code hien co trong Roblox Studio cho Green Again V6. Doc file nay truoc khi them, sua, tach, hoac refactor script trong Roblox.

Scope:

- Dua tren V6 docs hien tai va cay script doc truc tiep tu Roblox Studio.
- Tap trung vao code gameplay/story active cua V6.
- Cac script nam trong asset import/model review duoc ghi nhan la "asset script" va khong phai runtime chinh neu chua duoc V6 doc chap nhan.

## 0. V6 Expansion Note

V6 inherits the active V5 story runtime baseline, then adds Chapter 5 expansion content inside the same MVP scripts and map root:

```text
Q5_05_ResidentialAfterRain
-> Q5_06_CareSmallLives
-> Q5_07_NeighborhoodPlanting
-> Q5_08_ReturnToCommunityHouse
```

These are implemented inside the existing `StoryRuntimeMVP` and `StoryClientMVP` patterns. Do not add animal AI, pathfinding, rescue simulation, or a new minigame for `CareSmallLives`; use cleanup, placement, visual state changes, and dialogue reactions.

Important: the current Studio root remains `Workspace["=== GREEN AGAIN V5 ==="]`. Any `=== GREEN AGAIN V6 ===` root should be treated as a future migration/rename note, not the active implementation target for this pass.

## 1. Rule Doc Truoc Khi Code

Truoc khi code trong Roblox, agent phai lam theo thu tu:

1. Doc `docs/V6/AGENT_COLLABORATION_RULES_GREEN_AGAIN_V6.md`.
2. Doc `docs/V6/GREEN_AGAIN_V6_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`.
3. Doc `docs/V6/GREEN_AGAIN_V6_MVP_IMPLEMENTATION_SUMMARY.md`.
4. Doc file nay de biet script nao dang so huu behavior nao.
5. Neu sua quest/dialogue/map/cutscene, doc them doc chuyen biet tuong ung.
6. Viet plan ngan truoc khi sua script:
   - Logic gameplay se chay tu dau den dau.
   - Script/folder nao se duoc sua.
   - Data nao can them vao bang quest/dialogue/config.
   - RemoteEvent/Attribute nao se dung.
   - UI nao hien thi/bi an.
   - Cach test sau khi code.

Khong tao script moi neu behavior co the nam trong script active hien co.

## 2. High-Level Architecture

Green Again V6 hien la mot MVP Roblox Studio tap trung vao 2 script story chinh:

```text
ServerScriptService
+-- GreenAgainProject
    +-- Runtime_To_Add
    |   +-- StoryRuntimeMVP       -- server authority: quest, dialogue, state, interaction
    +-- Existing_Environment_Systems
        +-- DayNightCycle         -- lighting setup

ReplicatedFirst
+-- GreenAgainStartupLoader     -- startup brand loader before waiting screen is ready

StarterPlayer
+-- StarterPlayerScripts
|   +-- StoryClientMVP            -- client story HUD, marker, dialogue UI, input E
|   +-- GraphicsManager           -- graphics quality UI and visual settings
|   +-- PlayerScriptsLoader       -- default Roblox PlayerModule loader
|   +-- PlayerModule              -- default Roblox camera/control modules
|   +-- RbxCharacterSounds        -- default Roblox character sound script
+-- StarterCharacterScripts
    +-- SprintStaminaScript       -- Shift sprint, no stamina UI
    +-- CustomFootstepSounds      -- quieter character sounds, grass footstep override

StarterGui
+-- MainMenuGui
|   +-- MainMenuController        -- team-owned waiting screen / main menu
+-- TeleportFrame
    +-- Handler                   -- fade overlay for teleport portals

ReplicatedStorage
+-- TeleportationDoorEvent        -- teleport fade event
+-- GreenAgainProject
    +-- Data_To_Add               -- currently reserved/empty
    +-- Events_To_Add             -- RemoteEvents for story runtime/client

Workspace
+-- === GREEN AGAIN V5 ===        -- current main map root used by V6 expansion
+-- Trash                         -- source asset library for trash templates and scene dressing
+-- GreenAgainV5_ClientAnchors    -- server-created marker anchor parts
+-- GreenAgainV5_StoryRuntime     -- runtime props folder when spawned
+-- GreenAgainV5_LocalObjectiveAnchors -- local client marker anchors while playing
+-- MainMenuAssets                -- client-created menu particles/buttons while menu active
```

Design principle:

- Server owns progression and validates interaction.
- Client owns presentation and local input.
- Map objects are selected by Attributes, not by hardcoded click detectors on every object.
- Runtime props are temporary gameplay affordances, not permanent fake map locations.

## 3. Active Runtime Ownership

| Layer | Path | Class | Owner | Chinh sua khi nao |
|---|---|---|---|---|
| Server story | `game.ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP` | `Script` | Green Again V6 MVP | Quest, dialogue data, interaction routing, runtime trash/bin/placement, NPC staging, player story state |
| Client story | `game.StarterPlayer.StarterPlayerScripts.StoryClientMVP` | `LocalScript` | Green Again V6 MVP | HUD, marker, dialogue panel, choice buttons, interaction prompt, notebook/end overlay |
| Startup loader | `game.ReplicatedFirst.GreenAgainStartupLoader` | `LocalScript` | Startup presentation | Logo loading screen before `MainMenuGui`/`MainMenuAssets` finish rendering |
| Sprint | `game.StarterPlayer.StarterCharacterScripts.SprintStaminaScript` | `LocalScript` | Movement utility | Shift sprint speed only; do not restore old stamina bar |
| Main menu | `game.StarterGui.MainMenuGui.MainMenuController` | `LocalScript` | Team-owned waiting screen | Only touch if user explicitly assigns menu/startup flow |
| Teleport server | `Workspace["=== GREEN AGAIN V5 ==="].MAP_ROUTE.00_Spawn_And_Teleport.TeleportSystem_Active.TeleportMasterScript` | `Script` | Map transition utility | Portal touched -> fade -> move character to destination |
| Teleport client | `game.StarterGui.TeleportFrame.Handler` | `LocalScript` | Map transition utility | Teleport fade UI |
| Graphics | `game.StarterPlayer.StarterPlayerScripts.GraphicsManager` | `LocalScript` | Visual/performance utility | Quality slider, lighting effects, wind sway |
| Environment | `game.ServerScriptService.GreenAgainProject.Existing_Environment_Systems.DayNightCycle` | `Script` | Environment utility | Global lighting baseline |
| Footsteps | `game.StarterPlayer.StarterCharacterScripts.CustomFootstepSounds` | `LocalScript` | Audio utility | Character sound volume and grass footstep id |

Obsolete systems must not be recreated:

- `StarterGui.GreenAgainHUD_V6`
- `StarterPlayer.StarterPlayerScripts.GreenAgainObjectiveClient`
- `ServerScriptService.GreenAgainProject.Runtime_To_Add.MapWiringBootstrap`
- Text UI cu: `Dang noi map Green Again V6...`

## 4. Server Runtime: StoryRuntimeMVP

Path:

```text
game.ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP
```

Primary responsibility:

- Tao RemoteEvents can thiet trong `ReplicatedStorage.GreenAgainProject.Events_To_Add`.
- Giu story state rieng cho tung player.
- Dinh nghia quest data, dialogue data, notebook text, NPC/location mapping.
- Tag map objects bang Attributes de client biet object nao dang interactable.
- Spawn runtime trash, sorting bins, placement markers/tree.
- Xu ly `OnInteractRequested` tu client.
- Mo/ket thuc dialogue va complete quest.
- Stage NPC o cac thoi diem quan trong.
- Fire objective/update/toast/notebook/end text ve client.

### 4.1 Data Tables Chinh

| Table | Vai tro |
|---|---|
| `EVENTS` | Danh sach RemoteEvents story runtime can co |
| `NPCS` | NPC id -> display name |
| `LOCATION_PATHS` | Location id -> duong dan trong map root |
| `LOCATION_FALLBACK_NAMES` | Ten object fallback khi path folder thay doi |
| `LOCATION_GAMEPLAY_POSITIONS` | Toa do gameplay grounded de marker/spawn khong bay cao |
| `QUEST_CLEANUP_POSITIONS` | Toa do rac runtime theo quest cleanup |
| `NPC_STAGE_POSITIONS` | Toa do staging NPC cho chuong/song/cao trao/ending |
| `QUESTS` | Quest id -> title, chapter, objective, target, complete rule, next quest |
| `ORDER` | Thu tu quest states |
| `NOTEBOOK` | Noi dung so tay theo chapter |
| `DIALOGUES` | Dialogue id -> lines, choices, completeQuest, ending |
| `SORTING_BINS` | Four minigame bins: Hazardous/Recycle/Organic/Mixed |
| `SORTING_CATEGORY_TO_BIN` | Runtime trash category -> correct minigame bin |
| `SORTING_ITEM_NAMES` | Runtime trash category -> display name in sorting minigame |

### 4.2 Quest Model

Moi quest trong `QUESTS` nen theo dang:

```lua
Q2_03_CleanGrocery = {
    title = "Truoc Cua Tiem",
    chapter = 2,
    objective = "Don rac quanh tap hoa",
    targetType = "Cleanup",
    targetId = "Grocery",
    complete = "Cleanup",
    count = 5,
    next = "Q2_04_SortGroceryTrash",
}
```

Fields quan trong:

- `targetType`: `Location`, `NPC`, `Cleanup`, `Sorting`, `Placement`, `Community`, `Cutscene`.
- `targetId`: id map/NPC/runtime target.
- `complete`: cach quest duoc complete.
- `dialogue`: dialogue id neu quest la NPC/dialogue-driven.
- `count`: so item can nhat/dat/ru.
- `notebook`: chapter note duoc unlock khi complete quest.
- `next`: quest tiep theo.

### 4.3 Player State

State duoc giu trong memory theo player:

```text
playerState[player]
+-- questId
+-- cleanup[questId]
+-- sorting[questId]
+-- placements[questId]
+-- community[npcId]
+-- notebooks[chapterId]
+-- bag[TrashCategory]
+-- bagItems[] = { id, category, name, templatePath }
+-- endingShown
```

State hien khong persistence qua DataStore. Neu can save/load sau nay, khong chen truc tiep lung tung vao client; tao plan rieng cho persistence layer.

### 4.4 RemoteEvents

`StoryRuntimeMVP` tao/dung cac event trong:

```text
game.ReplicatedStorage.GreenAgainProject.Events_To_Add
```

| RemoteEvent | Direction | Payload | Muc dich |
|---|---|---|---|
| `OnInteractRequested` | Client -> Server | `interactId` string | Player nhan E/click touch button |
| `OnQuestStarted` | Server -> Client | `questId` | Bao quest moi bat dau |
| `OnQuestCompleted` | Server -> Client | `questId` | Bao quest vua xong |
| `OnObjectiveChanged` | Server -> Client | objective table | Cap nhat tracker/marker |
| `OnDialogueOpen` | Server -> Client | dialogue payload | Mo dialogue lines/choices |
| `OnDialogueClose` | Client -> Server and Server -> Client | none | Client bao dialogue dong; server complete quest neu session cho phep |
| `OnFeedbackToast` | Server -> Client | text | Toast nho |
| `OnNotebookEntry` | Server -> Client | `{ chapter, text }` | So tay chapter |
| `OnEndText` | Server -> Client | text | Overlay ket thuc/post-ending |
| `OnSortingMinigameOpen` | Server -> Client | sorting payload or `{ close = true }` | Mo/dong UI keo-tha phan loai rac |
| `OnSortingMinigameSubmit` | Client -> Server | `itemCategory`, `binId` | Submit mot mon rac vao thung; server validate dung/sai |
| `OnCutsceneStart` | Server -> Client | `{ id = "CS1" }` | Bat dau cinematic lightweight tren client |
| `OnCutsceneFinished` | Client -> Server | `{ id = "CS1" }` | Bao server cutscene da ket thuc; server validate session/quest truoc khi tiep tuc |

`OnInteractionPrompt` dang ton tai trong ReplicatedStorage nhung khong phai event chinh cua `StoryClientMVP` hien tai.

Sorting payload item shape:

```lua
{
    id = "Q1_03_CleanEntrance_2",
    category = "Plastic",
    name = "Chai nhua",
    templatePath = "Collectibles/Plastic/PlasticBottle_03",
    correctBin = "Recycle",
}
```

`templatePath` is resolved by `StoryClientMVP` under `Workspace.Trash` and rendered inside a `ViewportFrame` for the draggable card. Keep it slash-separated and relative to the `Workspace.Trash` root.

### 4.5 Attribute Contract

Server tag objects bang Attributes. Client dua cac object co contract sau vao cache interactable:

```text
Interactable = true
InteractId = non-empty string
```

Performance note:

- `StoryClientMVP` khong duoc quet `workspace:GetDescendants()` moi frame.
- Client hien build cache object co `InteractId`, update cache bang `workspace.DescendantAdded/DescendantRemoving`, va refresh thua lam fallback.
- Check object gan player duoc throttle bang `NEARBY_SCAN_INTERVAL`, khong chay 60 lan/giay.
- Neu them loai object interactable moi, chi can gan dung Attributes de cache nhan ra; khong them mot vong scan rieng trong `Heartbeat`/`RenderStepped`.

Attributes dung chung:

| Attribute | Vi du | Muc dich |
|---|---|---|
| `GreenAgainV6` | `true` | Danh dau object thuoc runtime V6 |
| `GreenAgainKind` | `NPC`, `Location`, `Trash`, `SortingBin`, `Placement`, `Decoration` | Routing interaction |
| `InteractId` | `npc_BacXanh`, `loc_Hub`, `trash_Q1_03_CleanEntrance_1` | Id client gui len server |
| `ObjectName` | `Bac Xanh`, `Cong thoat nuoc cuoi xom` | Ten hien thi tren prompt/marker |
| `Action` | `Tro chuyen voi`, `Kiem tra`, `Nhat`, `Phan loai vao`, `Dat`, `Trong` | Text action trong prompt |
| `Interactable` | `true/false` | Bat/tat interaction theo quest |
| `NpcId` | `BacXanh` | NPC routing |
| `StoryLocation` | `Hub`, `TrashSite`, `Drain` | Location routing |
| `StoryQuestId` | `Q5_02_ClearDrain` | Runtime prop thuoc quest nao |
| `TrashCategory` | `Plastic`, `Metal`, `Paper`, `Mixed` | Sorting bag/bin |
| `Collected` | `true/false` | Cleanup state |
| `Sorted` | `true/false` | Sorting bin state |
| `Placed` | `true/false` | Placement state |
| `PlacementVisual` | `Tree`, `Flat` | Placement visual transform |
| `GreenAgainAssetRole` | `Template`, `RuntimeClone`, `ScenePlacement` | Distinguish source assets in `Workspace.Trash` from live quest props |

Khi them gameplay moi, uu tien mo rong contract nay thay vi tao mot he detect rieng.

### 4.6 Interaction Flow

```text
Player gan object interactable
-> StoryClientMVP hien prompt
-> Player nhan E hoac touch button
-> Client gui OnInteractRequested(interactId)
-> Server tim object bang InteractId
-> Server check Interactable va GreenAgainKind
-> Neu dang co cutscene session thi server bo qua interaction
-> handleNpc / handleTrash / handleSorting / handlePlacement / handleLocation
-> Server update state
-> Server fire Objective/Dialogue/Toast/Notebook/EndText
-> Client cap nhat UI/marker
```

Server la noi quyet dinh quest co duoc complete hay khong. Client khong tu tang quest.

## 5. Client Runtime: StoryClientMVP

Path:

```text
game.StarterPlayer.StarterPlayerScripts.StoryClientMVP
```

Primary responsibility:

- Wait `ReplicatedStorage.GreenAgainProject.Events_To_Add`.
- Tao `PlayerGui.GreenAgainStoryHUD` bang code.
- An UI cu `GreenAgainHUD_V6` va text `Dang noi map`.
- Hien quest tracker, interaction prompt, touch button, toast, notebook book/panel.
- Hien dialogue panel, progress text, continue button, 2 choice buttons.
- Tao marker objective dang hinh thoi xanh nho, khong co distance text.
- Chi bat story UI khi player da roi menu va o gan main map activation zone.
- Gui `OnInteractRequested` khi player nhan E/click touch interact.
- Gui `OnDialogueClose` khi dialogue ket thuc.
- Chay cutscene cinematic lightweight tu `OnCutsceneStart`: hide HUD/marker/notebook, camera `Scriptable`, letterbox/subtitle, tween camera, restore camera/UI, gui `OnCutsceneFinished`.
- Cache interactable targets theo `InteractId` va throttle nearby checks de tranh CPU spike tren map lon.

### 5.1 UI Created At Runtime

```text
PlayerGui.GreenAgainStoryHUD
+-- QuestTracker
|   +-- ChapterLabel
|   +-- QuestTitle
|   +-- ObjectiveLabel
+-- InteractionPrompt
+-- TouchInteractButton
+-- FeedbackToast
+-- NotebookUnlockNotice
+-- NotebookButton
+-- NotebookBook
|   +-- LeftPage
|   +-- RightPage
|   +-- Spine
+-- CutsceneOverlay
|   +-- TopBar
|   +-- BottomBar
|   +-- Title
|   +-- Subtitle
+-- DialoguePanel
|   +-- Speaker
|   +-- Progress
|   +-- DialogueText
|   +-- ContinueButton
|   +-- ChoiceA
|   +-- ChoiceB
+-- EndOverlay
+-- IntroOverlay
```

### 5.2 Marker System

Client tao local folder:

```text
Workspace.GreenAgainV5_LocalObjectiveAnchors
+-- CurrentStoryObjectiveAnchor
    +-- GreenAgainStoryObjectiveMarker
        +-- Diamond
        +-- Title
```

Server co the tao anchor parts trong:

```text
Workspace.GreenAgainV5_ClientAnchors
```

Marker rules:

- Chi mot marker active.
- Hinh thoi xanh + ten target.
- Billboard `StudsOffset` hien tai la `Vector3.new(0, 3.4, 0)` de marker nam gan target hon.
- Khong hien distance.
- An khi dialogue mo.
- An khi main menu con active.
- An trong free roam/post-ending.

### 5.3 Story UI Activation

`StoryClientMVP` khong hien HUD ngay trong lobby/menu. Client dung:

- `isMainMenuActive()` de check `PlayerGui.MainMenuGui`.
- `MAP_ACTIVATION_POINTS` + `STORY_ACTIVATION_DISTANCE` de xac dinh player da vao khu story.

Neu sua startup/menu/teleport, phai test:

- Menu con khoa di chuyen truoc PLAY.
- Sau PLAY character duoc unlock.
- Story HUD chi hien sau khi vao map chinh.
- Khong co duplicate HUD.

### 5.4 Interaction Performance

`StoryClientMVP` tung gay CPU cao vi `findNearbyTarget()` quet `workspace:GetDescendants()` moi Heartbeat khi player dang gameplay binh thuong. Khi dialogue mo, heartbeat return som nen CPU giam. Pattern nay da duoc thay the.

Current behavior:

- `interactableTargets` cache cac Instance co `InteractId`.
- `interactableSet` tranh duplicate trong cache.
- `refreshInteractableCache(true)` chay luc client init.
- `workspace.DescendantAdded` them target moi vao cache.
- `workspace.DescendantRemoving` xoa target khoi set; list duoc prune khi scan.
- `refreshInteractableCache(false)` chi refresh fallback theo `INTERACTABLE_CACHE_REFRESH_INTERVAL`.
- `findNearbyTarget(false)` throttle bang `NEARBY_SCAN_INTERVAL`.
- Prompt text/visibility chi update khi target/text doi.
- Cleanup HUD cu chi chay mot lan bang `oldConnectionHudCleaned`.

Rules:

- Khong them `workspace:GetDescendants()` trong Heartbeat/RenderStepped de tim interactable.
- Khong set UI text/visible moi frame neu gia tri khong doi.
- Neu can scan lon, cache truoc roi throttle hoac update bang event.

### 5.5 Field Center Anchor

Chapter 3 khong con phu thuoc vao holder/marker khung thanh de tuong tac.

Runtime data:

- `LOCATION_GAMEPLAY_POSITIONS.FieldCenter = Vector3.new(-59.66, 55.45, -3309.73)`
- `Q3_01_ToFootballField.targetId = "FieldCenter"`
- `Q3_03_CleanField.targetId = "FieldCenter"`
- `Q3_06_FieldReminder.targetId = "FieldCenter"`

`getLocation(locationId)` co fallback tao invisible `Part` trong `Workspace.GreenAgainV5_ClientAnchors` neu location co gameplay position nhung khong co object map that. Voi `FieldCenter`, part nay la interaction anchor o trung tam san bong:

```text
Workspace.GreenAgainV5_ClientAnchors.Location_FieldCenter
```

Rules:

- Anchor nay khong phai placeholder visual cho san bong; no chi dung de marker/prompt/interact route.
- Khong dua Q3 interaction ve `KhungThanh_01_Marker` / `KhungThanh_02_Marker` neu holder khung thanh khong con on dinh.
- Neu user do lai tam san chinh xac hon, chi cap nhat `LOCATION_GAMEPLAY_POSITIONS.FieldCenter` va docs lien quan.

## 6. Main Menu: MainMenuController

### 6.0 Startup Loader

Path:

```text
game.ReplicatedFirst.GreenAgainStartupLoader
```

Purpose:

- Replaces the default Roblox loading screen with a Green Again branded loader.
- Shows logo asset `rbxassetid://112991523200169` on a dark green background.
- Waits until the waiting screen has built its first usable state:
  - `PlayerGui.MainMenuGui` exists and is enabled.
  - `MainMenuGui.LogoImage` exists.
  - `Workspace.MainMenuAssets.PlayBtn` exists.
  - `Workspace.MainMenuAssets.SetBtn` exists.
  - `workspace.CurrentCamera` exists.
- Holds for at least `MIN_VISIBLE_TIME` so the player sees a stable logo, then fades out.

QA attributes written on `PlayerGui`:

```text
GreenAgainStartupLoaderShown
GreenAgainStartupLoaderReady
GreenAgainStartupLoaderTimedOut
GreenAgainStartupLoaderDuration
GreenAgainStartupLoaderClosed
```

Rule:

- Keep this as a separate `ReplicatedFirst` guard layer. Do not fold it into `MainMenuController` unless the menu owner explicitly takes over startup presentation.

Path:

```text
game.StarterGui.MainMenuGui.MainMenuController
```

Status: team-owned. Khong sua neu user khong giao ro.

Responsibilities:

- Neo character tai vi tri menu `MENU_CHARACTER_CFRAME`.
- Set camera scriptable tai `CAM`.
- Tao `workspace.MainMenuAssets`.
- Tao logo image, particles leaf/droplet, floating models, 3D PLAY/SETTING buttons.
- Khi PLAY:
  - Tao `TransitionOverlay` rieng de fade khong bi destroy som.
  - Unbind `MenuLoop`.
  - Move character ve `SpawnLocation` trong root V6 hoac fallback.
  - Set `player:SetAttribute("GreenAgainMenuFinished", true)`.
  - Cleanup pending ClickToMove path tu nut PLAY 3D.
  - Unanchor character va restore camera/humanoid.
  - Disable/destroy `MainMenuGui`.

Integration rule:

- `StoryClientMVP` phai ton trong viec menu con song.
- Menu khong nen nhan story/quest logic.
- Story HUD khong nen dieu khien visual/menu camera.
- Menu khong nen disable/re-enable PlayerModule controls trong khi mo; character duoc khoa bang anchor de PlayerModule van nhan du KeyDown/KeyUp, tranh ket WASD/Space sau PLAY.
- Khong force `DevComputerMovementMode` hoac them delayed control reset sau fade neu khong co ly do/plan test ro rang.

## 7. Movement And Presentation Utilities

### 7.1 SprintStaminaScript

Path:

```text
game.StarterPlayer.StarterCharacterScripts.SprintStaminaScript
```

Behavior:

- LeftShift/RightShift -> `Humanoid.WalkSpeed = 25`.
- Khong shift -> `Humanoid.WalkSpeed = 16`.
- Xoa `PlayerGui.StaminaGui` neu con ton tai.
- Khong dung Heartbeat de set speed moi frame; speed chi doi khi Shift pressed/released.

Rule:

- Khong khoi phuc stamina bar cu neu user khong yeu cau.
- Neu them stamina that, can plan UI/logic rieng va test khong che menu/story input.
- Khong them lai stamina drain/cooldown hoac vong `Heartbeat` ghi WalkSpeed lien tuc neu chua co yeu cau moi.

### 7.2 CustomFootstepSounds

Path:

```text
game.StarterPlayer.StarterCharacterScripts.CustomFootstepSounds
```

Behavior:

- Giam volume character sounds ve 30%.
- Neu `Humanoid.FloorMaterial == Grass`, doi Running sound sang grass footstep asset id.
- Khi roi grass, tra ve sound id mac dinh.

### 7.3 GraphicsManager

Path:

```text
game.StarterPlayer.StarterPlayerScripts.GraphicsManager
```

Behavior:

- Tao `PlayerGui.GraphicsQualityGui`.
- Co 5 muc chat luong do hoa.
- Dieu khien `Lighting.GlobalShadows`, bloom, sun rays, depth of field, atmosphere.
- Co auto-detect FPS.
- Co wind sway nhe cho mot so tree model theo ten.

Note:

- Script nay hien dung mot so icon Unicode trong UI. Neu sua file/script nay trong Studio, giu y nghia UI hien co.
- Day khong phai story HUD; khong tron quest UI vao day.

### 7.4 DayNightCycle

Path:

```text
game.ServerScriptService.GreenAgainProject.Existing_Environment_Systems.DayNightCycle
```

Behavior:

- Set `Lighting.GlobalShadows = true`.
- Set `ShadowSoftness = 0.25`.
- Set `ClockTime = 9.5`.
- Set `GeographicLatitude = 0`.

## 8. Teleport System

Server path:

```text
Workspace["=== GREEN AGAIN V5 ==="].MAP_ROUTE.00_Spawn_And_Teleport.TeleportSystem_Active.TeleportMasterScript
```

Client path:

```text
game.StarterGui.TeleportFrame.Handler
```

Structure expected:

```text
TeleportSystem_Active
+-- Portals
+-- Destinations
+-- TeleportMasterScript
```

Flow:

```text
Portal touched
-> read portal Attribute "Destination"
-> find matching BasePart in Destinations
-> FireClient TeleportationDoorEvent
-> wait fade seconds
-> move HumanoidRootPart to destination + EXIT_OFFSET
-> debounce 2 seconds
```

Client `TeleportFrame.Handler` fades `StarterGui.TeleportFrame.Frame` in/out when `TeleportationDoorEvent` fires.

Rule:

- Portal destination names live in Attributes.
- Do not use teleport to skip story quest states unless the quest docs explicitly say so.

## 9. ReplicatedStorage Contract

Current tree:

```text
ReplicatedStorage
+-- TeleportationDoorEvent
+-- GreenAgainProject
    +-- Data_To_Add
    +-- Events_To_Add
        +-- OnInteractRequested
        +-- OnInteractionPrompt
        +-- OnObjectiveChanged
        +-- OnDialogueOpen
        +-- OnDialogueClose
        +-- OnFeedbackToast
        +-- OnQuestStarted
        +-- OnQuestCompleted
        +-- OnNotebookEntry
        +-- OnEndText
```

Rules:

- Story RemoteEvents belong under `GreenAgainProject.Events_To_Add`.
- Teleport event currently lives at top-level `ReplicatedStorage.TeleportationDoorEvent`.
- Do not add duplicate RemoteEvents with similar names until old use is removed/documented.
- If adding shared config/modules later, place them under `GreenAgainProject.Data_To_Add` or a clearly named sibling and document the new contract.

## 10. Workspace Map And Runtime Folders

Main V6 root:

```text
Workspace["=== GREEN AGAIN V5 ==="]
```

Important child folders:

```text
MAP_ROUTE
+-- 00_Spawn_And_Teleport
+-- 01_Hub_NhaVanHoa
+-- 02_DiemTapKet_Rac
+-- 03_Lang_And_TapHoa
+-- 04_SanBong
+-- 05_River_And_Drain
+-- 06_NPCs

SYSTEMS_REVIEW
ENVIRONMENT_IMPORTED_REVIEW
PROPS_AND_INTERACTABLES_REVIEW
UNSORTED_REVIEW
NPC_CANDIDATES_REVIEW
```

Story-critical map objects:

| Id | Technical object | Display meaning |
|---|---|---|
| `Hub` | `NhaVanHoa_ThonNoiChuan` | Nha van hoa thon Ven Song |
| `TrashSite` | `DiemTapKetRacThai_ThonVenSong` | Diem tap ket rac |
| `Grocery` | `TapHoaCoTu_HouseOnly_Rural` | Tap hoa Co Tu |
| `FieldA` | `KhungThanh_01_Marker` | San bong thon Ven Song |
| `FieldB` | `KhungThanh_02_Marker` | San bong thon Ven Song |
| `FieldCenter` | runtime invisible anchor `Location_FieldCenter` | Trung tam san bong dung cho Chapter 3 interaction |
| `River` | `NPC_OngSau_Marker` | Bo song cho Ong Sau |
| `DrainMarker` | `OngNuoc_XaThai_Marker` | Cong thoat nuoc cuoi xom marker |
| `Drain` | `SYSTEMS_REVIEW.Doors_Vehicles_And_AssetScripts.OngThoatNuoc` | Cong thoat nuoc cuoi xom |
| `ResidentialLane` | runtime invisible anchor on `PROPS_AND_INTERACTABLES_REVIEW.Loose_Props.duong` | Ngo dan cu sau mua, `(250.00, 48.90, -3370.00)` |
| `SmallLivesCorner` | runtime invisible anchor on the same lane | Goc song nho, `(246.00, 48.90, -3385.00)` |
| `TreePlantingZone` | runtime route point | Cay non ngo dan cu, `(250.00, 48.90, -3370.00)` |

NPCs:

```text
Workspace["=== GREEN AGAIN V5 ==="].MAP_ROUTE.06_NPCs
+-- BacXanh
+-- ChiLan
+-- CoTu
+-- AnhTung
+-- BeNa
+-- OngSau
```

Runtime-created folders:

| Folder | Creator | Muc dich |
|---|---|---|
| `Workspace.GreenAgainV5_ClientAnchors` | Server runtime | Invisible anchor parts gan target object/model de marker co diem grounded |
| `Workspace.GreenAgainV5_StoryRuntime` | Server runtime | Runtime trash, sorting bins, placement props/tree crown |
| `Workspace.GreenAgainV5_LocalObjectiveAnchors` | Client runtime | Local objective marker anchor |
| `Workspace.MainMenuAssets` | Main menu client | Menu-only 3D buttons, droplets/leaves |

Asset library folders:

| Folder | Owner | Muc dich |
|---|---|---|
| `Workspace.Trash` | Green Again V6 asset library | Source templates for trash collectibles, sorting/bin props, piles, large debris, and preserved scene dressing |

## 11. Trash Asset Library

Detailed source doc:

```text
docs/V6/GREEN_AGAIN_V6_TRASH_ASSET_LIBRARY.md
```

Current root:

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
+-- _Unsorted
+-- README_TrashLibrary
```

Role:

- `Workspace.Trash` is a source asset library, not the active quest runtime folder.
- Live quest trash should still be cloned/spawned under `Workspace.GreenAgainV5_StoryRuntime`.
- Templates in `Workspace.Trash` must keep `Interactable=false`.
- Runtime clones must set quest-specific `InteractId`, `StoryQuestId`, `Collected`, `TrashCategory`, `ObjectName`, and `Action` before becoming interactable.
- Imported `Script` / `LocalScript` descendants inside the library are disabled unless a future documented gameplay system intentionally enables them.
- There should be exactly one root `Workspace.Trash`, and it should be a `Folder`.

`StoryRuntimeMVP` integration:

- `TRASH_LIBRARY_ROOT_NAME = "Trash"` points to the source library.
- `TRASH_ASSET_VARIANTS` maps cleanup quest id + item index to a source template, runtime category, and Vietnamese display name.
- Current cleanup counts are Q1=10, Q2=9, Q3=10, Q4=9, Q5=9. Keep each quest `count` aligned with its `TRASH_ASSET_VARIANTS` entry count.
- Dirt/stain cleanup visuals should use `Workspace.Trash.Props.Piles`; current mappings use `TrashPile_Part` for small flat stains and `TrashPile_Model` for larger pile/stain clusters.
- `TRASH_ASSET_VARIANTS` entries may include `rotation`, `preserveTemplateRotation`, `scale`, and `heightOffset`. Current `TrashPile_Part` entries use `rotation = CFrame.Angles(math.rad(90), 0, 0)`, current `TrashPile_Model` entries use `preserveTemplateRotation = true`, and all pile/stain entries use `heightOffset = -0.04`; current small mixed bags use `scale = 1.45` or `1.25`.
- `Q1_03_CleanEntrance` spawn Y is `48.43`, measured against `SanBeTong_Truoc` in front of the community house.
- `Q3_03_CleanField` and `Q4_02_FollowRiverTrash` cleanup spawn Y is `48.23`, measured from Terrain raycasts around those cleanup clusters (`~48.203`). Do not raise these back to `49.5`; that value makes several runtime clones float.
- `Q5_02_ClearDrain` stages Bác Xanh / Chị Lan on the dry bank using NPC pivot heights: `BacXanh = Vector3.new(-216.0, 53.58, -3512.0)`, `ChiLan = Vector3.new(-213.0, 53.36, -3510.0)`.
- `SORTING_BIN_TEMPLATE_PATH = { "Props", "Bins", "TrashCan_P7" }` is used for runtime sorting bin visuals.
- Cleanup trash clones are created by `createTrashModel()` / `createTrashObject()` and parented under `Workspace.GreenAgainV5_StoryRuntime`.
- Sorting bin clones are created by `createSortingBinObject()` and parented under `Workspace.GreenAgainV5_StoryRuntime`.
- `pivotModelBottomTo()` applies optional extra rotation and height offset, then grounds each clone by world-corner Y extents so rotated flat parts sit on the configured spawn Y plus any `heightOffset`.
- `setModelVisible()` operates over all `BasePart` descendants so wrapped `Model`, `MeshPart`, and imported `Accessory` templates work consistently.
- `handleSorting()` opens the sorting minigame instead of auto-sorting when the player interacts with a world bin.
- `TrashSite` uses ground-level gameplay/interact Y `51.52` so the green marker and sorting-bin interaction are reachable without jumping.
- Sorting-bin world interactables are invisible `StorySortingBinHitbox_*` parts; do not clone visible bin props at runtime because the sorting station already has static visible bins.
- Fallback primitive trash still exists only as a safety fallback if a source template is missing.

Current categories:

| Category folder | Runtime category | Notes |
|---|---|---|
| `Collectibles.Plastic` | `Plastic` | Bottles, cup, wrappers, plastic bag |
| `Collectibles.Metal` | `Metal` | Crushed can |
| `Collectibles.PaperCardboard` | `Paper` | Paper and cardboard props |
| `Collectibles.Mixed` | `Mixed` | Trash bags, food cartons, takeout containers |
| `Collectibles.Organic` | `Organic` | Food waste, currently used by Q3 |
| `Collectibles.Hazardous` | `Hazardous` | Batteries/chemical bottle, currently used by Q4/Q5 |
| `Props.Bins` | Sorting/placement prop | Bin models/templates |
| `Props.Piles` | `Mixed` or decoration | Runtime dirt/stain cleanup visuals and static pile visuals |
| `Props.LargeDebris` | Decoration/debris | Large non-sorting debris |

Sorting minigame rule:

- World bins are approach/interaction targets only.
- Actual classification happens in `StoryClientMVP.SortingMinigame`.
- Drag items are visual cards; each card renders the picked trash model in a `ViewportFrame` from its `templatePath`.
- `Props.Piles` cards use world-corner preview bounds and a higher angled camera so thin pile/stain visuals are not rendered edge-on.
- `Collectibles.Plastic.PlasticBag_Crumpled` uses the same high-angle preview path as piles so the crumpled bag is not framed too flat.
- Drag positioning uses centered cards and `ResponsiveScale`-corrected panel coordinates. Do not restore the old `draggingItem.offset = point - button.AbsolutePosition` approach, because it can shift away from the cursor when the HUD is scaled or the pointer starts over a child icon.
- Server validation lives in `StoryRuntimeMVP` via `SORTING_CATEGORY_TO_BIN`.
- Server keeps both aggregate counts in `bag[TrashCategory]` and per-item visual data in `bagItems`.
- Current quest cleanup categories map as `Plastic`, `Metal`, `Paper` -> `Recycle`; `Mixed` -> `Mixed`.
- `Organic` and `Hazardous` bins are visible and supported by the minigame/server mapping for future items, but current main quest cleanup mappings do not yet place those categories in the bag.
- If changing cleanup visuals, update `TRASH_ASSET_VARIANTS` and `docs/V6/GREEN_AGAIN_V6_TRASH_ASSET_LIBRARY.md` together.

## 12. Imported Asset Scripts

Studio hien co nhieu script nam trong:

- `Workspace["=== GREEN AGAIN V5 ==="].SYSTEMS_REVIEW`
- `Workspace["=== GREEN AGAIN V5 ==="].UNSORTED_REVIEW`
- Imported door/vehicle/fixture/tree/model folders
- `Workspace.Trash` source assets, if new imported models include scripts

Examples observed:

- Door/gate/sampan floating scripts.
- Light/fixture scripts.
- Model scripts with generic names like `Script`, `MainScript`, `Blink`, `PoseTexture`.

Rule:

- Khong xem cac asset script nay la game architecture chinh cua V6.
- Khong sua hang loat asset script neu task la story/quest/HUD.
- Trong `Workspace.Trash`, imported asset scripts should stay disabled unless their behavior is explicitly needed and documented.
- Neu mot asset script gay loi runtime, ghi ro path va log, sua dung script do, khong refactor lan sang story runtime.
- Neu chuyen asset thanh gameplay-critical object, cap nhat file nay va implementation summary.

## 12.5 Temporary Ch5 NPC Placeholders

Current runtime still targets `Workspace["=== GREEN AGAIN V5 ==="]`. Until real models for Cô Hạnh and Em Phúc are added under `MAP_ROUTE.06_NPCs`, `StoryRuntimeMVP.getNpc()` creates visible placeholder NPC models under `Workspace.GreenAgainV5_ClientAnchors`.

Rules:

- Placeholder names are `NPC_CoHanh` and `NPC_EmPhuc`.
- The model itself carries `GreenAgainKind="NPC"`, `NpcId`, `InteractId`, `ObjectName`, `Action`, and `Interactable`; child visual parts do not carry the interact id.
- Placeholder visuals use simple anchored parts plus a nameplate, not invisible-only anchors.
- Default residential-lane positions are `CoHanh = Vector3.new(248.0, 51.15, -3370.0)` and `EmPhuc = Vector3.new(252.0, 51.15, -3370.0)`.
- `Q5_05_ResidentialAfterRain` stages both placeholders on the residential lane; `CoHanh` is the interactable quest target.
- `Q5_06_CareSmallLives` stages both placeholders beside the placement markers at `(242.0, 51.15, -3382.0)` and `(250.0, 51.15, -3382.0)` so they do not overlap the care-corner markers.
- Runtime verification: placeholder bottom Y was `48.350` against road ground `48.345` in both Q5.05 and Q5.06.

## 13. How To Add A New Quest Step

Truoc khi code:

1. Xac nhan quest trong `GDD_GreenAgain_v6_QUEST_FLOW.md`.
2. Xac nhan location trong `GDD_GreenAgain_v6_CURRENT_MAP_DRAFT.md`.
3. Xac nhan dialogue trong `GDD_GreenAgain_NPC_DIALOGUE_v6.md`.
4. Viet plan logic/cau truc code ngan.

Trong code:

1. Them quest vao `QUESTS`.
2. Them id vao `ORDER` neu can theo thu tu.
3. Them dialogue vao `DIALOGUES` neu quest la dialogue-driven.
4. Them `NOTEBOOK` entry neu chapter moi can unlock.
5. Neu la cleanup, them `QUEST_CLEANUP_POSITIONS`.
6. Neu la NPC/location moi, them `NPCS`, `LOCATION_PATHS`, fallback, display name va tag trong `tagWorld()`.
7. Neu la target runtime moi, mo rong spawn function tuong ung.
8. Dam bao `buildObjective()` tra dung `displayName`, `interactId`, `position`.
9. Dam bao `onInteract()` route ve dung handler.
10. Test Play mode.

Khong lam:

- Khong complete quest tren client.
- Khong tao duplicate marker/HUD.
- Khong spawn placeholder map location neu object that da ton tai.
- Khong bo qua dialogue chi de di nhanh hon.

## 14. How To Add A New Gameplay Activity

Moi gameplay activity moi phai co mini-spec truoc khi code:

```text
Activity name:
Quest unlock:
Map object / runtime object:
TargetType:
GreenAgainKind:
InteractId pattern:
Prompt Action:
Completion count/rule:
State fields needed:
RemoteEvents used:
HUD/marker behavior:
Test cases:
```

Neu activity la bien the cua cleanup/sorting/placement/community, uu tien mo rong handler hien co. Chi tao handler moi khi co interaction semantics that su khac.

## 15. Test Checklist For Code Structure Changes

Sau khi sua code trong Roblox:

- Play mode khong co MVP script error moi.
- `StoryRuntimeMVP ready with ... quest states` xuat hien neu runtime load dung.
- `StoryClientMVP ready` xuat hien tren client.
- Main menu van hien va PLAY van dua player ve map.
- Story HUD chi hien sau khi vao map chinh.
- Current objective co dung mot marker.
- Marker khong co distance text.
- Prompt hien dung `Action - ObjectName`.
- NPC dialogue mo/dong mot lan, khong double-complete.
- Choice dialogue khong bi ket.
- Cleanup/sorting/placement/community count dung.
- Runtime props spawn gan mat dat.
- Cong khong interactable truoc quest cua no.
- Post-ending free roam an tracker/marker.
- Neu co console noise tu imported asset, tach rieng voi loi MVP.

Trash asset library checks:

- `Workspace.Trash` exists as exactly one root `Folder`.
- Source templates under `Workspace.Trash` keep `Interactable=false`.
- No enabled `Script` or `LocalScript` remains inside `Workspace.Trash` unless documented.
- Runtime clones, if used, are created under `Workspace.GreenAgainV5_StoryRuntime`.

## 16. Handoff Requirements

Moi lan sua code/gameplay, handoff phai noi ro:

- Script/folder da sua.
- Logic da them/sua.
- Quest/dialogue/map docs da doc.
- Test da chay.
- Console errors/noise con lai.
- Summary doc nao da cap nhat.

Neu chi sua docs nhu file nay, khong can cap nhat MVP implementation summary vi khong doi behavior trong Studio.
