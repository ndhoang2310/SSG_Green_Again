# Green Again v5 - Detailed Implementation Plan

> Plan này dùng để build v5 trong Roblox theo hướng story-first. Mục tiêu không phải thêm nhiều mechanic, mà là làm người chơi hiểu chuyện qua cutscene, thoại, marker, rồi mới hành động.

## 0. Build Strategy

Build theo chiều dọc từng lát nhỏ:

```text
Foundation systems
-> Chapter 1 playable
-> Chapter 2 playable
-> Chapter 3 playable
-> Chapter 4 playable
-> Chapter 5 playable
-> ending
-> NPC phụ/polish
```

Không build toàn bộ hệ thống lớn rồi mới gắn story. Mỗi milestone phải có thể playtest từ đầu tới cuối phần đó.

## 1. Milestone M0 - Map Confirmation And Naming

Goal: khóa lại sự thật map trước khi code sâu.

Tasks:

- [ ] Kiểm tra teleport destination/spawn thật sau lobby.
- [ ] Nếu spawn không gần Nhà văn hóa, quyết định:
  - di chuyển destination về lối vào Nhà văn hóa, hoặc
  - sửa route docs cho khớp thực tế.
- [ ] Xác nhận `PicnicArea` visual là sân bóng.
- [ ] Xác nhận `Dam_C1/C2/C3` visual có thể đọc là cống thoát nước.
- [ ] Xác nhận đường đi: Nhà văn hóa -> điểm tập kết -> tạp hóa -> sân bóng -> Ông Sáu -> sông/cống.
- [ ] Tạo bảng mapping display name:
  - `PicnicArea` -> `Sân bóng thôn Ven Sông`
  - `ResidentialSt` -> `Thị trấn / làng Ven Sông`
  - `RiverNE` -> `Bờ sông chỗ Ông Sáu`
  - `RiverBend` -> `Khúc sông sau làng`
  - `Dam_C1/C2/C3` -> `Cống thoát nước cuối xóm`

Deliverable:

- Map route playtest: player có thể chạy theo tuyến bằng marker debug.
- Không còn UI story gọi sai công viên/picnic/đập.

## 2. Milestone M1 - Story Data Foundation

Goal: có data model để story điều khiển gameplay.

Data modules cần có:

```text
ReplicatedStorage.GreenAgain.Data.QuestData
ReplicatedStorage.GreenAgain.Data.DialogueData
ReplicatedStorage.GreenAgain.Data.CutsceneData
ReplicatedStorage.GreenAgain.Data.NotebookData
ReplicatedStorage.GreenAgain.Data.LocationData
```

Events cần có:

```text
OnQuestStarted
OnQuestCompleted
OnObjectiveChanged
OnDialogueStarted
OnDialogueEnded
OnCutsceneStarted
OnCutsceneEnded
OnNotebookEntry
OnStoryFlagChanged
```

Server services:

```text
QuestManager
DialogueService
StoryStateService
ObjectiveMarkerService
CutsceneService
NotebookService
```

Client controllers:

```text
DialogueController
QuestTrackerController
ObjectiveMarkerController
CutsceneController
NotebookController
InteractionController adapter
```

Acceptance:

- Server can set `currentQuestId`.
- Client receives objective text and marker target.
- Interacting with a target NPC can start dialogue by quest state.
- Dialogue completion can complete a quest.

## 3. Milestone M2 - Dialogue UI And Conversation Flow

Goal: dialogue đủ tốt để story là gameplay chính.

Required UI behavior:

- Speaker name.
- Multi-line continue.
- Optional player choices.
- Typewriter or clean text reveal.
- Skip/continue input.
- Movement lock for important scenes, optional for normal talk.
- Camera focus optional.
- Prevent repeated spam while dialogue active.

Data shape:

```lua
{
    id = "BacXanh_Q1_Intro",
    speaker = "Bác Xanh",
    lines = {
        {speaker = "Bác Xanh", text = "..."},
        {speaker = "Player", text = "..."},
    },
    choices = {
        {text = "...", next = "branchA"},
        {text = "...", next = "branchB"},
    },
    onComplete = {
        completeQuest = "Q1_02_MeetBacXanh",
        startQuest = "Q1_03_CleanEntrance",
    }
}
```

Acceptance:

- Implement được một cuộc nói chuyện 10-16 line mà không vỡ UI.
- Player có thể chọn 1 trong 2 response.
- Sau dialogue, quest/objective đổi đúng.

## 4. Milestone M3 - Objective Markers Instead Of Scanner

Goal: player luôn biết đi đâu mà không cần scanner.

Marker types:

| Type | Use |
|---|---|
| NPC | Gặp Bác Xanh, Cô Tư, Anh Tùng, Ông Sáu |
| Location | Đi tới Nhà văn hóa, sân bóng, cống |
| Area | Dọn rác quanh tạp hóa/sân bóng/bờ sông |
| Placement | Đặt thùng/biển/cây |

Rules:

- Chỉ marker chính nổi bật.
- Marker hiển thị tên Việt hóa.
- Nếu target xa, có icon/beam/arrow nhẹ.
- Khi player vào gần, marker nhỏ lại hoặc chuyển thành interaction prompt.

Acceptance:

- Quest `Gặp Cô Tư ở tạp hóa` dẫn đúng tới Cô Tư.
- Quest `Đi tới sân bóng` không hiện chữ `PicnicArea`.
- Quest `Đi tới cống thoát nước cuối xóm` không hiện chữ `Dam`.

## 5. Milestone M4 - Cutscene Foundation

Goal: có cutscene ngắn, không text stuck, không kẹt control.

Cutscene step types:

```lua
Fade
Letterbox
CameraFocus
CameraLookAt
Dialogue
Wait
SetObjective
RestoreCamera
UnlockPlayer
```

Acceptance:

- CS0 after teleport plays once.
- CS1 at Nhà văn hóa plays once.
- Text/camera always restores when cutscene ends.
- Player input returns after cutscene.

## 6. Milestone M5 - Chapter 1 Vertical Slice

Goal: chứng minh story-first loop chạy từ teleport tới tutorial phân loại.

Quest chain:

```text
Q1_01_ArriveVenSong
-> Q1_02_MeetBacXanh
-> Q1_03_CleanEntrance
-> Q1_04_SortFirstTrash
-> Q2_01_ToGrocery
```

Build tasks:

- [ ] CS0: teleport intro.
- [ ] Marker to Nhà văn hóa.
- [ ] Bác Xanh intro dialogue from dialogue doc.
- [ ] Cleanup cluster near Nhà văn hóa/đường vào.
- [ ] Chị Lan sorting dialogue.
- [ ] Simple sorting interaction at Điểm tập kết rác.
- [ ] Notebook entry Ch1.
- [ ] Transition line to Cô Tư.

Acceptance:

- Player understands Ven Sông từng xanh.
- Player learns rác cần đi đúng chỗ.
- Player knows next target is Tạp hóa Cô Tư.

## 7. Milestone M6 - Chapter 2 Tạp Hóa / Làng

Quest chain:

```text
Q2_01_ToGrocery
-> Q2_02_ObserveVillageTrash
-> Q2_03_CleanGrocery
-> Q2_04_SortGroceryTrash
-> Q2_05_GroceryCommitment
-> Q2_06_TalkToBacXanh
-> Q3_01_ToFootballField
```

Build tasks:

- [ ] Marker from Nhà văn hóa/điểm tập kết to Tạp hóa.
- [ ] Cô Tư intro conversation.
- [ ] Trash cluster: túi nilon, vỏ bánh, chai nước near tạp hóa.
- [ ] Optional inspect points around đường làng.
- [ ] Sorting minigame for grocery trash at `TrashSite`.
- [ ] AfterQuest Cô Tư commitment.
- [ ] Bác Xanh transition dialogue outside grocery.
- [ ] Add thùng rác visual/commitment near tạp hóa.
- [ ] Notebook Ch2.
- [ ] Transition to sân bóng.

Acceptance:

- Player understands rác sinh hoạt đến từ nhu cầu và thói quen.
- Cô Tư changes from "lát dọn" to "cô nhắc khách".

## 8. Milestone M7 - Chapter 3 Sân Bóng

Quest chain:

```text
Q3_01_ToFootballField
-> Q3_02_TalkAnhTung
-> Q3_03_CleanField
-> Q3_04_SortFieldTrash
-> Q3_05_BeNaMoment
-> Q3_06_FieldReminder
-> Q4_01_ToRiver
```

Build tasks:

- [ ] Display name `Sân bóng thôn Ven Sông` for hotspot.
- [ ] Add field trash: chai nước, túi snack, ly nhựa.
- [ ] Anh Tùng intro dialogue with Bé Na interruption.
- [ ] Cleanup around ghế/khung thành/edge sân.
- [ ] Sorting minigame for field trash at `TrashSite`.
- [ ] Bé Na after dialogue.
- [ ] Add field reminder: biển/thùng/commitment.
- [ ] Notebook Ch3.
- [ ] Transition to Ông Sáu/bờ sông.

Acceptance:

- Player sees sân bóng as communal space, not random cleanup area.
- Anh Tùng changes from "lát dọn" to "sân của tụi anh".

## 9. Milestone M8 - Chapter 4 Bờ Sông / Ông Sáu

Quest chain:

```text
Q4_01_ToRiver
-> Q4_02_FollowRiverTrash
-> Q4_03_SortRiverTrash
-> Q4_04_RiverRealization
-> Q5_01_FindDrain
```

Build tasks:

- [ ] Marker from sân bóng to Ông Sáu.
- [ ] Ông Sáu intro dialogue.
- [ ] River trail markers from bờ sông to khúc sông.
- [ ] River trash cluster/visual: bags caught on grass/edge.
- [ ] Sorting minigame for river trash at `TrashSite`.
- [ ] AfterQuest realization dialogue.
- [ ] Notebook Ch4.
- [ ] Transition to cống.

Acceptance:

- Player understands rác không đứng yên.
- Ông Sáu changes from "tui đâu vứt xuống sông" to "không làm ngơ nữa".

## 10. Milestone M9 - Chapter 5 Cống / Community / Ending

Quest chain:

```text
Q5_01_FindDrain
-> Q5_02_ClearDrain
-> Q5_03_SortDrainTrash
-> Q5_04_GatherCommunity
-> Q5_05_PreventReturn
-> Q5_06_ReturnToCommunityHouse
-> EndingSequence
```

Build tasks:

- [ ] Display name `Cống thoát nước cuối xóm`.
- [ ] Add cống visual if missing.
- [ ] Add cống blockage trash cluster.
- [ ] CS5A Cống Nghẹt.
- [ ] Clear drain interaction and visual change.
- [ ] CS5B Dọn Cống Không Đủ.
- [ ] Gather community conversations:
  - Cô Tư
  - Anh Tùng
  - Ông Sáu
  - Chị Lan
  - optional Anh Hòa
- [ ] Prevention actions:
  - thùng gần tạp hóa
  - biển/thùng gần sân bóng
  - biển bờ sông or cây xanh
- [ ] Return to Nhà văn hóa.
- [ ] Ending gathering and final dialogue.
- [ ] Post-ending state/free roam.

Acceptance:

- Chapter 5 không cảm giác là một checklist dài.
- Player sees cause -> consequence -> prevention -> community promise.
- Ending fires once and does not branch.

## 11. Milestone M10 - NPC Phụ And Ambient Life

Goal: làm làng có nhiều tiếng nói hơn.

Priority NPCs:

1. Bác Bảy near Nhà văn hóa.
2. Chú Minh near Điểm tập kết rác.
3. Cô Hạnh/Em Phúc near làng/tạp hóa.
4. Dì Năm/Nam thủ môn/Cô Mai near sân bóng.
5. Chú Lộc/Bà Tám near bờ sông.
6. Anh Hòa near cống.

Tasks:

- [ ] Spawn NPC models or reuse simple villagers.
- [ ] Add Before/After lines from dialogue doc.
- [ ] Add optional ending attendance for NPCs interacted with.
- [ ] Ensure NPC phụ do not show main objective marker.

Acceptance:

- Player can talk to extra NPCs without breaking route.
- Story feels populated, not just 5 quest givers.

## 12. Milestone M11 - Polish And QA

QA checklist:

- [ ] No old UI text says `PicnicArea`, `Dam`, `Dùng Scanner`.
- [ ] No chapter text gets stuck.
- [ ] Player input returns after every dialogue/cutscene.
- [ ] Quest marker always points somewhere valid.
- [ ] Every chapter can be completed from fresh player state.
- [ ] Ending only plays once.
- [ ] Rejoining or respawning does not reset story incorrectly.
- [ ] Trash collected/hidden state is consistent.
- [ ] NPC dialogue state changes after quest completion.

Playtest questions:

- Did player know why they were cleaning?
- Did player know where to go next?
- Did each NPC feel like a person, not a menu?
- Did Chapter 5 feel like a climax, not cleanup grind?
- Did ending feel earned?

## 13. Suggested Build Order For The Next Work Session

Do this next:

1. Inspect current Roblox scripts and GreenAgain folders.
2. Freeze current v4 systems that still work: teleport, interaction, trash pickup.
3. Add `QuestData` and `DialogueData` for Chapter 1 only.
4. Add objective marker controller.
5. Add dialogue UI/controller.
6. Wire `Q1_01` to `Q1_04`.
7. Playtest Chapter 1 end-to-end.
8. Only then continue Chapter 2.

Reason:

Chapter 1 is the vertical slice. If Chapter 1 proves dialogue -> marker -> cleanup -> sorting -> notebook works, every later chapter becomes content/data plus a few special interactions.
