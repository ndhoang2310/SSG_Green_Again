# Green Again v5 - Quest Flow

> Quest v5 là nhịp kể chuyện. Mỗi quest phải có story beat, marker, dialogue, hành động minh họa và kết quả cảm xúc.

## 1. Quest State Model

Mỗi quest nên có:

```text
QuestId
Title
Chapter
ObjectiveText
TargetType: NPC | Location | Item | Cleanup | Placement | Cutscene
TargetId
StartTrigger
CompleteTrigger
OnStartDialogue
OnCompleteDialogue
NotebookEntry
NextQuestId
```

## 2. Global Rules

- Chỉ hiện 1 objective chính.
- NPC phụ không chen marker chính.
- Không dùng "Dùng Scanner" làm objective.
- Objective phải là hành động tự nhiên: `Gặp Cô Tư`, `Theo dấu rác ra bờ sông`, `Quay về Nhà văn hóa`.
- Mỗi chapter có ít nhất 1 notebook entry.

## 3. Chapter 1 Flow

| QuestId | Title | Objective | Trigger complete | Next |
|---|---|---|---|---|
| Q1_01_ArriveVenSong | Đến Ven Sông | Đi tới Nhà văn hóa | Enter Nhà văn hóa zone | Q1_02_MeetBacXanh |
| Q1_02_MeetBacXanh | Gặp Bác Xanh | Nói chuyện với Bác Xanh | Dialogue complete | Q1_03_CleanEntrance |
| Q1_03_CleanEntrance | Lối Vào Bị Bỏ Quên | Nhặt rác quanh lối vào | Trash count reached | Q1_04_SortFirstTrash |
| Q1_04_SortFirstTrash | Rác Đi Đâu? | Phân loại rác vừa nhặt tại điểm tập kết | Sorting minigame complete | Q1_05_MeetChiLan |
| Q1_05_MeetChiLan | Chị Lan Và Các Thùng Rác | Nói chuyện với Chị Lan | Dialogue complete | Q2_01_ToGrocery |

Notebook:

```text
Ven Sông từng xanh hơn. Rác không chỉ cần được nhặt, nó cần đi đúng chỗ.
```

## 4. Chapter 2 Flow

| QuestId | Title | Objective | Trigger complete | Next |
|---|---|---|---|---|
| Q2_01_ToGrocery | Cái Túi Nhỏ | Gặp Cô Tư ở tạp hóa | Talk Cô Tư | Q2_02_ObserveVillageTrash |
| Q2_02_ObserveVillageTrash | Chuyện Nhỏ Mỗi Ngày | Quan sát rác quanh tạp hóa | Inspect/cleanup spots | Q2_03_CleanGrocery |
| Q2_03_CleanGrocery | Trước Cửa Tiệm | Dọn rác quanh tạp hóa | Trash count reached | Q2_04_SortGroceryTrash |
| Q2_04_SortGroceryTrash | Đem Rác Về Đúng Chỗ | Phân loại rác tạp hóa ở điểm tập kết | Sorting minigame complete | Q2_05_GroceryCommitment |
| Q2_05_GroceryCommitment | Một Chỗ Để Bỏ Rác | Nói lại với Cô Tư | Dialogue complete | Q2_06_TalkToBacXanh |
| Q2_06_TalkToBacXanh | Người Cùng Làm | Gặp Bác Xanh ngoài tiệm tạp hóa | Dialogue complete | Q3_01_ToFootballField |

Notebook:

```text
Một cái túi nhỏ không nhỏ nữa nếu cả làng đều nghĩ vậy.
```

## 5. Chapter 3 Flow

| QuestId | Title | Objective | Trigger complete | Next |
|---|---|---|---|---|
| Q3_01_ToFootballField | Sau Trận Bóng | Đi tới sân bóng | Enter sân bóng zone | Q3_02_TalkAnhTung |
| Q3_02_TalkAnhTung | Có Người Dọn Mà | Nói chuyện với Anh Tùng | Dialogue complete | Q3_03_CleanField |
| Q3_03_CleanField | Sân Của Tụi Mình | Dọn rác quanh sân bóng | Trash count reached | Q3_04_SortFieldTrash |
| Q3_04_SortFieldTrash | Chai Sau Trận | Phân loại rác sân bóng ở điểm tập kết | Sorting minigame complete | Q3_05_BeNaMoment |
| Q3_05_BeNaMoment | Chỗ Chơi Của Bé Na | Nói chuyện với Bé Na | Dialogue complete | Q3_06_FieldReminder |
| Q3_06_FieldReminder | Nhắc Nhau Sau Trận | Đặt nhắc nhở ở trung tâm sân bóng | Placement/interact complete | Q4_01_ToRiver |

Notebook:

```text
Không gian chung chỉ sạch nếu người dùng nó cũng xem đó là trách nhiệm của mình.
```

## 6. Chapter 4 Flow

| QuestId | Title | Objective | Trigger complete | Next |
|---|---|---|---|---|
| Q4_01_ToRiver | Xuống Bờ Sông | Gặp Ông Sáu | Talk Ông Sáu | Q4_02_FollowRiverTrash |
| Q4_02_FollowRiverTrash | Rác Không Đứng Yên | Theo dấu rác dọc bờ sông | Visit markers/collect trash | Q4_03_SortRiverTrash |
| Q4_03_SortRiverTrash | Rác Từ Bờ Sông | Đem rác bờ sông về điểm tập kết để phân loại | Sorting minigame complete | Q4_04_RiverRealization |
| Q4_04_RiverRealization | Gió Và Mưa Không Hỏi | Nói lại với Ông Sáu | Dialogue complete | Q5_01_FindDrain |

Notebook:

```text
Rác không biến mất. Nó chỉ chuyển chỗ, và nơi nhận hậu quả có thể là sông.
```

## 7. Chapter 5 Flow

| QuestId | Title | Objective | Trigger complete | Next |
|---|---|---|---|---|
| Q5_01_FindDrain | Cuối Dòng Nước | Đi tới cống thoát nước cuối xóm | Enter drain zone | Q5_02_ClearDrain |
| Q5_02_ClearDrain | Cống Nghẹt | Dọn rác mắc ở cống | Clear drain trash | Q5_03_SortDrainTrash |
| Q5_03_SortDrainTrash | Rác Cuối Dòng | Phân loại rác lấy ra từ cống | Sorting minigame complete | Q5_04_GatherCommunity |
| Q5_04_GatherCommunity | Không Thể Dọn Một Mình | Rủ mọi người cùng thay đổi | 3+ NPC reactions | Q5_05_PreventReturn |
| Q5_05_PreventReturn | Để Rác Không Quay Lại | Đặt thùng, biển nhắc và trồng cây ở khu làng | placement count reached | Q5_06_ReturnToCommunityHouse |
| Q5_06_ReturnToCommunityHouse | Lời Hứa Ven Sông | Quay về Nhà văn hóa gặp Bác Xanh | Talk Bác Xanh | EndingSequence |
| EndingSequence | Ven Sông Bắt Đầu Xanh Lại | Lắng nghe lời hứa Ven Sông | Auto | PostEnding_FreeRoam |

Notebook:

```text
Dọn cống là xử lý hậu quả. Để rác không quay lại, cả làng phải đổi thói quen nhỏ của mình.
```

## 8. Ending Sequence State

```text
EndingSequence_Start
-> Fade/camera Nhà văn hóa
-> NPC commitments
-> Bác Xanh final line
-> End text
-> PostEnding_FreeRoam
```

Post-ending quest:

```text
Giữ Ven Sông xanh
```

## 9. Marker Strategy

| Quest type | Marker |
|---|---|
| Talk NPC | icon/person marker over NPC |
| Go location | soft ring + label at zone |
| Cleanup | marker on area, not every trash unless player is close |
| Placement | marker on one chosen placement spot |
| Ending return | marker at Bác Xanh/Nhà văn hóa |

## 10. Implementation Notes

- Old scanner markers can be repurposed into story objective markers.
- QuestManager should store `currentQuestId`, `chapter`, `completedStoryFlags`.
- Dialogue should be data-driven by `NpcId` + quest state.
- Notebook entry fires on quest completion, not on every trash pickup.
