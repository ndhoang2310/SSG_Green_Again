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

- `StarterPlayer.StarterCharacterScripts.SprintStaminaScript`, but with stamina UI removed.

## Story And Quest Flow

Implemented the MVP quest route from Chapter 1 through post-ending free roam:

- `Q1_01_ArriveVenSong`
- `Q1_02_MeetBacXanh`
- `Q1_03_CleanEntrance`
- `Q1_04_SortFirstTrash`
- `Q2_01_ToGrocery`
- `Q2_02_ObserveVillageTrash`
- `Q2_03_CleanGrocery`
- `Q2_04_GroceryCommitment`
- `Q3_01_ToFootballField`
- `Q3_02_TalkAnhTung`
- `Q3_03_CleanField`
- `Q3_04_BeNaMoment`
- `Q3_05_FieldReminder`
- `Q4_01_ToRiver`
- `Q4_02_FollowRiverTrash`
- `Q4_03_RiverRealization`
- `Q5_01_FindDrain`
- `Q5_02_ClearDrain`
- `Q5_03_GatherCommunity`
- `Q5_04_PreventReturn`
- `Q5_05_ReturnToCommunityHouse`
- `PostEnding_FreeRoam`

Implemented systems:

- Per-player story state with current quest, chapter, cleanup counts, placement counts, community progress, notebook flags, and ending flag.
- Quest start and completion.
- Dialogue-driven quest completion.
- Interaction routing for NPCs, locations, trash, placement actions, and drain cleanup.
- Runtime trash spawning for cleanup quests when needed.
- Runtime placement markers for MVP prevention/placement actions.
- Notebook toast once per chapter.
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
- Notebook toast.
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

## Stamina / Sprint

Changed `SprintStaminaScript`:

- Removed the visible stamina bar UI.
- Removed `StaminaGui` creation.
- Kept sprint logic.
- Player can still hold Shift to run faster.
- Walk speed still changes from default speed to sprint speed.

## Height And Position Fixes

Fixed the early-game marker/trash height issue:

- The first objective marker no longer uses the high pivot of the `NhaVanHoa_ThonNoiChuan` model.
- Hub gameplay position now uses a grounded override near the actual player surface.
- First cleanup trash around Nhà văn hóa now spawns near ground height instead of floating.

Validated values during Play:

- Hub marker around `284.24, 51.85, -3570`.
- Q1 cleanup trash around `Y ~= 52.2`.

## Deleted Legacy Pieces

Deleted old MVP wiring pieces to avoid duplicate UI and duplicate behavior:

- Old HUD: `GreenAgainHUD_V5`
- Old client objective script: `GreenAgainObjectiveClient`
- Old server bootstrap: `MapWiringBootstrap`

The current active MVP path is:

- Server: `StoryRuntimeMVP`
- Client: `StoryClientMVP`

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
- Verified sprint script still exists and keeps Shift sprint behavior.
- Verified Q1 marker and trash use corrected ground-level positions.

Known unrelated console noise from imported assets remained, including texture permission and existing asset script warnings. These were not introduced by the MVP story scripts.

