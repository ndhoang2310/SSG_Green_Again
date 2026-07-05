# Green Again V5 MVP Implementation Summary

Date: 2026-07-02

## Scope

Built the Green Again V5 MVP as a story-first vertical slice using the existing Roblox Studio workspace and current V5 docs:

- `GDD_GreenAgain_v5_QUEST_FLOW.md`
- `GDD_GreenAgain_NPC_DIALOGUE_v5.md`
- `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`
- `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
- `GDD_GreenAgain_v5_STORY_BIBLE.md`

The implementation uses the real map objects already present in `Workspace["=== GREEN AGAIN V5 ==="]`. It does not create placeholder locations for the football field or drain.

## Main Runtime Added

Added:

- `ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP`
- `StarterPlayer.StarterPlayerScripts.StoryClientMVP`

Removed old wiring sources:

- `StarterGui.GreenAgainHUD_V5`
- `StarterPlayer.StarterPlayerScripts.GreenAgainObjectiveClient`
- `ServerScriptService.GreenAgainProject.Runtime_To_Add.MapWiringBootstrap`

Kept:

- `StarterPlayer.StarterCharacterScripts.SprintStaminaScript`, rebuilt as simple Shift sprint with no stamina drain, recovery, cooldown, or sprint time limit.

## Story And Quest Flow

Implemented the MVP quest route from Chapter 1 through post-ending free roam:

- `Q1_01_ArriveVenSong`
- `Q1_02_MeetBacXanh`
- `Q1_03_CleanEntrance`
- `Q1_04_SortFirstTrash`
- `Q1_05_MeetChiLan`
- `Q2_01_ToGrocery`
- `Q2_02_ObserveVillageTrash`
- `Q2_03_CleanGrocery`
- `Q2_04_SortGroceryTrash`
- `Q2_05_GroceryCommitment`
- `Q2_06_TalkToBacXanh`
- `Q3_01_ToFootballField`
- `Q3_02_TalkAnhTung`
- `Q3_03_CleanField`
- `Q3_04_SortFieldTrash`
- `Q3_05_BeNaMoment`
- `Q3_06_FieldReminder`
- `Q4_01_ToRiver`
- `Q4_02_FollowRiverTrash`
- `Q4_03_SortRiverTrash`
- `Q4_04_RiverRealization`
- `Q5_01_FindDrain`
- `Q5_02_ClearDrain`
- `Q5_03_SortDrainTrash`
- `Q5_04_GatherCommunity`
- `Q5_05_PreventReturn`
- `Q5_06_ReturnToCommunityHouse`
- `EndingSequence`
- `PostEnding_FreeRoam`

Implemented systems:

- Per-player story state with current quest, chapter, cleanup counts, placement counts, community progress, notebook flags, and ending flag.
- Quest start and completion.
- Dialogue-driven quest completion.
- Interaction routing for NPCs, locations, trash, placement actions, and drain cleanup.
- Runtime trash spawning for cleanup quests when needed.
- Runtime placement markers for MVP prevention/placement actions.
- Notebook book/panel once per chapter: each unlocked chapter becomes a page, opens automatically on unlock, and can be reopened with the `Nhật ký` button or `N`.
- Ending text after the final dialogue.

## Dialogue

Added data-driven dialogue for the main V5 route:

- Bác Xanh intro
- Chị Lan sorting explanation
- Cô Tư intro and after-cleanup commitment
- Anh Tùng and Bé Na football field sequence
- Ông Sáu river sequence
- Drain realization with Bác Xanh and Chị Lan
- Community gather reactions from Cô Tư, Anh Tùng, Ông Sáu, Chị Lan
- Ending dialogue with Bác Xanh, Chị Lan, Cô Tư, Anh Tùng, Ông Sáu, Bé Na

Dialogue supports:

- Multiple lines
- Speaker names
- Simple choices
- Continue by pressing `E` or the continue button
- Debounce so completed dialogue does not immediately reopen

## Map Object Mapping

Used existing objects:

- `BacXanh`, `ChiLan`, `CoTu`, `AnhTung`, `BeNa`, `OngSau` from `MAP_ROUTE.06_NPCs`
- `NhaVanHoa_ThonNoiChuan`
- `DiemTapKetRacThai_ThonVenSong`
- `TapHoaCoTu_HouseOnly_Rural`
- `KhungThanh_01_Marker`
- `KhungThanh_02_Marker`
- `NPC_OngSau_Marker`
- `OngThoatNuoc`

Chapter 3 sân bóng interaction update:

- Holder/marker khung thành có thể bị xóa hoặc không tương tác được.
- `Q3_01_ToFootballField`, `Q3_03_CleanField`, and `Q3_06_FieldReminder` now use `FieldCenter` instead of `FieldA`.
- `FieldCenter` is an invisible runtime interaction anchor at `(-59.66, 55.45, -3309.73)`, placed at the center of the real football field.
- This anchor is only for interaction/marker routing; it is not a visual placeholder for the field.

Drain object:

- Uses `Workspace["=== GREEN AGAIN V5 ==="].SYSTEMS_REVIEW.Doors_Vehicles_And_AssetScripts.OngThoatNuoc`
- Kept anchored.
- Only becomes relevant/interactable in Chapter 5.

## Objective Marker And HUD

Implemented a new client HUD:

- Quest tracker with chapter, quest title, and objective.
- Interaction prompt.
- Dialogue panel.
- Feedback toast.
- Notebook book with previous/next page navigation.
- End overlay.

Marker behavior:

- Only one active marker at a time.
- Marker is a small green diamond with the target name.
- No distance text.
- Marker appears only when the player has reached/teleported into the main map area.
- Marker and tracker are hidden while the player is still in the connection/lobby area.

Removed the old top-left text:

- Removed source scripts/UI that generated `Đang nối map Green Again V5...`.
- Verified no labels with that text spawn during Play.

## UI Polish

Updated the MVP UI to be smaller and cleaner:

- Quest tracker is less intrusive.
- Dialogue panel is wider and easier to read.
- Dialogue panel shows speaker and line progress, such as `1 / 4`.
- Prompt format changed to `[E]  Action - Object`.
- Toast and notebook UI made visually consistent with the new HUD.
- Added responsive scale for smaller screens.
- Added a lightweight CS0 intro overlay when the player first enters the main map.
- Added dialogue advance debounce so repeated `E` presses do not skip lines too quickly.
- Fixed dialogue choices:
  - Choice buttons no longer appear from the first dialogue line.
  - Choices appear only on the final dialogue line.
  - The continue button is hidden while a choice is required.
  - Clicking a choice inserts it as a player line before the dialogue closes.
- Pressing `E` while choices are shown selects the first choice so keyboard play does not get stuck.
- Post-ending free roam now hides the tracker and removes the objective marker.

## Main Menu / Waiting Screen

Observed in Roblox Studio on 2026-07-03:

- `StarterGui.MainMenuGui.MainMenuController` now exists and appears to be the team's current waiting screen / main menu work.
- This is separate from the story HUD in `StoryClientMVP`.
- `ReplicatedFirst.GreenAgainStartupLoader` now shows a Green Again logo loading screen before the waiting screen is ready.
- Startup loader behavior:
  - Calls `ReplicatedFirst:RemoveDefaultLoadingScreen()`.
  - Shows logo asset `rbxassetid://112991523200169` on a dark green loading screen.
  - Waits for `MainMenuGui.LogoImage`, `Workspace.MainMenuAssets.PlayBtn`, and `Workspace.MainMenuAssets.SetBtn`.
  - Fades out after the menu is ready, with a max wait fallback.
  - Writes QA attributes on `PlayerGui`: `GreenAgainStartupLoaderShown`, `GreenAgainStartupLoaderReady`, `GreenAgainStartupLoaderDuration`, `GreenAgainStartupLoaderClosed`.
- Current behavior from the script:
  - Holds the player in place during menu by anchoring the character at the menu scene, while leaving PlayerModule input state alive.
  - Uses a scriptable camera at roughly `(-249.381, 49.143, -3296.098)`.
  - Creates runtime `Workspace.MainMenuAssets`.
  - Adds a 2D logo image with asset id `rbxassetid://112991523200169`.
  - Animates floating menu models such as `Noob` and `honda cub` if present.
  - Spawns decorative water droplets and leaves.
  - Creates 3D `PLAY` and `SETTING` buttons with `ClickDetector`.
  - Uses a separate `TransitionOverlay` ScreenGui for fade in/out when pressing PLAY.
  - On PLAY, moves the character to the real waiting-island `SpawnLocation` before unanchoring/restoring physics.
  - Hides `MainMenuGui`, destroys `MainMenuAssets`, restores controls, and returns camera to custom mode after PLAY.
- Bug fix:
  - The old PLAY transition could unanchor the character near the menu scene, causing the player to fall and die before respawning.
  - `MainMenuController` now resolves `Workspace["=== GREEN AGAIN V5 ==="].MAP_ROUTE.00_Spawn_And_Teleport.SpawnLocation` and pivots the character to that safe spawn plus a small Y offset before physics resumes.
  - Character velocity is reset during the transition to avoid carried falling momentum.
  - `MainMenuController` no longer disables/re-enables PlayerModule controls while the menu is open. The character is held in place by anchoring, while PlayerModule keeps receiving normal key up/down events. This avoids stale WASD/jump states after PLAY.
  - On PLAY, the script only clears any pending ClickToMove path from the 3D PLAY click, then unanchors the character and restores the camera/humanoid. Do not force `DevComputerMovementMode` or add delayed control resets; both can make movement lock or drift.
- Story UI gating:
  - `StoryClientMVP` treats `MainMenuGui` as an active menu guard only while the GUI is still enabled.
  - While enabled `MainMenuGui` exists, quest tracker, prompt, touch button, dialogue panel, notebook book/panel, and objective marker are forced hidden.
  - After PLAY, the story UI still stays hidden on the waiting island.
  - Quest tracker and objective marker appear only after the player reaches the main island activation zone.
- Ownership note:
  - Treat this menu as teammate-owned work.
  - Other agents should not replace or refactor `MainMenuGui` / `MainMenuController` unless explicitly asked.
  - Any story HUD changes should remain in `StoryClientMVP` and avoid interfering with the menu flow.

## Stamina / Sprint

Changed `SprintStaminaScript`:

- Removed the visible stamina bar UI.
- Removed `StaminaGui` creation.
- Removed stamina drain, stamina recovery, cooldown, and sprint exhaustion logic.
- Player can hold Left Shift or Right Shift to run faster for as long as Shift is held.
- Walk speed now toggles directly between default speed `16` and sprint speed `25`.
- Sprint is event-based: it changes speed only on Shift press/release, not every Heartbeat.

## Height And Position Fixes

Fixed the early-game marker/trash height issue:

- The first objective marker no longer uses the high pivot of the `NhaVanHoa_ThonNoiChuan` model.
- Hub gameplay position now uses a grounded override near the actual player surface.
- First cleanup trash around Nhà văn hóa now spawns near ground height instead of floating.

Validated values during Play:

- Hub marker around `284.24, 51.85, -3570`.
- Q1 cleanup trash around `Y ~= 52.2`.

## Doc-Driven Patch From Full Build Guide

Applied after `GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md` was created:

- Added `BacXanh_Q1_AfterClean`, a short after-cleanup beat before sending the player to Chị Lan.
- Changed Q5 community gather to require the three main return visits from Cô Tư, Anh Tùng, and Ông Sáu.
- Kept Chị Lan's Q5 role in the drain aftermath and ending, without requiring her as the fourth gather target.
- Sent a `freeRoam` objective payload after ending so `StoryClientMVP` hides tracker/marker cleanly.
- Extended gameplay positions for TrashSite, Grocery, FieldA, FieldB, FieldCenter, River, and Drain so runtime markers/trash/placements use grounded map locations.
- Objective marker for cleanup and placement quests now follows the current uncollected trash or unplaced action instead of only pointing at the broad area.
- Added explicit cleanup spawn positions for Ch4 river trash and Ch5 drain trash, so those clusters no longer rely on broad area offsets.
- Changed cleanup trash from quest-time spawning to ambient pollution:
  - Trash for all cleanup chapters now appears at game start.
  - Trash starts as visible but non-interactable environmental pollution.
  - When the related cleanup quest begins, only that quest's trash becomes interactable.
  - Collected trash is hidden so the area visibly gets cleaner.
- Replaced single-block trash visuals with Roblox-native composite trash models:
  - Trash bag: body lumps + tied top.
  - Plastic bottle: body + neck + cap.
  - Metal can: body + top + bottom.
  - Snack wrapper/paper: sheet + colored edge + label.
- Added trash category attributes for future sorting gameplay:
  - `Mixed`
  - `Plastic`
  - `Metal`
  - `Paper`
- Collected trash now records into the player's runtime bag by category before disappearing.
- Added lightweight runtime NPC staging:
  - Bác Xanh can appear near the river during Ông Sáu's story beat.
  - Bác Xanh and Chị Lan can appear near the drain for the Ch5 drain aftermath.
  - Bác Xanh, Chị Lan, Cô Tư, Anh Tùng, Ông Sáu, and Bé Na stage around Nhà văn hóa for the ending.
- Dialogue now hides the objective marker while open and restores it after close if the quest is still active.
- Added `TouchInteractButton` for touch/mobile interaction while keeping keyboard `E`.

## Gameplay Expansion Patch

Expanded the MVP loop after the user requested deeper gameplay:

- Added sorting quests after cleanup chapters:
  - `Q1_04_SortFirstTrash`
  - `Q2_04_SortGroceryTrash`
  - `Q3_04_SortFieldTrash`
  - `Q4_03_SortRiverTrash`
  - `Q5_03_SortDrainTrash`
- Trash now works as a simple carried bag system:
  - Collected trash increments the player's runtime bag by category.
  - Categories are `Plastic`, `Metal`, `Paper`, and `Mixed`.
  - Sorting quests spawn four runtime bins at the real trash collection point.
  - Interacting with the correct bin empties that category from the bag.
  - A sorting quest completes only after the bag is empty.
- Expanded the final prevention quest:
  - It now requires 3 actions instead of 2.
  - Place a trash bin near Cô Tư's grocery.
  - Place a reminder sign near the football field.
  - Plant a young tree in the village area beside Nhà văn hóa.
- Added a simple runtime tree visual:
  - Before interaction it is a planting marker.
  - After interaction it becomes a trunk plus green crown.

## Trash Asset Library

Structured the new `game.Workspace.Trash` asset folder so future runtime work can reuse imported trash models safely.

Current purpose:

- `Workspace.Trash` is a source asset library and scene-dressing holder.
- Active quest trash, bins, and placement props should still be spawned/cloned into `Workspace.GreenAgainV5_StoryRuntime`.
- Source templates in `Workspace.Trash` keep `Interactable=false` so `StoryClientMVP` does not treat them as live quest targets.

Current structure:

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

Important details:

- There was previously a duplicate root name issue: one `Workspace.Trash` was a `Model`, another was a `Folder`.
- The root is now a single `Folder`.
- The old placed trash scene was preserved under `Workspace.Trash.ScenePlacements.LegacyTrashScene_CongArea`.
- Imported scripts inside trash source assets were disabled, not deleted.
- Template attributes now include `GreenAgainV5`, `GreenAgainAssetRole`, `GreenAgainKind`, `TrashCategory`, `ObjectName`, `Action`, and `Interactable=false`.
- Full usage rules are documented in `docs/GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md`.

Runtime replacement patch on 2026-07-04:

- `StoryRuntimeMVP` now clones cleanup trash visuals from `Workspace.Trash.Collectibles` instead of building old primitive part models.
- `StoryRuntimeMVP` now clones sorting bin visuals from `Workspace.Trash.Props.Bins.TrashCan_P7` instead of using plain colored block bins.
- Each runtime clone is wrapped as a `Model`, tagged with `GreenAgainAssetRole="RuntimeClone"` and `SourceTrashTemplate`, and parented under `Workspace.GreenAgainV5_StoryRuntime`.
- Runtime clone placement uses bounding-box grounding: after pivoting to the quest position, the clone shifts so its bottom sits exactly on the configured spawn Y.
- Current cleanup mapping is documented in `docs/GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md`.

Cleanup diversity patch on 2026-07-04:

- Cleanup quests now spawn more varied visuals across all chapters: 10 items in Q1, 9 in Q2, 10 in Q3, 9 in Q4, and 9 in Q5.
- Dirt/stain cleanup visuals use `Workspace.Trash.Props.Piles` (`TrashPile_Part` or `TrashPile_Model`) instead of ad hoc primitive stains.
- Pile/stain runtime clones now support per-entry `rotation`, `preserveTemplateRotation`, and `heightOffset`. `TrashPile_Part` uses `CFrame.Angles(math.rad(90), 0, 0)`, while `TrashPile_Model` keeps its template rotation.
- Pile/stain runtime clones now use per-entry `heightOffset = -0.04`, placing the thin stain plane slightly into the ground so it does not appear to float.
- Runtime grounding now uses world-corner Y extents instead of `Model:GetBoundingBox()` height, which keeps rotated flat pile parts from floating above the ground.
- Mixed trash bag runtime clones now support per-entry `scale`; `TrashBag_BlackSmall` uses `1.45`, and `TrashBag_Garbage01` uses `1.25`.
- `Q1_03_CleanEntrance` trash spawn Y was corrected from the old floating height to `48.43`; normal Q1 clone bottoms sit at `48.43`, while Q1 pile bottoms sit around `48.39` because of `heightOffset = -0.04`.

Sorting minigame patch on 2026-07-04:

- Sorting quests no longer auto-sort a whole category when the player presses `E` on a bin.
- Interacting with any sorting bin opens a drag-and-drop minigame in `StoryClientMVP`.
- The UI shows the current bag items as visual 3D trash cards and four bins: `Nguy hiểm`, `Tái chế`, `Hữu cơ`, `Còn lại`.
- Each trash card uses a `ViewportFrame` preview cloned from the item's `Workspace.Trash` source template, so the minigame shows actual trash/pile models instead of text-only buttons.
- Pile previews use world-corner bounds and a higher angled camera so thin `Props.Piles` assets render visibly instead of edge-on.
- `PlasticBag_Crumpled` previews also use the higher angled camera so the crumpled plastic bag is framed visibly.
- `StoryRuntimeMVP` now tracks `state.bagItems` with each picked item's `category`, `name`, and `templatePath`.
- `StoryRuntimeMVP` validates each drop through `OnSortingMinigameSubmit`.
- Current mapping:
  - `Plastic`, `Metal`, `Paper` -> `Recycle` / `Tái chế`.
  - `Mixed` -> `Mixed` / `Còn lại`.
  - `Organic` -> `Organic` / `Hữu cơ`.
  - `Hazardous` -> `Hazardous` / `Nguy hiểm`.
- When the bag is empty, the server closes the minigame and completes the sorting quest.

## Deleted Legacy Pieces

Deleted old MVP wiring pieces to avoid duplicate UI and duplicate behavior:

- Old HUD: `GreenAgainHUD_V5`
- Old client objective script: `GreenAgainObjectiveClient`
- Old server bootstrap: `MapWiringBootstrap`

The current active MVP path is:

- Server: `StoryRuntimeMVP`
- Client: `StoryClientMVP`

## Performance Fixes

- Fixed a major client-side CPU issue in `StoryClientMVP`.
- Cause:
  - `findNearbyTarget()` previously called `workspace:GetDescendants()` every Heartbeat while normal gameplay was active.
  - When dialogue opened, `StoryClientMVP` returned early before that scan, which is why CPU dropped and lag stopped during conversations.
- Current behavior:
  - Interactable objects are cached by `InteractId`.
  - The cache is built once, updated from `workspace.DescendantAdded/DescendantRemoving`, and refreshed only occasionally as a fallback.
  - Nearby interaction checks are throttled to about 5-6 times per second instead of 60 times per second.
  - Prompt UI text/visibility is only updated when the target or text actually changes.
  - Old duplicate HUD cleanup now runs once instead of every Heartbeat.
- `SprintStaminaScript` no longer writes `Humanoid.WalkSpeed` every Heartbeat. Shift sprint is now event-based: speed changes only when Shift is pressed or released.
- Team rule: do not add `workspace:GetDescendants()`, large descendant scans, or repeated UI property writes inside `Heartbeat`/`RenderStepped` without caching and throttling.

## Test Results

Play tests performed:

- Verified fresh MVP flow can advance through the story route to `PostEnding_FreeRoam`.
- Verified only one objective marker appears.
- Verified marker has name only and no distance.
- Verified marker/tracker are hidden before entering the main map.
- Verified marker/tracker activate after teleporting to the main map.
- Verified old connection text no longer appears.
- Verified old HUD no longer spawns.
- Verified stamina UI no longer appears.
- Verified sprint script now has no stamina/cooldown variables and keeps direct Shift sprint behavior.
- Verified Q1 marker and trash use corrected ground-level positions.
- Lowered the client objective marker offset from `Vector3.new(0, 4.4, 0)` to `Vector3.new(0, 3.4, 0)` so the guide marker sits closer to the target.
- Removed the small fake trash/can props `BanSoanRac_ChongRacGia_1`, `BanSoanRac_ChongRacGia_2`, and `BanSoanRac_ChongRacGia_3` from the trash sorting station scene.
- Verified CS0 intro overlay appears after entering the main map.
- Verified Q1 after-cleanup Bác Xanh dialogue opens before `Q1_04_SortFirstTrash`.
- Verified free-roam objective payload hides tracker and removes marker.
- Verified cleanup marker points to runtime trash.
- Verified route can continue from Q4 through `PostEnding_FreeRoam` after the doc-driven patches.
- Verified ending staging moves all six main NPCs to ground-level positions around Nhà văn hóa.
- Updated Ch4 river gameplay/cleanup area to the real main-map river/drain-side coordinates provided by the user:
  - `(-160.482, 51.689, -3571.701)`
  - `(-198.184, 51.689, -3502.522)`
  - `(-204.840, 54.054, -3481.669)`
- Verified Ch4 river trash spawns at those three positions, with client streaming all three models after teleporting near the river area.
- Previously verified 16 ambient trash models existed at game start, with 53 visible child parts and `Interactable=false`; the 2026-07-04 diversity patch now maps 47 cleanup visuals total: Q1=10, Q2=9, Q3=10, Q4=9, Q5=9.
- Verified entering Q1 cleanup activates exactly 10 Q1 trash objects.
- Verified Q1 runtime clone bottoms use the corrected ground-level Y; normal Q1 clone bottoms sit at `48.43`, while Q1 pile bottoms sit around `48.39` because of `heightOffset = -0.04`.
- Q1 sorting visual cards use `ViewportFrame` previews with `WorldModel` children and template paths; after the diversity patch Q1 bag items include:
  - `Collectibles/Mixed/TrashBag_BlackSmall`
  - `Collectibles/Plastic/PlasticBottle_03`
  - `Collectibles/Metal/MetalCan_Crushed`
  - `Props/Piles/TrashPile_Part`
  - `Collectibles/Plastic/CandyWrapper`
  - `Collectibles/PaperCardboard/PaperSheet`
  - `Props/Piles/TrashPile_Model`
  - `Collectibles/PaperCardboard/CardboardBox_Carton`
  - `Collectibles/Plastic/PlasticBag_Crumpled`
  - `Props/Piles/TrashPile_Part`
- Fixed sorting drag alignment after visual cards were added:
  - Removed the old click-offset based drag positioning.
  - Drag clone now anchors at its center and follows the pointer using coordinates corrected by `StoryClientMVP`'s `ResponsiveScale`.
  - Verified Q1 sorting previously opened at UI scale `0.84765625`; current Q1 cleanup now feeds 10 visual items into the same centered drag path.
- Verified wrong submit `Plastic -> Mixed` keeps quest `Rác Đi Đâu?` active and reopens the minigame with retry text.
- Verified correct submits `Plastic -> Recycle`, `Metal -> Recycle`, `Mixed -> Mixed` close the minigame and advance to `Q1_05_MeetChiLan`.
- Verified collecting Q1 trash hides those objects while other ambient pollution remains visible.
- Verified collecting a plastic bottle marks only that model collected/invisible, while the nearby bag/can remain visible and interactable.
- Verified Q1 cleanup now leads into a sorting step at the trash collection point.
- Verified sorting bins spawn for `Q1_04_SortFirstTrash` and become the active objective marker.
- Verified sorting `Mixed`, `Plastic`, and `Metal` from the Q1 bag advances to `Q1_05_MeetChiLan`.
- Verified Cô Tư choice dialogue starts with choices hidden and continue visible.
- Verified Cô Tư choices appear only on the final line, with continue hidden while waiting for a choice.
- Verified the updated scripts start in Play mode without new `StoryRuntimeMVP` or `StoryClientMVP` errors.
- Verified while `MainMenuGui` exists:
  - `QuestTracker.Visible=false`
  - `InteractionPrompt.Visible=false`
  - `TouchInteractButton.Visible=false`
  - no local objective marker anchors are present.
- Verified the player remains alive at the waiting-island spawn after the menu safety fix:
  - health `100`
  - position near `(34.236, 17.351, -95.290)`
  - quest tracker still hidden.
- Simulated post-PLAY flow:
  - after `MainMenuGui` is removed, waiting island still has quest tracker hidden and no objective marker.
  - after moving to main island, quest tracker becomes visible and one `CurrentStoryObjectiveAnchor` marker is created.
- Verified `Workspace.Trash` has exactly one root folder after restructuring.
- Verified `Workspace.Trash` source templates have no descendants with `Interactable=true`.
- Verified no enabled `Script` or `LocalScript` remains inside `Workspace.Trash`.
- Verified Play mode spawns 16 cleanup trash clones from `Workspace.Trash` into `Workspace.GreenAgainV5_StoryRuntime`.
- Verified all spawned cleanup clones have `SourceTrashTemplate` pointing to the new library asset.
- Verified clone bottom Y matches the configured spawn Y for Q1, Q2, Q3, Q4 and Q5 cleanup trash.
- Verified an automated Q1 flow reaches `Q1_04_SortFirstTrash` and spawns 4 sorting bin clones from `Workspace.Trash.Props.Bins.TrashCan_P7`.
- `TrashSite` gameplay/interact Y was lowered to `51.52` so the green objective marker and sorting-bin interaction are reachable from the ground.
- Runtime sorting-bin world objects are now invisible `StorySortingBinHitbox_*` parts; visible bins come from the static sorting station scene, avoiding duplicate small bin/can props in front of the table.
- Verified startup loader in Play mode:
  - `GreenAgainStartupLoaderShown=true`
  - `GreenAgainStartupLoaderReady=true`
  - `GreenAgainStartupLoaderClosed=true`
  - duration was about `3.59s`
  - loader ScreenGui was destroyed after fade
  - `MainMenuGui` remained enabled with `LogoImage`, `PlayBtn`, and `SetBtn` ready.

Known unrelated console noise from imported assets remained, including texture permission and existing asset script warnings. These were not introduced by the MVP story scripts.

## Bug Fixes Patch (2026-07-05)

- Fixed floating trash height issues for Chapter 3 and Chapter 4:
  - Chapter 3 field trash spawn height is `48.23`, measured against local Terrain around `Y=48.203`.
  - Chapter 4 river trash spawn height is `48.23`, measured against local Terrain around `Y=48.203`.
  - Ch5 drain staging now puts Bác Xanh and Chị Lan on the dry bank with NPC pivot-height coordinates: `BacXanh = Vector3.new(-216.0, 53.58, -3512.0)`, `ChiLan = Vector3.new(-213.0, 53.36, -3510.0)`.
  - V6 Ch5 temporary NPCs now use visible placeholder models for `CoHanh` and `EmPhuc`, staged at ground-aligned residential-lane positions instead of invisible buried anchors.
- Updated placement visuals to hide the flat plane and render 3D models properly:
  - `setModelVisible` now hides `Decal`, `Texture`, and `SurfaceAppearance` to ensure the flat placeholder part becomes completely invisible.
  - The Chapter 3 Sign Board placement now spawns an actual 3D SignBoard (`Part` + `SurfaceGui` text) at the football field instead of a flat visual marker.
  - Changed football field sign placement coordinates to `Vector3.new(-126.278, 49.203, -3356.146)`.
- Split Bác Xanh's dialogue out from Cô Tư's after-grocery interaction to improve the flow:
  - Added a new quest `Q2_06_TalkToBacXanh` right after `Q2_05_GroceryCommitment`.
  - Added new dialogue entry `BacXanh_Q2_After` containing Bác Xanh's lines about the grocery store and football field.
  - Teleports Bác Xanh to stand at the new coordinates (`114.281, 67.989, -3310.235`) for this step before sending the player to Chapter 3.
