# Green Again v5 - Implementation Blueprint

> Blueprint này chuyển v5 từ docs sang Roblox implementation. Ưu tiên: story flow, dialogue, cutscene, marker. Cleanup mechanics chỉ phục vụ story.

## 1. Implementation Order

1. Data model v5: chapters, quests, NPC dialogue states.
2. Objective marker system thay scanner.
3. Dialogue UI/data loading.
4. Cutscene/event sequencer.
5. Chapter 1 end-to-end.
6. Chapter 2-4 story route.
7. Chapter 5 + ending.
8. NPC phụ + ambient polish.
9. Post-ending free roam.

## 2. Folder/Data Proposal

```text
ReplicatedStorage.GreenAgain
  Data
    QuestData
    DialogueData
    CutsceneData
    NotebookData
  Events
    OnQuestStarted
    OnQuestCompleted
    OnDialogueStarted
    OnDialogueEnded
    OnCutsceneStarted
    OnCutsceneEnded
    OnNotebookEntry
    OnObjectiveMarker

ServerScriptService.GreenAgain
  QuestManager
  DialogueService
  CutsceneService
  StoryStateService
  ObjectiveMarkerService

StarterGui
  DialogueGui
  NotebookGui
  QuestTracker
  Letterbox/CutsceneOverlay
```

## 3. Story State

Minimum server state per player:

```lua
{
    chapter = 1,
    currentQuestId = "Q1_01_ArriveVenSong",
    completedQuests = {},
    storyFlags = {
        metBacXanh = false,
        groceryCleaned = false,
        fieldCleaned = false,
        riverUnderstood = false,
        drainCleared = false,
        endingPlayed = false,
    },
    npcStates = {
        BacXanh = "BeforeQuest",
        CoTu = "BeforeQuest",
    },
    notebookEntries = {},
}
```

## 4. QuestManager Requirements

QuestManager must:

- Start quest by ID.
- Set objective text.
- Set objective marker target.
- Listen for completion events.
- Fire dialogue/cutscene when configured.
- Add notebook entry on completion.
- Advance to next quest.

Avoid:

- Quest progress hidden inside trash pickup scripts only.
- Multiple unrelated objectives on screen.
- Chapter transitions without dialogue.

## 5. Dialogue System Requirements

Dialogue should be data-driven:

```lua
DialogueData[NpcId][StateOrQuestId] = {
    speaker = "Bác Xanh",
    lines = {...},
    choices = optional,
    onComplete = "CompleteQuest",
}
```

Need support:

- Speaker name.
- Multiple lines.
- Optional 2-choice response.
- Typewriter or simple text reveal.
- Continue button.
- Lock movement optional during important scenes.
- Camera focus optional.

## 6. Cutscene System Requirements

CutsceneService should support simple steps:

```lua
{
    {type = "Fade", value = "In", duration = 0.6},
    {type = "CameraFocus", target = "NhaVanHoa_ThonNoiChuan", duration = 2.0},
    {type = "Dialogue", id = "CS1_BacXanhIntro"},
    {type = "SetObjective", questId = "Q1_03_CleanEntrance"},
}
```

MVP can be simple:

- Fade in/out.
- Letterbox.
- Camera look-at target.
- Dialogue sequence.
- Restore camera/player control.

## 7. Objective Markers

Replace scanner-first logic with objective markers:

- NPC marker: floating icon/name above NPC.
- Location marker: ring/beam at destination.
- Area marker: marker at center of cleanup zone.
- Placement marker: marker on exact spot.

Rules:

- Only current quest marker is prominent.
- Nearby interact prompts still work.
- Marker labels must use Vietnamese location names.

## 8. Chapter Build Checklist

### Chapter 1

- [ ] Ensure portal intro fires only after teleport to main map.
- [ ] Rename fiction from `Portal1Destination` to Spawner/lối vào Nhà văn hóa in UI.
- [ ] Add CS0 and CS1.
- [ ] Add Bác Xanh dialogue.
- [ ] Add Chị Lan/Điểm tập kết tutorial.
- [ ] Ensure first cleanup feels like evidence, not grind.

### Chapter 2

- [ ] Marker from Nhà văn hóa to Tạp hóa Cô Tư.
- [ ] Add Cô Tư dialogue states.
- [ ] Add village/tạp hóa trash cluster.
- [ ] Optional NPC phụ: Cô Hạnh, Em Phúc.
- [ ] Add notebook entry.

### Chapter 3

- [ ] Treat `PicnicArea` as `Sân bóng thôn Ven Sông` in UI.
- [ ] Add sân bóng trash cluster.
- [ ] Add Anh Tùng + Bé Na dialogue.
- [ ] Add placement/commitment near sân bóng.
- [ ] Optional NPC phụ: Dì Năm, Nam thủ môn, Cô Mai.

### Chapter 4

- [ ] Marker from sân bóng to Ông Sáu.
- [ ] Add bờ sông/river trash trail.
- [ ] Add Ông Sáu realization dialogue.
- [ ] Treat RiverNE/RiverBend as one continuous river story.
- [ ] Optional NPC phụ: Chú Lộc, Bà Tám.

### Chapter 5

- [ ] Treat `Dam_C1/C2/C3` as `Cống thoát nước cuối xóm` in UI.
- [ ] Add cống trash cluster and visual blockage.
- [ ] Add CS5A and CS5B.
- [ ] Implement Q5_03_GatherCommunity.
- [ ] Implement 2-3 prevention actions.
- [ ] Add ending gathering at Nhà văn hóa.
- [ ] Set post-ending state.

## 9. Content Migration From v4

Keep:

- Trash interaction base.
- Bin sorting if it works.
- Placement zones if useful.
- Existing NPC models as anchors.
- Portal intro system.

Change:

- Scanner becomes optional or removed from main flow.
- `PicnicArea` display name becomes `Sân bóng thôn Ven Sông`.
- `Dam_C1/C2/C3` display as `Cống thoát nước cuối xóm`.
- Quest text becomes story objectives.
- Chapter banners should be short and tied to cutscenes.

Remove/avoid:

- PL/pollution level as main player-facing text.
- Long static chapter text stuck on screen.
- Objectives that say only "Dùng scanner" or "Hoàn thành nhiệm vụ".

## 10. Acceptance Criteria

V5 MVP is acceptable when:

- Player can complete Chapters 1-5 in order.
- Every chapter has at least one meaningful NPC conversation.
- Every cleanup/placement action has a story reason.
- Cutscenes do not leave text stuck on screen.
- Player always knows where to go next.
- Ending triggers once and returns player to free roam.
- The story can be understood without reading external docs.

