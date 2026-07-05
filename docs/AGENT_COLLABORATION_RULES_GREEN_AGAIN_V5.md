# Green Again V5 - Agent Collaboration Rules

Date: 2026-07-03

Purpose: this file is the shared operating rulebook for Codex and any other agent working on the Green Again V5 Roblox project. Every agent should read this before editing the game, docs, or Roblox Studio workspace.

## 1. Single Source Of Truth

Use these documents as the current source of truth, in this priority order:

1. `docs/GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`
2. `docs/GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`
3. `docs/GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`
4. `docs/GDD_GreenAgain_v5_QUEST_FLOW.md`
5. `docs/GDD_GreenAgain_NPC_DIALOGUE_v5.md`
6. `docs/GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
7. `docs/GDD_GreenAgain_v5_STORY_BIBLE.md`
8. `docs/GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`

Do not use `docs/legacy_v4/` for new implementation unless the user explicitly asks for a v4 reference.

If docs conflict with the current Studio build, inspect the Studio build and document the difference before changing behavior.

## 2. Pre-Code Planning Gate

Before writing or editing Roblox code, every agent must do a short planning pass.

Required reading before code:

- `docs/AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`
- `docs/GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`
- `docs/GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`
- `docs/GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`
- The specific quest/dialogue/map/cutscene doc related to the change.

Required plan before touching scripts:

- What gameplay/story logic is being changed.
- Which existing script owns that behavior.
- Whether the change belongs in `StoryRuntimeMVP`, `StoryClientMVP`, `MainMenuController`, or a utility script.
- What data tables, RemoteEvents, Attributes, UI surfaces, and runtime folders are affected.
- How quest progression will start, update, complete, and recover from invalid interaction.
- What Play-mode tests will prove the change works.

Do not create real code first and explain architecture afterward. Plan the logic and code structure first, then implement.

## 3. Current Runtime Ownership

The current active MVP path is:

- Startup loader: `game.ReplicatedFirst.GreenAgainStartupLoader`
- Server: `game.ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP`
- Client: `game.StarterPlayer.StarterPlayerScripts.StoryClientMVP`
- Sprint: `game.StarterPlayer.StarterCharacterScripts.SprintStaminaScript`
- Team-owned waiting screen / main menu: `game.StarterGui.MainMenuGui.MainMenuController`

Deleted or obsolete systems must not be recreated:

- `GreenAgainHUD_V5`
- `GreenAgainObjectiveClient`
- `MapWiringBootstrap`
- Old connection label text: `Đang nối map Green Again V5...`

Before adding a new script, first check whether the behavior belongs in the existing active MVP scripts.

For code ownership details, read `docs/GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`.

Main menu ownership rule:

- `MainMenuGui` / `MainMenuController` is currently being worked on by another team member.
- Do not rewrite, delete, or visually redesign it unless the user explicitly assigns that task.
- Keep `GreenAgainStartupLoader` as a separate `ReplicatedFirst` guard unless the menu owner explicitly takes over startup loading.
- Story HUD and objective marker work should remain in `StoryClientMVP` and should not assume the menu has already been destroyed.
- If touching startup flow, verify that the menu still locks controls, restores controls after PLAY, and does not reintroduce duplicate HUD.

## 4. Multi-Agent Safety Rules

- Never revert another agent's or the user's changes unless the user explicitly asks.
- Before editing, check current state with `git status --short` and inspect the target script/doc.
- Keep edits scoped to the requested feature or bug.
- If another agent changed the same file, read the whole relevant section and merge with it instead of overwriting.
- Do not rename quest ids, object names, or paths casually. If a rename is necessary, update every reference and record it in the summary doc.
- Do not delete Studio objects unless the user explicitly asks.
- Prefer adding small, documented runtime systems over large rewrites.
- At the end of work, update `docs/GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md` with meaningful behavior changes and tests.

## 5. Roblox Studio Rules

- Always verify Studio mode before edits. If Play mode is running, stop it before editing persistent scripts.
- After implementation, run Play mode when possible and check the console.
- If console has existing unrelated imported asset noise, mention it separately from MVP script errors.
- Do not leave Play mode running when handing work back.
- Do not create placeholder locations for already existing map locations.
- Runtime interaction markers, sorting bins, trash, planting markers, and temporary gameplay objects are allowed when they are clearly gameplay affordances, not fake map locations.

## 6. Map And Object Rules

Use real objects already in `Workspace["=== GREEN AGAIN V5 ==="]`.

Important object mappings:

- `BacXanh`, `ChiLan`, `CoTu`, `AnhTung`, `BeNa`, `OngSau`: `MAP_ROUTE.06_NPCs`
- Nhà văn hóa: `NhaVanHoa_ThonNoiChuan`
- Điểm tập kết rác: `DiemTapKetRacThai_ThonVenSong`
- Tạp hóa Cô Tư: `TapHoaCoTu_HouseOnly_Rural`
- Sân bóng: map thật nằm quanh `KhungThanh_01_Marker` / `KhungThanh_02_Marker` nếu còn tồn tại; Chapter 3 interaction dùng runtime invisible anchor `FieldCenter` ở trung tâm sân, không phụ thuộc holder khung thành.
- Cống thật: `SYSTEMS_REVIEW.Doors_Vehicles_And_AssetScripts.OngThoatNuoc`

Current important gameplay coordinates:

- Nhà văn hóa hub: `(284.24, 51.85, -3570.00)`
- Điểm tập kết rác / `TrashSite`: `(93.57, 51.52, -3533.43)` for gameplay marker/interact hitbox. The visible sorting station is higher/around this area, but runtime interaction should stay ground-reachable.
- Tạp hóa: `(78.78, 49.45, -3187.65)`
- Sân bóng A: `(-67.07, 51.55, -3225.84)`
- Sân bóng B: `(-51.72, 56.05, -3390.71)`
- Trung tâm sân bóng / `FieldCenter`: `(-59.66, 55.45, -3309.73)`
- Bờ sông Ch4: `(-160.482, 51.689, -3571.701)`
- Gần cống Ch4: `(-198.184, 51.689, -3502.522)`
- Gần bờ sông Ch4: `(-204.840, 54.054, -3481.669)`
- Cống Ch5: `(-221.32, 45.50, -3507.80)`

If the user provides a new coordinate, prefer using it directly and record it in the summary.

## 7. Story And Quest Rules

Green Again V5 is story-first. Do not reduce it to a generic cleanup simulator.

Keep the intended route:

1. Nhà văn hóa / Bác Xanh
2. Điểm tập kết rác / Chị Lan
3. Tạp hóa Cô Tư
4. Sân bóng / Anh Tùng / Bé Na
5. Ông Sáu / bờ sông
6. Cống thoát nước
7. Community prevention
8. Ending at Nhà văn hóa
9. Post-ending free roam

Current expanded MVP loops:

- Trash appears as ambient pollution at game start.
- Cleanup activates only the current quest's trash.
- Collected trash goes into a runtime bag by category.
- Sorting quests spawn bins at the real trash collection point.
- Final prevention includes placing a bin, placing a reminder sign, and planting a tree near the village area beside Nhà văn hóa.

Do not skip dialogue beats to speed up implementation. If a gameplay loop is added, place it between story beats where it makes narrative sense.

## 8. Dialogue Rules

- Use Vietnamese dialogue.
- Use existing V5 dialogue docs first.
- New dialogue should match the tone: grounded, gentle, community-focused, not preachy.
- Choices must not break progression.
- Choice UI rules:
  - Choices appear only when the dialogue reaches the choice point.
  - Continue is disabled or hidden while a choice is required.
  - Choosing an option should either add a player line or branch clearly.
  - Closing a dialogue should complete a quest only once.
- Avoid duplicate reopen bugs by using debounce and server-side dialogue sessions.

## 9. UI/UX Rules

- Marker shows only the current objective.
- Marker is a small green diamond plus name.
- No distance text.
- Marker and tracker appear only after the player reaches or teleports into the main map.
- Hide marker while dialogue is open, then restore it if the objective remains active.
- Do not reintroduce the old top-left connection text.
- Keep UI compact and readable.
- Do not add tutorial walls or large explanatory panels unless the user asks.
- Do not update prompt text/visibility every frame if the target/text did not change.

## 10. Gameplay Rules

Allowed MVP gameplay systems:

- Interact with NPCs and map targets.
- Pick up trash into a bag.
- Sort trash by category at the collection point.
- Place bins/signs/reminders.
- Plant trees.
- Gather community members.
- Lightweight cutscene/fade/focus moments.

Avoid heavy systems unless requested:

- Complex minigames.
- Full inventory UI.
- Economy/rewards.
- Combat or unrelated movement mechanics.
- Large procedural systems.
- Uncached per-frame scans over Workspace or large descendants.

If adding a new gameplay activity, define:

- Where it happens.
- Which quest unlocks it.
- What object the marker points to.
- What action text appears in the prompt.
- How completion is counted.
- How it affects story progression.

## 11. Assets And Models

- Prefer real map objects already in the workspace.
- Runtime generated trash or markers are allowed as gameplay props.
- Do not import unknown marketplace assets blindly.
- If using external Roblox assets, record the asset id/source and verify permission.
- If asset import fails due to permissions, keep the native fallback and report it.
- Do not replace user-made map objects without permission.

## 12. Testing Checklist

For every meaningful implementation, test as much as possible:

- Studio enters Play mode without new MVP script errors.
- Player reaches main map and UI appears only there.
- Current objective has exactly one marker.
- Marker has no distance.
- Interaction prompt points to the correct active object.
- Dialogue opens once and closes once.
- Choice dialogue does not get stuck.
- Quest advances to the correct next quest.
- Runtime props spawn at grounded, believable positions.
- Cống is not interactable before its quest.
- Post-ending free roam hides tracker/marker.
- Normal gameplay CPU does not spike compared with dialogue-open state.
- If a change touches interaction scan/UI prompt, verify it uses caching/throttling rather than `workspace:GetDescendants()` every frame.

Record test results in the summary doc.

## 13. Performance Rules

- Never add `workspace:GetDescendants()` or other large tree scans inside `Heartbeat`, `RenderStepped`, or per-frame UI loops.
- Interactable detection belongs in `StoryClientMVP`'s cached target list using `InteractId`, `DescendantAdded`, `DescendantRemoving`, and throttled nearby checks.
- Do not set `Humanoid.WalkSpeed`, UI text, UI visibility, marker contents, or prompt strings every frame if the value did not change.
- Dialogue should not be the only state where the game runs smoothly. If performance improves while dialogue is open, inspect code paths skipped by `dialogueOpen`.
- If a performance fix changes runtime code structure, update both `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md` and `GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`.

## 14. Documentation Rules

When changing behavior, update:

- `docs/GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`

When changing collaboration process, update:

- `docs/AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`

When changing Roblox code structure, ownership, RemoteEvents, Attributes, or runtime folders, update:

- `docs/GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`

When adding a major new design system, create a focused doc under `docs/` and link it from the summary.

Keep docs in Vietnamese when they are user-facing game design docs. This collaboration rulebook can stay in English for agent clarity, but Vietnamese notes are welcome when describing user-facing behavior.

## 15. Handoff Format

Every agent should end with a concise handoff:

- What changed.
- Which scripts/docs were touched.
- What was tested.
- Any known unrelated console noise.
- Any questions or assumptions.

If blocked, say exactly what is missing, for example:

- Need user-provided coordinate.
- Need asset id/link.
- Need confirmation before deleting/replacing an object.

## 16. Open Questions To Ask The User When Needed

Ask before making risky assumptions about:

- Exact placement of new gameplay locations.
- Whether a new object should be permanent in the map or runtime-only.
- Whether imported assets are allowed and which asset ids to use.
- Whether dialogue should branch meaningfully or only reflect player tone.
- Whether a new gameplay loop should be mandatory in the main quest or optional in free roam.

Do not ask if the answer can be safely inferred from the current V5 docs and workspace.
