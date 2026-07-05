# GREEN AGAIN V5 — DOCUMENT TỔNG HỢP VÀ HƯỚNG DẪN BUILD

> **Phiên bản:** 1.0 — 2026-07-02
> **Mục đích:** Một document duy nhất đóng vai trò Game Design Document, Build Guide, Implementation Reference, UI/UX Spec và NPC/Dialogue/Cutscene/Movement Spec cho Green Again V5.
> **Ngôn ngữ:** Tiếng Việt. Tên kỹ thuật, path Roblox, quest ID, script name giữ nguyên tiếng Anh.

---

## MỤC LỤC

1. [Tổng Quan Game](#1-tổng-quan-game)
2. [Pillars Thiết Kế](#2-pillars-thiết-kế)
3. [Trạng Thái Build Hiện Tại](#3-trạng-thái-build-hiện-tại)
4. [Roblox Workspace Mapping](#4-roblox-workspace-mapping)
5. [Quest Flow Đầy Đủ](#5-quest-flow-đầy-đủ)
6. [Dialogue Bible](#6-dialogue-bible)
7. [NPC Role Và Movement Spec](#7-npc-role-và-movement-spec)
8. [Cutscene Và Staging](#8-cutscene-và-staging)
9. [Gameplay Systems](#9-gameplay-systems)
10. [UI/UX Spec Đầy Đủ](#10-uiux-spec-đầy-đủ)
11. [Build Guide Dành Cho Codex](#11-build-guide-dành-cho-codex)
12. [Current Technical Details](#12-current-technical-details)
13. [Test Plan](#13-test-plan)
14. [Gaps / Chưa Rõ / Đề Xuất Bổ Sung](#14-gaps--chưa-rõ--đề-xuất-bổ-sung)

---

## 1. TỔNG QUAN GAME

**Nguồn chính:** `GDD_GreenAgain_v5.md`, `GDD_GreenAgain_v5_STORY_BIBLE.md`

### 1.1 Thông tin cơ bản

| Mục | Nội dung |
|---|---|
| **Tên game** | Green Again |
| **Phiên bản thiết kế** | V5 |
| **Platform** | Roblox |
| **Thể loại** | Story-driven educational game |
| **Chủ đề** | Giáo dục môi trường tại thôn Ven Sông |
| **Đối tượng** | Trẻ em và thanh thiếu niên Việt Nam, phù hợp mọi lứa tuổi |
| **Tone cảm xúc** | Ấm, đời thường, hơi buồn nhưng không bi quan. Không lên lớp, không đổ lỗi, không hù dọa |

### 1.2 Core Fantasy

> Mình bước vào một ngôi làng từng xanh, lắng nghe từng người, nhìn thấy đường đi của rác, và giúp cộng đồng bắt đầu thay đổi.

### 1.3 Mục tiêu MVP

MVP là một **story-first vertical slice** — một lượt chơi liền mạch từ khi player đến Ven Sông cho tới ending tại Nhà văn hóa, chứng minh:

- Dialogue là gameplay chính.
- Nhặt rác, phân loại, đặt thùng, dựng biển là hành động minh họa cho câu chuyện.
- Mỗi chương mở ra một mảnh sự thật về Ven Sông.
- Kết thúc bằng cộng đồng cùng nhận phần việc nhỏ.

### 1.4 Player Experience — 5 cảm giác

1. **Lạ lẫm:** Ven Sông có gì đó đẹp nhưng đang bị bỏ quên.
2. **Hiểu nguyên nhân:** Rác không đến từ một người xấu.
3. **Nhìn thấy thói quen:** "Chỉ một chút thôi" tạo thành nhiều.
4. **Nhìn thấy hệ quả:** Rác không đứng yên, nó đi theo dòng nước.
5. **Hy vọng:** Cộng đồng bắt đầu cùng thay đổi.

---

## 2. PILLARS THIẾT KẾ

**Nguồn chính:** `GDD_GreenAgain_v5.md` (Section 2), `GDD_GreenAgain_v5_STORY_BIBLE.md` (Section 3)

| Pillar | Nghĩa là gì | Không làm |
|---|---|---|
| **Story first** | Mỗi chương mở ra một mảnh sự thật về Ven Sông | Không giao nhiệm vụ kiểu "nhặt 10 rác" nếu không có câu chuyện |
| **NPC-driven** | Người dân là nguồn cảm xúc và thông tin | Không để NPC chỉ làm máy giao quest |
| **Small actions, visible consequences** | Hành động nhỏ tạo thay đổi nhìn thấy được | Không biến gameplay thành score grind |
| **Vietnamese village texture** | Địa điểm, lời thoại, thói quen gần Việt Nam | Không dùng tên/địa điểm generic như "Picnic Area" trong story |
| **One hopeful ending** | Một ending truyền cảm hứng tại Nhà văn hóa | Không chia ending A/B/C bằng điểm số |

### Theme chính

> Từng hành động nhỏ đều để lại dấu vết.

### Theme phụ

- Môi trường là ký ức chung của cộng đồng.
- Rác không biến mất; nó chỉ chuyển chỗ.
- Người lớn thay đổi để trẻ con có chỗ sống và chơi tốt hơn.
- Cộng đồng không cần hoàn hảo để bắt đầu.

### Quy tắc Story-Gameplay

- Không bắt đầu bằng "nhặt rác ngay" nếu chưa có cảm xúc hoặc bối cảnh.
- Mỗi hành động cleanup phải trả lời: player vừa hiểu điều gì?
- Mỗi NPC chính phải có thay đổi nhỏ trước và sau chương.
- Marker chỉ dẫn rõ, nhưng không thay thế lời dẫn của Bác Xanh/NPC.
- Sổ tay là nơi chốt bài học bằng ngôn ngữ mềm, không giảng đạo đức.

---

## 3. TRẠNG THÁI BUILD HIỆN TẠI

**Nguồn chính:** `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`

### 3.1 Script hiện dùng

| Loại | Path | Ghi chú |
|---|---|---|
| **Startup loader** | `ReplicatedFirst.GreenAgainStartupLoader` | Màn loading đầu game có logo Green Again, đợi waiting screen render xong rồi fade |
| **Server runtime** | `ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP` | Script server chính điều khiển story, quest, dialogue, interaction routing, cleanup spawning, placement, drain, community gather, notebook, ending |
| **Client script** | `StarterPlayer.StarterPlayerScripts.StoryClientMVP` | Script client chính xử lý HUD, marker, dialogue UI, sorting minigame, interaction prompt, feedback toast, notebook book/panel, ending overlay |
| **Sprint script** | `StarterPlayer.StarterCharacterScripts.SprintStaminaScript` | Giữ logic sprint (Shift chạy nhanh), đã xóa stamina bar UI |

### 3.2 Script/UI đã xóa

| Đã xóa | Lý do |
|---|---|
| `StarterGui.GreenAgainHUD_V5` | HUD cũ gây duplicate UI |
| `StarterPlayer.StarterPlayerScripts.GreenAgainObjectiveClient` | Client objective cũ gây duplicate behavior |
| `ServerScriptService.GreenAgainProject.Runtime_To_Add.MapWiringBootstrap` | Server bootstrap cũ gây duplicate wiring |

### 3.3 HUD hiện tại

Startup loader:
- `ReplicatedFirst.GreenAgainStartupLoader` thay default Roblox loading screen.
- Hiện logo Green Again bằng asset `rbxassetid://112991523200169`.
- Đợi `MainMenuGui.LogoImage`, `Workspace.MainMenuAssets.PlayBtn`, và `Workspace.MainMenuAssets.SetBtn` sẵn sàng rồi fade ra.

MVP HUD được tạo bởi `StoryClientMVP`, bao gồm:
- Quest tracker (chapter, quest title, objective text).
- Interaction prompt (`[E] Action - Object`).
- Dialogue panel (speaker, line progress `1 / 4`, continue/choice buttons).
- Feedback toast.
- Notebook book/panel: mỗi chapter unlock một trang, có thể mở lại bằng nút `Nhật ký` hoặc phím `N`.
- Sorting minigame: kéo từng món rác trong túi vào thùng `Nguy hiểm`, `Tái chế`, `Hữu cơ`, hoặc `Còn lại`; mỗi món là card visual render model rác 3D từ `Workspace.Trash` bằng `ViewportFrame`.
- Ending overlay.

**Không còn:** Old top-left text `Đang nối map Green Again V5...`, old stamina bar.

### 3.4 Marker behavior (Đã build)

- Chỉ **một marker** active tại một thời điểm.
- Hình thoi xanh nhỏ (green diamond).
- Có tên target, **không có distance text**.
- Marker chỉ hiện khi player đã vào map chính (sau teleport).
- Marker/tracker ẩn khi player ở lobby/khu nối.

### 3.5 Quest system (Đã build)

Đã implement route đầy đủ từ `Q1_01_ArriveVenSong` đến `PostEnding_FreeRoam` (22 quest).

Hệ thống bao gồm:
- Per-player story state: current quest, chapter, cleanup counts, placement counts, community progress, notebook flags, ending flag.
- Quest start/completion.
- Dialogue-driven quest completion.
- Interaction routing cho NPCs, locations, trash, placement, drain.
- Runtime trash spawning.
- Sorting quests mở mini game kéo-thả; server validate từng item trước khi complete quest.
- Runtime placement markers.
- Notebook book page unlock (1 lần/chapter).
- Ending text.

### 3.6 Dialogue system (Đã build)

Data-driven dialogue cho toàn bộ main route:
- Multiple lines, speaker names, simple choices.
- Continue bằng `E` hoặc nút continue.
- Debounce để dialogue đã complete không mở lại ngay.

### 3.7 Sprint/Stamina (Đã build)

- Sprint logic giữ nguyên: giữ Shift để chạy nhanh.
- Stamina bar UI đã bị xóa.
- Walk speed thay đổi từ default → sprint speed.

### 3.8 Cống thật đang dùng

- Object: `Workspace["=== GREEN AGAIN V5 ==="].SYSTEMS_REVIEW.Doors_Vehicles_And_AssetScripts.OngThoatNuoc`
- Kept anchored.
- Chỉ trở nên interactable ở Chapter 5.

### 3.9 Height/Position fixes (Đã build)

- Marker đầu game không dùng pivot cao của `NhaVanHoa_ThonNoiChuan`.
- Hub gameplay position dùng grounded override gần mặt đất.
- Q1 cleanup trash spawn gần ground height thay vì floating.
- Validated: Hub marker ~`284.24, 51.85, -3570`, Q1 trash ~`Y = 52.2`.

### 3.10 Test đã chạy

- ✅ Fresh MVP flow advance tới `PostEnding_FreeRoam`.
- ✅ Chỉ một objective marker.
- ✅ Marker có tên, không có distance.
- ✅ Marker/tracker ẩn trước khi vào main map.
- ✅ Marker/tracker hiện sau teleport.
- ✅ Old connection text không còn.
- ✅ Old HUD không còn.
- ✅ Stamina UI không còn.
- ✅ Sprint script giữ Shift sprint.
- ✅ Q1 marker và trash dùng ground-level positions.

---

## 4. ROBLOX WORKSPACE MAPPING

**Nguồn chính:** `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`, `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`

### 4.1 Root

| Path | Mô tả |
|---|---|
| `Workspace["=== GREEN AGAIN V5 ==="]` | Root folder chứa toàn bộ map V5 |
| `Workspace.Trash` | Thư viện source asset cho model rác/thùng rác/scene dressing; không phải runtime quest folder |
| `MAP_ROUTE` | Sub-folder chính chứa route story |
| `MAP_ROUTE.06_NPCs` | Folder chứa toàn bộ NPC chính |

Trash asset library details live in:

```text
docs/GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md
```

Rule: template trong `Workspace.Trash` phải giữ `Interactable=false`. Runtime quest props vẫn spawn/clone vào `Workspace.GreenAgainV5_StoryRuntime`.

Runtime status:

- Cleanup trash visuals now clone from `Workspace.Trash.Collectibles`.
- Sorting bin visuals now clone from `Workspace.Trash.Props.Bins.TrashCan_P7`.
- Runtime clones are grounded by bounding box so their bottom sits on the configured spawn Y.

### 4.2 NPC Objects

| Object | Path | Tên hiển thị | Vai trò story | Quest liên quan | Ghi chú implementation |
|---|---|---|---|---|---|
| `BacXanh` | `MAP_ROUTE.06_NPCs.BacXanh` | Bác Xanh | Mentor, người giữ ký ức Ven Sông, dẫn player qua story | Q1_02, transitions, Q5_05, ending | NPC chính, interactable nhiều nhất |
| `ChiLan` | `MAP_ROUTE.06_NPCs.ChiLan` | Chị Lan | Phụ trách phân loại rác, tổ môi trường | Q1_04, Q5_02-03, ending | Đứng gần Điểm tập kết rác |
| `CoTu` | `MAP_ROUTE.06_NPCs.CoTu` | Cô Tư | Chủ tạp hóa, nguồn rác sinh hoạt | Q2_01, Q2_05, Q5_04, ending | Đứng gần tạp hóa |
| `AnhTung` | `MAP_ROUTE.06_NPCs.AnhTung` | Anh Tùng | Thanh niên chơi bóng, thói quen "lát dọn" | Q3_01-05, Q5_03, ending | Đứng ở sân bóng |
| `BeNa` | `MAP_ROUTE.06_NPCs.BeNa` | Bé Na | Em nhỏ, đại diện thế hệ sau | Q3_02-04, ending | Gần sân bóng |
| `OngSau` | `MAP_ROUTE.06_NPCs.OngSau` | Ông Sáu | Người sống lâu bờ sông, hoài niệm | Q4_01-03, Q5_03, ending | Gần bờ sông |

### 4.3 Location Objects

| Object | Path gần đúng | Tên hiển thị | Vai trò story | Quest liên quan | Ghi chú |
|---|---|---|---|---|---|
| `NhaVanHoa_ThonNoiChuan` | Trong `MAP_ROUTE` hoặc root V5 | Nhà văn hóa thôn Ven Sông | Hub khởi đầu, nơi gặp Bác Xanh, ending | Q1_01, Q1_02, Q5_05, ending | Hub trung tâm |
| `DiemTapKetRacThai_ThonVenSong` | Trong `MAP_ROUTE` | Điểm tập kết rác thôn | Tutorial phân loại, nơi Chị Lan giải thích | Q1_04 | Bên phải/hơi trên Nhà văn hóa |
| `TapHoaCoTu_HouseOnly_Rural` | Trong `MAP_ROUTE` | Tạp hóa Cô Tư | Nơi kể chuyện nhu cầu tăng, bao bì tăng | Q2_01-06 | Nối làng với sân bóng |
| `KhungThanh_01_Marker` | Trong `MAP_ROUTE` | Khung thành sân bóng (1) | Đánh dấu khu vực sân bóng | Q3_01-05 | Dùng cho sân bóng thôn Ven Sông |
| `KhungThanh_02_Marker` | Trong `MAP_ROUTE` | Khung thành sân bóng (2) | Đánh dấu khu vực sân bóng | Q3_01-05 | Cặp với marker 01 |
| `NPC_OngSau_Marker` | Trong `MAP_ROUTE` | Vị trí Ông Sáu | Đánh dấu khu bờ sông Ông Sáu | Q4_01-03 | Gần sông |
| `OngThoatNuoc` | `SYSTEMS_REVIEW.Doors_Vehicles_And_AssetScripts.OngThoatNuoc` | Cống thoát nước cuối xóm | Cao trào Ch5: rác tụ, nghẹt, hậu quả | Q5_01-02 | Anchored, chỉ interactable Ch5 |

### 4.4 Sơ đồ không gian

```text
                         THỊ TRẤN / LÀNG VEN SÔNG
                  nhà dân, đường làng, khu sinh hoạt
                                      |
                                TẠP HÓA CÔ TƯ
                         điểm chuyển từ làng sang sân bóng
                                      |
  SPAWNER ---- NHÀ VĂN HÓA ---- ĐIỂM TẬP KẾT RÁC -------- SÂN BÓNG
  bắt đầu      hub kể chuyện     tutorial phân loại        Anh Tùng, Bé Na
               Bác Xanh          / rác cộng đồng           rác sau vui chơi
                                                                  |
                                                              ÔNG SÁU
                                                        bờ sông / ký ức cũ
                                                                  |
                                                          DÒNG SÔNG LIÊN TỤC
                                                        rác trôi theo dòng
                                                                  |
                                                       CỐNG THOÁT NƯỚC CUỐI XÓM
                                                       rác tụ, nghẹt, hậu quả
```

### 4.5 Quy ước tên hiển thị

| Tên kỹ thuật cũ | Tên hiển thị V5 | Lưu ý |
|---|---|---|
| `PicnicArea` | Sân bóng thôn Ven Sông | KHÔNG gọi là "Công viên", "Bãi picnic" |
| `ResidentialSt` | Thị trấn / làng Ven Sông | KHÔNG gọi là "Xóm ven đường" cho cụm lớn |
| `RiverNE` | Bờ sông chỗ Ông Sáu | — |
| `RiverBend` | Khúc sông sau làng | — |
| `Dam_C1/C2/C3` | Cống thoát nước cuối xóm | KHÔNG gọi là "Đập" |
| `Portal1Destination` | Spawner / Lối vào Nhà văn hóa | — |

---

## 5. QUEST FLOW ĐẦY ĐỦ

**Nguồn chính:** `GDD_GreenAgain_v5_QUEST_FLOW.md`, `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`

### 5.1 Chapter 1 — Người Lạ Đến Ven Sông

**Story question:** Ven Sông từng xanh như thế nào?
**Main NPC:** Bác Xanh, Chị Lan
**Notebook:** "Ven Sông từng xanh hơn. Rác không chỉ cần được nhặt, nó cần đi đúng chỗ."

#### Q1_01_ArriveVenSong

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q1_01_ArriveVenSong` |
| **Chapter** | 1 |
| **Title** | Đến Ven Sông |
| **Objective** | Đi tới Nhà văn hóa |
| **Target** | `NhaVanHoa_ThonNoiChuan` (location) |
| **Interaction type** | Enter zone |
| **Completion condition** | Player enter Nhà văn hóa zone |
| **Dialogue** | Không (CS0 text on screen: "Thôn Ven Sông — Một nơi từng xanh hơn những gì bạn đang thấy.") |
| **Marker** | Marker tại Nhà văn hóa |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q1_02_MeetBacXanh` |
| **Notes** | Marker chỉ hiện sau khi player đã vào main map. CS0 fade in từ đen |

#### Q1_02_MeetBacXanh

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q1_02_MeetBacXanh` |
| **Chapter** | 1 |
| **Title** | Gặp Bác Xanh |
| **Objective** | Nói chuyện với Bác Xanh |
| **Target** | `BacXanh` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Dialogue complete (Bác Xanh intro conversation) |
| **Dialogue** | `BacXanh_Ch1_Intro` — Bác Xanh Và Ảnh Cũ (xem Section 6) |
| **Marker** | Marker trên Bác Xanh |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q1_03_CleanEntrance` |
| **Notes** | CS1 trigger khi player tới Nhà văn hóa. Dialogue complete → objective đổi |

#### Q1_03_CleanEntrance

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q1_03_CleanEntrance` |
| **Chapter** | 1 |
| **Title** | Lối Vào Bị Bỏ Quên |
| **Objective** | Nhặt rác quanh lối vào Nhà văn hóa |
| **Target** | Khu vực quanh Nhà văn hóa (area cleanup) |
| **Interaction type** | Cleanup |
| **Completion condition** | Trash count reached (số lượng cần nhặt) |
| **Dialogue** | Bác Xanh after first cleanup (xem Section 6) |
| **Marker** | Marker trên area/trash gần Nhà văn hóa |
| **Runtime object** | Runtime trash spawned gần ground height (~Y = 52.2) |
| **Quest tiếp theo** | `Q1_04_SortFirstTrash` |
| **Notes** | Trash spawn gần mặt đất, không floating |

#### Q1_04_SortFirstTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q1_04_SortFirstTrash` |
| **Chapter** | 1 |
| **Title** | Rác Đi Đâu? |
| **Objective** | Mang rác tới điểm tập kết |
| **Target** | `DiemTapKetRacThai_ThonVenSong` + `ChiLan` |
| **Interaction type** | Interact Chị Lan/bin |
| **Completion condition** | Interact với Chị Lan → dialogue complete (sorting explanation) |
| **Dialogue** | `ChiLan_Ch1_Intro` — Rác Đi Đâu? (xem Section 6) |
| **Marker** | Marker tại Điểm tập kết rác |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q2_01_ToGrocery` |
| **Notes** | CS1B trigger. Notebook entry Ch1 fires |

### 5.2 Chapter 2 — Chỉ Một Chút Thôi Mà

**Story question:** Rác sinh hoạt bắt đầu từ đâu?
**Main NPC:** Cô Tư
**Notebook:** "Một cái túi nhỏ không nhỏ nữa nếu cả làng đều nghĩ vậy."

#### Q2_01_ToGrocery

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q2_01_ToGrocery` |
| **Chapter** | 2 |
| **Title** | Cái Túi Nhỏ |
| **Objective** | Gặp Cô Tư ở tạp hóa |
| **Target** | `CoTu` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Talk Cô Tư (dialogue complete) |
| **Dialogue** | `CoTu_Ch2_Intro` — Cái Túi Nhỏ (xem Section 6) |
| **Marker** | Marker trên Cô Tư |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q2_02_ObserveVillageTrash` |
| **Notes** | Bác Xanh transition line dẫn player tới tạp hóa trước khi quest bắt đầu |

#### Q2_02_ObserveVillageTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q2_02_ObserveVillageTrash` |
| **Chapter** | 2 |
| **Title** | Chuyện Nhỏ Mỗi Ngày |
| **Objective** | Quan sát rác quanh tạp hóa |
| **Target** | Khu vực quanh tạp hóa (inspect/cleanup spots) |
| **Interaction type** | Inspect + Cleanup |
| **Completion condition** | Inspect/cleanup spots đủ |
| **Dialogue** | Cô Tư during quest lines |
| **Marker** | Marker trên area gần tạp hóa |
| **Runtime object** | Runtime trash: túi nilon, vỏ bánh, chai nước |
| **Quest tiếp theo** | `Q2_03_CleanGrocery` |
| **Notes** | — |

#### Q2_03_CleanGrocery

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q2_03_CleanGrocery` |
| **Chapter** | 2 |
| **Title** | Trước Cửa Tiệm |
| **Objective** | Dọn rác quanh tạp hóa |
| **Target** | Khu vực tạp hóa (area cleanup) |
| **Interaction type** | Cleanup |
| **Completion condition** | Trash count reached |
| **Dialogue** | Cô Tư during quest lines |
| **Marker** | Marker trên area |
| **Runtime object** | Runtime trash |
| **Quest tiếp theo** | `Q2_04_SortGroceryTrash` |
| **Notes** | — |

#### Q2_04_SortGroceryTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q2_04_SortGroceryTrash` |
| **Chapter** | 2 |
| **Title** | Đem Rác Về Đúng Chỗ |
| **Objective** | Phân loại rác tạp hóa ở điểm tập kết |
| **Target** | `TrashSite` |
| **Interaction type** | Sorting minigame |
| **Completion condition** | Sorting complete |
| **Dialogue** | — |
| **Marker** | Marker trên điểm tập kết / sorting hitbox |
| **Runtime object** | Invisible sorting hitboxes; static scene bins are the visible bins |
| **Quest tiếp theo** | `Q2_05_GroceryCommitment` |
| **Notes** | Uses the same drag-and-drop sorting UI as Q1 |

#### Q2_05_GroceryCommitment

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q2_05_GroceryCommitment` |
| **Chapter** | 2 |
| **Title** | Một Chỗ Để Bỏ Rác |
| **Objective** | Nói lại với Cô Tư |
| **Target** | `CoTu` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Dialogue complete |
| **Dialogue** | `CoTu_Ch2_After` — Cô Tư after cleanup + commitment (xem Section 6) |
| **Marker** | Marker trên Cô Tư |
| **Runtime object** | Có thể thêm visual thùng rác gần tạp hóa |
| **Quest tiếp theo** | `Q2_06_TalkToBacXanh` |
| **Notes** | Cô Tư commitment only; Bác Xanh transition is separated into the next quest |

#### Q2_06_TalkToBacXanh

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q2_06_TalkToBacXanh` |
| **Chapter** | 2 |
| **Title** | Người Cùng Làm |
| **Objective** | Gặp Bác Xanh ngoài tiệm tạp hóa |
| **Target** | `BacXanh` staged near grocery |
| **Interaction type** | Talk NPC |
| **Completion condition** | Dialogue complete |
| **Dialogue** | `BacXanh_Q2_After` — transition from grocery story to football field |
| **Marker** | Marker trên Bác Xanh |
| **Runtime object** | NPC stage position `Vector3.new(114.281, 67.989, -3310.235)` |
| **Quest tiếp theo** | `Q3_01_ToFootballField` |
| **Notes** | Notebook entry Ch2 fires here |

### 5.3 Chapter 3 — Sau Trận Bóng

**Story question:** Nơi vui chơi chung bị ảnh hưởng thế nào?
**Main NPC:** Anh Tùng, Bé Na
**Notebook:** "Không gian chung chỉ sạch nếu người dùng nó cũng xem đó là trách nhiệm của mình."

#### Q3_01_ToFootballField

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q3_01_ToFootballField` |
| **Chapter** | 3 |
| **Title** | Sau Trận Bóng |
| **Objective** | Đi tới sân bóng |
| **Target** | Khu vực sân bóng (`KhungThanh_01_Marker`/`KhungThanh_02_Marker`) |
| **Interaction type** | Enter zone |
| **Completion condition** | Enter sân bóng zone |
| **Dialogue** | Bác Xanh transition: "Ở tạp hóa, rác đến từ thói quen hằng ngày..." |
| **Marker** | Marker tại sân bóng |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q3_02_TalkAnhTung` |
| **Notes** | — |

#### Q3_02_TalkAnhTung

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q3_02_TalkAnhTung` |
| **Chapter** | 3 |
| **Title** | Có Người Dọn Mà |
| **Objective** | Nói chuyện với Anh Tùng |
| **Target** | `AnhTung` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Dialogue complete |
| **Dialogue** | `AnhTung_Ch3_Intro` — Sau Trận Bóng (có Bé Na chen vào, có player choice) (xem Section 6) |
| **Marker** | Marker trên Anh Tùng |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q3_03_CleanField` |
| **Notes** | CS3 trigger |

#### Q3_03_CleanField

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q3_03_CleanField` |
| **Chapter** | 3 |
| **Title** | Sân Của Tụi Mình |
| **Objective** | Dọn rác quanh sân bóng |
| **Target** | Khu vực sân bóng (area cleanup) |
| **Interaction type** | Cleanup |
| **Completion condition** | Trash count reached |
| **Dialogue** | Anh Tùng during quest: "Sau khung thành còn mấy chai đó." |
| **Marker** | Marker trên area sân bóng |
| **Runtime object** | Runtime trash: chai nước, túi snack, ly nhựa |
| **Quest tiếp theo** | `Q3_04_SortFieldTrash` |
| **Notes** | Trash gần ghế ngồi + sau khung thành |

#### Q3_04_SortFieldTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q3_04_SortFieldTrash` |
| **Chapter** | 3 |
| **Title** | Chai Sau Trận |
| **Objective** | Phân loại rác sân bóng ở điểm tập kết |
| **Target** | `TrashSite` |
| **Interaction type** | Sorting minigame |
| **Completion condition** | Sorting complete |
| **Dialogue** | — |
| **Marker** | Marker trên điểm tập kết / sorting hitbox |
| **Runtime object** | Invisible sorting hitboxes; static scene bins are the visible bins |
| **Quest tiếp theo** | `Q3_05_BeNaMoment` |
| **Notes** | Uses the picked field trash bag items |

#### Q3_05_BeNaMoment

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q3_05_BeNaMoment` |
| **Chapter** | 3 |
| **Title** | Chỗ Chơi Của Bé Na |
| **Objective** | Nói chuyện với Bé Na |
| **Target** | `BeNa` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Dialogue complete |
| **Dialogue** | `BeNa_Ch3_After` — Bé Na after sân bóng clean (xem Section 6) |
| **Marker** | Marker trên Bé Na |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q3_06_FieldReminder` |
| **Notes** | Cảm xúc beat — Bé Na tạo emotional turn |

#### Q3_06_FieldReminder

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q3_06_FieldReminder` |
| **Chapter** | 3 |
| **Title** | Nhắc Nhau Sau Trận |
| **Objective** | Đặt nhắc nhở ở trung tâm sân bóng |
| **Target** | Placement zone gần sân bóng |
| **Interaction type** | Placement/interact |
| **Completion condition** | Placement/interact complete |
| **Dialogue** | Anh Tùng after: "Lần sau đá xong anh rủ tụi nó gom chai lại." |
| **Marker** | Marker tại placement spot |
| **Runtime object** | Runtime placement marker (biển/thùng) |
| **Quest tiếp theo** | `Q4_01_ToRiver` |
| **Notes** | Notebook entry Ch3 fires |

### 5.4 Chapter 4 — Rác Không Đứng Yên

**Story question:** Rác đi đâu sau khi bị bỏ lại?
**Main NPC:** Ông Sáu
**Notebook:** "Rác không biến mất. Nó chỉ chuyển chỗ, và nơi nhận hậu quả có thể là sông."

#### Q4_01_ToRiver

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q4_01_ToRiver` |
| **Chapter** | 4 |
| **Title** | Xuống Bờ Sông |
| **Objective** | Gặp Ông Sáu |
| **Target** | `OngSau` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Talk Ông Sáu (dialogue complete) |
| **Dialogue** | `OngSau_Ch4_Intro` — Rác Trôi Theo Nước (xem Section 6) |
| **Marker** | Marker trên Ông Sáu |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q4_02_FollowRiverTrash` |
| **Notes** | CS4 trigger. Bác Xanh transition line trước đó |

#### Q4_02_FollowRiverTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q4_02_FollowRiverTrash` |
| **Chapter** | 4 |
| **Title** | Rác Không Đứng Yên |
| **Objective** | Theo dấu rác dọc bờ sông |
| **Target** | River markers / trash dọc bờ sông |
| **Interaction type** | Visit markers + collect trash |
| **Completion condition** | Visit markers / collect trash đủ |
| **Dialogue** | Ông Sáu during: "Chỗ bụi cỏ kia... nước lên là rác mắc lại đó." |
| **Marker** | Marker dọc bờ sông |
| **Runtime object** | Runtime trash dọc bờ sông: bags, túi mắc vào cỏ/bụi |
| **Quest tiếp theo** | `Q4_03_SortRiverTrash` |
| **Notes** | — |

#### Q4_03_SortRiverTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q4_03_SortRiverTrash` |
| **Chapter** | 4 |
| **Title** | Rác Từ Bờ Sông |
| **Objective** | Đem rác bờ sông về điểm tập kết để phân loại |
| **Target** | `TrashSite` |
| **Interaction type** | Sorting minigame |
| **Completion condition** | Sorting complete |
| **Dialogue** | — |
| **Marker** | Marker trên điểm tập kết / sorting hitbox |
| **Runtime object** | Invisible sorting hitboxes; static scene bins are the visible bins |
| **Quest tiếp theo** | `Q4_04_RiverRealization` |
| **Notes** | Uses the picked river trash bag items |

#### Q4_04_RiverRealization

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q4_04_RiverRealization` |
| **Chapter** | 4 |
| **Title** | Gió Và Mưa Không Hỏi |
| **Objective** | Nói lại với Ông Sáu |
| **Target** | `OngSau` (NPC) |
| **Interaction type** | Talk NPC |
| **Completion condition** | Dialogue complete |
| **Dialogue** | `OngSau_Ch4_After` — Realization + Bác Xanh insight (xem Section 6) |
| **Marker** | Marker trên Ông Sáu |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q5_01_FindDrain` |
| **Notes** | Notebook entry Ch4 fires |

### 5.5 Chapter 5 — Cống Cuối Xóm Và Lời Hứa Ven Sông

**Story question:** Làm sao để chuyện không lặp lại?
**Main NPC:** Bác Xanh, cộng đồng
**Notebook:** "Dọn cống là xử lý hậu quả. Để rác không quay lại, cả làng phải đổi thói quen nhỏ của mình."

#### Q5_01_FindDrain

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q5_01_FindDrain` |
| **Chapter** | 5 |
| **Title** | Cuối Dòng Nước |
| **Objective** | Đi tới cống thoát nước cuối xóm |
| **Target** | `OngThoatNuoc` (location) |
| **Interaction type** | Enter zone |
| **Completion condition** | Enter drain zone |
| **Dialogue** | Không trước khi tới. CS5A trigger khi player tới |
| **Marker** | Marker tại cống |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q5_02_ClearDrain` |
| **Notes** | Cống chỉ interactable từ đây |

#### Q5_02_ClearDrain

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q5_02_ClearDrain` |
| **Chapter** | 5 |
| **Title** | Cống Nghẹt |
| **Objective** | Dọn rác mắc ở cống |
| **Target** | `OngThoatNuoc` (drain interaction) |
| **Interaction type** | Clear drain trash |
| **Completion condition** | Clear drain trash (interact/cleanup) |
| **Dialogue** | Anh Hòa cống nghẹt conversation (xem Section 6). After clear: Bác Xanh + Chị Lan (xem Section 6) |
| **Marker** | Marker tại cống |
| **Runtime object** | Drain blockage trash cluster |
| **Quest tiếp theo** | `Q5_03_SortDrainTrash` |
| **Notes** | CS5A → CS5B sequence |

#### Q5_03_SortDrainTrash

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q5_03_SortDrainTrash` |
| **Chapter** | 5 |
| **Title** | Rác Cuối Dòng |
| **Objective** | Phân loại rác lấy ra từ cống |
| **Target** | `TrashSite` |
| **Interaction type** | Sorting minigame |
| **Completion condition** | Sorting complete |
| **Dialogue** | — |
| **Marker** | Marker trên điểm tập kết / sorting hitbox |
| **Runtime object** | Invisible sorting hitboxes; static scene bins are the visible bins |
| **Quest tiếp theo** | `Q5_04_GatherCommunity` |
| **Notes** | Uses drain cleanup bag items |

#### Q5_04_GatherCommunity

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q5_04_GatherCommunity` |
| **Chapter** | 5 |
| **Title** | Không Thể Dọn Một Mình |
| **Objective** | Gọi lại các NPC chính |
| **Target** | Cô Tư, Anh Tùng, Ông Sáu (multiple NPCs) |
| **Interaction type** | Talk NPCs |
| **Completion condition** | 3+ NPC reactions obtained |
| **Dialogue** | Community gather conversations: Cô Tư, Anh Tùng, Ông Sáu, Chị Lan (xem Section 6) |
| **Marker** | Marker lần lượt trên từng NPC cần gặp |
| **Runtime object** | Không |
| **Quest tiếp theo** | `Q5_05_PreventReturn` |
| **Notes** | Player quay lại gặp từng NPC ở vị trí của họ |

#### Q5_05_PreventReturn

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q5_05_PreventReturn` |
| **Chapter** | 5 |
| **Title** | Để Rác Không Quay Lại |
| **Objective** | Đặt thùng, biển nhắc và trồng cây ở khu làng |
| **Target** | Placement zones (tạp hóa, sân bóng, bờ sông) |
| **Interaction type** | Placement |
| **Completion condition** | Placement count reached (3) |
| **Dialogue** | Không — hành động trực tiếp |
| **Marker** | Marker tại placement spots |
| **Runtime object** | Runtime placement markers: thùng rác, biển nhắc, cây xanh |
| **Quest tiếp theo** | `Q5_06_ReturnToCommunityHouse` |
| **Notes** | — |

#### Q5_06_ReturnToCommunityHouse

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `Q5_06_ReturnToCommunityHouse` |
| **Chapter** | 5 |
| **Title** | Lời Hứa Ven Sông |
| **Objective** | Quay về Nhà văn hóa gặp Bác Xanh |
| **Target** | `BacXanh` (NPC) tại Nhà văn hóa |
| **Interaction type** | Talk NPC |
| **Completion condition** | Talk Bác Xanh → EndingSequence |
| **Dialogue** | Ending scene dialogue (xem Section 6) |
| **Marker** | Marker tại Bác Xanh / Nhà văn hóa |
| **Runtime object** | Không |
| **Quest tiếp theo** | `EndingSequence`, then `PostEnding_FreeRoam` |
| **Notes** | CS5C trigger. Ending fires once only |

#### PostEnding_FreeRoam

| Mục | Chi tiết |
|---|---|
| **Quest ID** | `PostEnding_FreeRoam` |
| **Chapter** | Post |
| **Title** | Giữ Ven Sông Xanh |
| **Objective** | (Tự do khám phá) |
| **Target** | Không cụ thể |
| **Interaction type** | Free roam |
| **Completion condition** | Không — trạng thái cuối |
| **Dialogue** | NPC PostEnding lines nếu có |
| **Marker** | Không marker |
| **Runtime object** | Không |
| **Quest tiếp theo** | Không |
| **Notes** | Player tự do đi lại trong Ven Sông "sáng hơn/sạch hơn" |

---

## 6. DIALOGUE BIBLE

**Nguồn chính:** `GDD_GreenAgain_NPC_DIALOGUE_v5.md`

### 6.1 Dialogue Philosophy

Mỗi cuộc trò chuyện chính cần nhịp:
1. **Hook:** NPC nói câu đời thường hoặc có cảm xúc.
2. **Context:** NPC kể hoàn cảnh.
3. **Friction:** NPC có niềm tin sai, né tránh, hoặc chưa thấy hậu quả.
4. **Player response:** Player hỏi, lắng nghe, hoặc đề nghị giúp.
5. **Turn:** NPC bắt đầu nhìn vấn đề khác đi.
6. **Objective:** Hành động gameplay xuất hiện tự nhiên.
7. **Aftermath:** NPC phản ứng sau khi player làm xong.

**Quy tắc:**
- Một dialogue chính: 8-16 line, chia nhiều bubble.
- Bubble ngắn, dễ đọc.
- NPC nói như người trong làng, không nói như sách giáo khoa.
- Player không phán xét; player hỏi, giúp, hoặc nhắc.

### 6.2 Dialogue States

| State | Mục đích |
|---|---|
| `BeforeQuest` | Tạo đời sống trước khi NPC thành mục tiêu chính |
| `IntroConversation` | Cuộc trò chuyện chính mở vấn đề |
| `PlayerChoice` | 1-2 lựa chọn phản hồi |
| `DuringQuest` | Nhắc nhẹ khi player đang làm |
| `AfterQuestConversation` | NPC nhận ra điều gì |
| `ChapterTransition` | Nối sang chương sau |
| `EndingCommitment` | NPC nói cam kết ở Nhà văn hóa |
| `PostEnding` | Free-roam sau ending |

### 6.3 Bác Xanh

**Tone:** Ấm, chậm, giàu ký ức. Không giao việc như quản lý; dẫn player nhìn kỹ hơn.

#### Ch1 — IntroConversation: Bác Xanh Và Ảnh Cũ

- **Dialogue ID:** `BacXanh_Ch1_Intro`
- **Quest:** `Q1_02_MeetBacXanh`
- **Trigger:** Player tới Nhà văn hóa lần đầu
- **Purpose:** Giới thiệu Ven Sông từng xanh, giải thích vì sao giờ khác
- **Điều kiện mở:** Quest `Q1_02` active
- **Điều kiện complete:** Dialogue complete → complete `Q1_02`, start `Q1_03`
- **Choice:** Không

**Lines:**

```
Bác Xanh: Cháu mới tới Ven Sông phải không?
Player: Dạ. Cháu thấy quanh đây có nhiều rác quá.
Bác Xanh: Ừ, bác cũng thấy. Nhưng cháu đừng để mấy túi rác kia kể hết câu chuyện về nơi này.
Bác Xanh: Nhìn tấm ảnh cũ bên kia đi. Hồi trước sân Nhà văn hóa chiều nào cũng đông. Trẻ con chạy chơi, người lớn họp xong thì ai cũng tự nhặt phần mình.
Player: Vậy sao bây giờ lại khác vậy bác?
Bác Xanh: Không phải vì người dân xấu đi. Cuộc sống chỉ nhanh hơn. Đồ mua mang đi nhiều hơn. Túi, chai, hộp... tiện hơn.
Bác Xanh: Mà khi mọi thứ tiện quá, người ta dễ nghĩ một cái vỏ nhỏ không đáng kể.
Player: Cháu có thể giúp gì trước không?
Bác Xanh: Giúp bác nhìn kỹ đoạn đường vào Nhà văn hóa đã. Nhặt vài thứ trước mắt, rồi mình đem về đúng chỗ.
Bác Xanh: Rác không biến mất chỉ vì mình nhặt nó lên. Nó cần có nơi để đi.
```

#### Ch1 — After First Cleanup

- **Dialogue ID:** `BacXanh_Ch1_AfterClean`
- **Quest:** `Q1_03_CleanEntrance` (on complete)
- **Purpose:** Chuyển tiếp sang điểm tập kết rác

```
Bác Xanh: Đường nhìn thoáng hơn rồi.
Player: Nhặt lên mới thấy nhiều thứ nhỏ thật bác.
Bác Xanh: Ừ. Thứ nhỏ nằm một mình thì dễ bỏ qua. Nằm chung lại thì thành câu chuyện khác.
Bác Xanh: Đi với bác tới điểm tập kết rác. Chị Lan sẽ chỉ cháu phần còn lại.
```

#### Chapter Transitions

- **Ch2:** "Muốn hiểu rác bắt đầu từ đâu, cháu ghé tạp hóa Cô Tư trước. Chuyện lớn nhiều khi bắt đầu từ một cái túi nhỏ..."
- **Ch3:** "Ở tạp hóa, rác đến từ thói quen hằng ngày. Còn ở sân bóng, nó đến từ những lúc vui nhất..."
- **Ch4:** "Rác quanh sân bóng còn dễ thấy. Nhưng có thứ không ở yên trên sân. Gió cuốn, mưa kéo, rồi nó đi xuống sông."
- **Ch5:** "Mình đã thấy rác đi tới đâu. Giờ phải xem nó mắc lại ở đâu..."

#### EndingCommitment

```
Bác Xanh: Hôm nay Nhà văn hóa sáng hơn mọi hôm.
Bác Xanh: Không phải vì sân đã sạch mãi mãi. Không ai hứa được chuyện đó.
Bác Xanh: Nhưng hôm nay, mỗi người ở đây đã thấy phần việc nhỏ của mình.
Bác Xanh: Cháu không làm Ven Sông xanh lại một mình.
Bác Xanh: Cháu giúp mọi người nhớ rằng từng việc nhỏ đều để lại dấu vết.
Bác Xanh: Mà nếu từng việc nhỏ có thể làm nơi này xấu đi, thì từng việc nhỏ cũng có thể làm nơi này xanh lại.
```

#### Ending Scene Final Lines

```
Bác Xanh: Nghe chưa? Không ai nhận làm hết. Mỗi người nhận một phần nhỏ.
Bác Xanh: Ngày trước Ven Sông xanh vì người ta nhớ phần nhỏ đó.
Bác Xanh: Từ hôm nay, mình nhớ lại.
Player: Ven Sông sẽ xanh lại chứ bác?
Bác Xanh: Không phải trong một ngày.
Bác Xanh: Nhưng hôm nay là một ngày Ven Sông bắt đầu xanh lại.
```

### 6.4 Chị Lan

**Tone:** Thực tế, rõ ràng, hơi mệt vì lâu nay làm một mình.

#### Ch1 — IntroConversation: Rác Đi Đâu?

- **Dialogue ID:** `ChiLan_Ch1_Intro`
- **Quest:** `Q1_04_SortFirstTrash`
- **Trigger:** Player tới Điểm tập kết rác sau khi nhặt rác đầu
- **Purpose:** Giải thích phân loại rác
- **Choice:** Không

```
Chị Lan: Em đem rác tới hả? Để chị xem.
Player: Em nhặt quanh lối vào Nhà văn hóa. Tưởng ít mà gom lại cũng nhiều.
Chị Lan: Đúng rồi. Nhưng nhặt được rác mới là một nửa thôi.
Player: Nửa còn lại là phân loại ạ?
Chị Lan: Ừ. Nếu chai nhựa, đồ ăn thừa, giấy ướt, pin cũ lẫn hết vào nhau thì sau này xử lý cực hơn nhiều.
Chị Lan: Nhiều người nghĩ bỏ vào một bao là xong. Với họ thì xong, nhưng với người gom rác thì mọi thứ mới bắt đầu.
Bác Xanh: Ven Sông không thiếu người muốn sạch. Chỉ thiếu một cách làm mà ai cũng nhớ để làm theo.
Player: Chị chỉ em phân loại lượt này với.
Chị Lan: Được. Chai nhựa để bên này. Giấy khô bên kia. Đồ ăn thừa để riêng. Mấy thứ nguy hiểm thì đừng bỏ chung.
```

- **During:** "Nhìn nhãn hoặc chất liệu trước. Không chắc thì hỏi chị."
- **After:** "Tốt đó. Thấy không, không khó. Chỉ cần đừng vội quăng chung hết." + "Nếu sau này em nói chuyện với mọi người, nhắc họ đem rác về đây."

#### Ch5 — Cống thông nhưng chưa xong

```
Chị Lan: Cống thông rồi, nhưng chị không thấy nhẹ hẳn.
Player: Vì rác có thể quay lại?
Chị Lan: Ừ. Nếu tạp hóa vẫn không có thùng, sân bóng vẫn để chai lung tung, bờ sông vẫn không ai nhắc... mình sẽ lại đứng trước cái cống này.
Chị Lan: Mình cần đặt chỗ bỏ rác dễ thấy, biển nhắc dễ nhớ, và người dân chịu nhắc nhau.
```

#### EndingCommitment

```
Chị Lan: Điểm tập kết rác mở sẵn.
Chị Lan: Ai chưa biết phân loại cứ đem tới, tôi hướng dẫn. Nhưng từ mai, mong mọi người đừng để rác đi lạc trước khi tới đây.
```

### 6.5 Cô Tư

**Tone:** Bận rộn, thực tế, đáng mến. Ban đầu hơi phòng thủ.

#### BeforeQuest

```
Cô Tư: Mua gì không con? Nước suối, bánh, kẹo đủ cả.
Cô Tư: À, tình nguyện viên hả? Cô bán cả ngày nên trước tiệm hơi bừa chút, lát cô dọn.
```

#### Ch2 — IntroConversation: Cái Túi Nhỏ

- **Dialogue ID:** `CoTu_Ch2_Intro`
- **Quest:** `Q2_01_ToGrocery`
- **Trigger:** Player gặp Cô Tư theo quest
- **Purpose:** Giải thích nhu cầu tăng → bao bì tăng → rác tăng
- **Choice:** Có (2 lựa chọn)
  1. "Một cái túi nhỏ, nhưng cả ngày nhiều người cùng bỏ thì sao cô?"
  2. "Cháu dọn phụ cô một lượt, rồi mình nhìn lại thử nhé."

```
Player: Cô Tư ơi, Bác Xanh bảo cháu ghé đây để hiểu chuyện rác trong làng.
Cô Tư: Trời, bác Xanh lại lo xa rồi. Trước tiệm cô có rác thiệt, nhưng cô vẫn quét mà.
Player: Cháu thấy nhiều túi nhỏ, vỏ bánh, chai nước quanh đường.
Cô Tư: Khách giờ ai cũng vội. Mua chai nước, gói bánh, cái túi nilon cho tiện. Cô không đưa túi thì họ than khó cầm.
Cô Tư: Ngày xưa bán ít hơn. Có khi người ta đem rổ, đem giỏ. Giờ thì cái gì cũng gói sẵn.
Player: Cô có nghĩ mấy thứ nhỏ đó trôi đi đâu không?
Cô Tư: Thú thật là cô ít nghĩ. Cô chỉ thấy trước tiệm bẩn thì quét. Cái nào bay xa rồi thì... chắc người khác dọn.
[Player choice]
Cô Tư: Ừ, con nói vậy thì cô cũng muốn xem. Chứ nhiều khi mình quen mắt rồi, không thấy nó nhiều nữa.
```

- **During:** "Con coi gần gốc cây với cạnh đường đó. Mấy cái vỏ nhỏ nhỏ bị đá vào chỗ khuất..."
- **After (commitment):**

```
Player: Cô Tư, tụi mình gom được từng này.
Cô Tư: Nhiều vậy hả? Cô tưởng chỉ vài cái vỏ bánh thôi.
Player: Mỗi cái đều nhỏ. Nhưng gom lại thì không nhỏ nữa.
Cô Tư: Cô hiểu rồi. Trước giờ cô cứ nghĩ rác trước tiệm là chuyện cô quét lúc rảnh.
Cô Tư: Nhưng nếu khách mua ở đây, rác từ đây bay ra đường, rồi trôi đi chỗ khác... cô cũng có phần trong đó.
Player: Mình đặt thùng gần đây được không cô?
Cô Tư: Được. Cô còn nhắc khách nữa. Nói nhẹ thôi, nhưng ngày nào cũng nói thì chắc thành quen.
```

#### EndingCommitment

```
Cô Tư: Từ mai cô để thùng ngay trước tiệm.
Cô Tư: Ai mua xong cô nhắc bỏ đúng chỗ. Cô cũng bớt đưa túi nếu khách không cần.
Cô Tư: Tiệm nhỏ thì phần việc cũng nhỏ thôi, nhưng cô làm được.
```

### 6.6 Anh Tùng

**Tone:** Vui, hơi xuề xòa, nói như thanh niên trong làng.

#### BeforeQuest

```
Anh Tùng: Ra sân bóng không? Chiều nay tụi anh đá vui lắm.
Anh Tùng: À, mấy cái chai kia tụi anh tính lát dọn. Đá xong ai cũng mệt mà.
```

#### Ch3 — IntroConversation: Sau Trận Bóng

- **Dialogue ID:** `AnhTung_Ch3_Intro`
- **Quest:** `Q3_02_TalkAnhTung`
- **Trigger:** Player tới sân bóng
- **Purpose:** Thói quen "lát dọn", Bé Na chen vào tạo friction
- **Choice:** Có (2 lựa chọn)
  1. "Mình dọn thử một vòng rồi nhìn sân khác thế nào nhé."
  2. "Anh giúp em chỉ những chỗ tụi anh hay để chai đi."

```
Player: Anh Tùng, sân bóng nhiều chai nước quá.
Anh Tùng: Có mấy chai thôi mà. Tụi anh đá xong mệt, lát quay lại dọn cũng được.
Bé Na: Hôm nào anh cũng nói lát.
Anh Tùng: Ủa Na, em ở đây hả?
Bé Na: Em nhặt bóng giúp mấy anh mà. Bóng lăn vào chỗ rác, em không dám lấy.
Anh Tùng: Thì... để anh lấy cho. Rác đó đâu tới mức ghê vậy.
Player: Nếu sân này là chỗ mọi người cùng chơi, ai sẽ là người dọn?
Anh Tùng: Chắc... ai rảnh? Hoặc cô chú dọn vệ sinh?
Bé Na: Nhưng người chơi nhiều nhất là mấy anh mà.
Anh Tùng: Ờ. Nghe cũng hơi kỳ. Tụi anh dùng sân nhiều nhất mà cứ để người khác dọn.
[Player choice]
Anh Tùng: Được. Mấy chỗ ghế ngồi với sau khung thành trước. Tụi anh hay để đồ ở đó.
```

- **During:** "Sau khung thành còn mấy chai đó. Ê, nhìn vậy mới thấy tụi anh để hơi nhiều thật."
- **After:**

```
Player: Sân sạch hơn rồi.
Bé Na: Giờ em chạy nhặt bóng được.
Anh Tùng: Nhìn khác hẳn. Mà thật ra dọn cũng đâu lâu.
Player: Khó nhất chắc là nhớ dọn sau khi chơi.
Anh Tùng: Ừ. Lúc vui thì ai cũng nghĩ "lát nữa". Nhưng lát nữa thường thành ngày mai.
Anh Tùng: Lần sau đá xong anh rủ tụi nó gom chai lại. Sân của tụi anh mà.
```

#### EndingCommitment

```
Anh Tùng: Tụi con đá xong sẽ tự dọn sân.
Anh Tùng: Không phải làm màu đâu. Sân của tụi con mà để bẩn thì tụi con chịu trước.
```

### 6.7 Bé Na

**Tone:** Ngắn, thật, nhìn vấn đề bằng cảm giác trực tiếp.

#### Ch3 — Intro Add-on

```
Bé Na: Em thích sân này lắm.
Bé Na: Nhưng có bữa bóng lăn vào chỗ rác, em đứng nhìn thôi. Em sợ dẫm trúng cái gì dơ.
Player: Em có nói với mấy anh chưa?
Bé Na: Em có nói. Mấy anh bảo lát dọn.
Bé Na: Nhưng "lát" lâu lắm.
```

#### After sân bóng

```
Bé Na: Sạch hơn rồi.
Bé Na: Không phải sáng bóng như mới, nhưng em thấy muốn chạy vào sân hơn.
Player: Mai em rủ bạn ra chơi được rồi đó.
Bé Na: Em sẽ rủ. Nhưng em cũng sẽ nhắc mấy bạn bỏ rác vào thùng.
```

#### Ch4 Optional

```
Bé Na: Nếu rác trôi xuống sông, cá có bị đau không?
Bác Xanh: Cá không nói được như mình. Nên mình phải nhìn kỹ hơn.
```

#### EndingCommitment

```
Bé Na: Vậy mai tụi con chơi bóng được không?
Bé Na: Con sẽ nhắc mấy bạn bỏ rác đúng chỗ. Nếu con quên, anh Tùng nhắc con nha.
```

### 6.8 Ông Sáu

**Tone:** Chậm, hoài niệm, hơi cứng đầu lúc đầu.

#### BeforeQuest

```
Ông Sáu: Ngồi đây nhìn sông quen rồi.
Ông Sáu: Hồi trước cá quẫy sát bờ, giờ thưa lắm. Chắc tại mùa, chắc tại nước đổi.
```

#### Ch4 — IntroConversation: Rác Trôi Theo Nước

- **Dialogue ID:** `OngSau_Ch4_Intro`
- **Quest:** `Q4_01_ToRiver`
- **Trigger:** Player gặp Ông Sáu sau sân bóng
- **Purpose:** Rác trên bờ → ảnh hưởng sông. Ông Sáu chưa thấy mình liên quan
- **Choice:** Không

```
Player: Ông Sáu, Bác Xanh bảo cháu xuống bờ sông xem rác đi đâu.
Ông Sáu: Rác thì ở trên bờ, dưới nước là chuyện của nước chứ.
Player: Ông hay câu cá ở đây ạ?
Ông Sáu: Ừ. Hồi xưa ngồi một lát là thấy cá quẫy. Giờ có khi cả buổi chẳng thấy gì.
Player: Ông có nghĩ rác trên bờ ảnh hưởng tới sông không?
Ông Sáu: Tui đâu có vứt xuống sông. Tui ngồi đây còn nhặt dây câu của mình đem về.
Bác Xanh: Ông Sáu không vứt xuống sông. Nhưng gió không hỏi rác của ai. Mưa cũng không hỏi.
Player: Chỗ bụi cỏ kia có mấy túi mắc lại. Có thể nước kéo từ trên xuống không ông?
Ông Sáu: Hừm... chỗ đó sau mưa hay đầy rác thật.
Ông Sáu: Nếu cháu muốn nhìn kỹ, đi dọc mép nước. Tui chỉ mấy chỗ rác hay mắc.
```

- **During:** "Chỗ bụi cỏ kia. Nước lên là rác mắc lại đó, rồi bữa sau lại trôi tiếp."
- **After (realization):**

```
Player: Rác mắc dọc bờ nhiều hơn cháu nghĩ.
Ông Sáu: Tui ngồi đây mỗi ngày mà nhìn quen mắt mất rồi.
Player: Có thứ từ sân bóng, có thứ giống túi ở tạp hóa.
Ông Sáu: Vậy là rác không ở yên chỗ người ta bỏ.
Bác Xanh: Nó đi theo đường nước. Và nơi nhận hậu quả nhiều khi không phải nơi bắt đầu.
Ông Sáu: Tui cứ nói mình không vứt xuống sông là đủ. Chắc chưa đủ thật.
```

#### EndingCommitment

```
Ông Sáu: Tui ngồi bờ sông mỗi ngày.
Ông Sáu: Ai bỏ rác, tui nhắc liền. Nhắc nhẹ thôi, nhưng không làm ngơ nữa.
```

### 6.9 Chapter 5 Community Conversations

#### Anh Hòa — Cống Nghẹt

```
Anh Hòa: Mỗi lần mưa lớn là nước dềnh lên chỗ này.
Player: Do cống nhỏ quá hả anh?
Anh Hòa: Cống nhỏ là một phần. Nhưng nhìn miệng cống đi.
Anh Hòa: Chai nước, túi nilon, bao snack, lá mục... thứ nào cũng nhỏ. Gặp nhau ở đây thì thành nút chặn.
Bác Xanh: Rác từ nhiều nơi cuối cùng lại biết đường gặp nhau.
Anh Hòa: Thông được hôm nay thì tốt. Nhưng nếu trên kia vẫn xả như cũ, cống này chỉ nghỉ được vài bữa.
```

#### After Clear Drain — Bác Xanh + Chị Lan

```
Player: Nước chảy lại rồi.
Chị Lan: Ừ, nhưng chị không muốn tuần sau lại đứng đây.
Bác Xanh: Dọn cống là xử lý phần cuối của câu chuyện.
Player: Vậy phần đầu là tạp hóa, sân bóng, bờ sông?
Bác Xanh: Và cả những lúc mọi người nghĩ "một chút thôi mà".
Chị Lan: Mình cần rủ mọi người đặt lại cách làm. Có chỗ bỏ rác. Có người nhắc. Có điểm tập kết thật sự được dùng.
```

#### Gather — Cô Tư

```
Player: Cô Tư, tụi cháu thấy túi nilon mắc ở cống.
Cô Tư: Cô nghe mà chột dạ. Không biết có cái nào từ tiệm cô không.
Player: Không cần biết cái nào của ai. Nhưng mình biết rác ở tiệm có thể đi xa.
Cô Tư: Ừ. Vậy cô nhận phần tiệm cô.
Cô Tư: Thùng rác để ngay trước cửa. Khách mua xong cô nhắc. Ai không cần túi thì cô khỏi đưa.
```

#### Gather — Anh Tùng

```
Player: Anh Tùng, có bao snack giống loại tụi anh hay ăn mắc ở cống.
Anh Tùng: Nghe quê thiệt.
Player: Không phải để trách anh. Nhưng sân bóng nối với bờ sông gần hơn mình nghĩ.
Anh Tùng: Ừ. Tụi anh đá xong mà không gom, gió với mưa gom giùm. Mà gom tới chỗ tệ hơn.
Anh Tùng: Để anh rủ tụi nó làm luật sân: đá xong gom chai, gom túi rồi mới về.
```

#### Gather — Ông Sáu

```
Player: Ông Sáu, rác từ bờ sông trôi xuống cống thật rồi.
Ông Sáu: Tui thấy. Nhìn cái cống nghẹt mới hết cãi được.
Player: Ông vẫn ngồi bờ sông mỗi ngày chứ?
Ông Sáu: Ngồi chứ. Từ mai tui ngồi thêm một việc nữa: ai bỏ rác, tui nhắc.
Ông Sáu: Sông không tự lên tiếng được. Người ngồi cạnh sông phải lên tiếng giùm.
```

### 6.10 Ending Scene Dialogue (Full)

**Trigger:** Player nói chuyện Bác Xanh ở Nhà văn hóa sau Q5.

```
Bác Xanh: Mọi người tới đủ rồi.
Bác Xanh: Hôm nay mình không họp để khen ai. Mình họp để nhớ một chuyện đơn giản: Ven Sông là chỗ chung.
Chị Lan: Điểm tập kết rác mở sẵn. Ai chưa biết phân loại cứ đem tới, tôi hướng dẫn.
Cô Tư: Tạp hóa của tôi sẽ có thùng rác trước cửa. Tôi cũng bớt đưa túi nếu khách không cần.
Anh Tùng: Sân bóng tụi con chơi thì tụi con dọn. Đá xong mới được về.
Ông Sáu: Tui ngồi bờ sông mỗi ngày. Tui sẽ nhắc người câu cá, người đi ngang, và nhắc cả tui nữa.
Bé Na: Con cũng nhắc mấy bạn. Nhưng người lớn nhớ làm trước nha.
Bác Xanh: Nghe chưa? Không ai nhận làm hết. Mỗi người nhận một phần nhỏ.
Bác Xanh: Ngày trước Ven Sông xanh vì người ta nhớ phần nhỏ đó.
Bác Xanh: Từ hôm nay, mình nhớ lại.
Player: Ven Sông sẽ xanh lại chứ bác?
Bác Xanh: Không phải trong một ngày.
Bác Xanh: Nhưng hôm nay là một ngày Ven Sông bắt đầu xanh lại.
```

**End text:**

> Ven Sông chưa sạch mãi mãi.
> Nhưng Ven Sông đã có người cùng chăm.

### 6.11 NPC Phụ — Dialogue

**Nguồn chính:** `GDD_GreenAgain_NPC_DIALOGUE_v5.md` (Section 11)

Mỗi NPC phụ có Before/After lines ngắn. Đã có đầy đủ trong docs, tóm tắt:

| NPC Phụ | Before (trước ending) | After (sau quest liên quan) |
|---|---|---|
| **Bác Bảy** (bảo vệ NVH) | "Hồi trước họp xong ai cũng tự nhặt..." | "Chiều nay sân NVH sáng hơn..." |
| **Chú Minh** (xe rác) | "Rác mà lẫn hết thì chở cũng cực..." | "Phân loại từ đầu là đỡ cho người gom..." |
| **Cô Hạnh** (tổ dân phố) | "Nhắc thì ai cũng gật..." | "Mỗi nhà nhớ một chút, đỡ nhắc bằng loa..." |
| **Em Phúc** (học sinh) | "Con đi học ngang đây mỗi ngày..." | "Đường sạch hơn, con đi học vui hơn..." |
| **Dì Năm** (bán nước) | "Bán nước gần sân bóng vui, mà chai bỏ lại nhiều..." | "Nếu có thùng gần sân, dì nhắc khách..." |
| **Nam** (thủ môn) | "Tui bắt bóng dở, dọn sân chắc khá hơn..." | "Đội thua gom rác trước..." |
| **Cô Mai** (phụ huynh) | "Tụi nhỏ mê sân... nhưng rác nhiều cô ngại..." | "Sân sạch thì người lớn yên tâm hơn..." |
| **Chú Lộc** (câu cá) | "Tui tưởng cá ít là do mùa..." | "Nhìn rác mắc bờ mới thấy mình cũng phải để ý..." |
| **Bà Tám** (ven sông) | "Hồi xưa nước trong tới mức nhìn thấy đáy..." | "Muốn xanh lại... phải làm mấy chuyện nhỏ hôm nay..." |
| **Anh Hòa** (thợ sửa cống) | "Mưa xuống là nước dềnh lên..." | "Thông cống một lần thì được. Nhưng giữ cho nó khỏi nghẹt lại mới là chuyện cả xóm." |

---

## 7. NPC ROLE VÀ MOVEMENT SPEC

**Nguồn chính:** `GDD_GreenAgain_v5_STORY_BIBLE.md` (Section 5), `GDD_GreenAgain_NPC_DIALOGUE_v5.md`, `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`

### 7.1 Bác Xanh

| Mục | Chi tiết |
|---|---|
| **Tính cách** | Ấm, chậm, giàu ký ức. Không ra lệnh. Hay nói "hồi trước", "cháu nhìn kỹ xem" |
| **Vai trò story** | Mentor, người giữ ký ức Ven Sông, nhịp cảm xúc chính |
| **Arc** | Cô đơn giữ ký ức → thấy player lắng nghe → thấy cộng đồng cùng nhận ra |
| **Location mặc định** | Nhà văn hóa thôn Ven Sông |
| **Quest xuất hiện** | Q1_02, chapter transitions, Q5_02-05, ending |
| **Interactable khi** | Q1_02 (intro), sau mỗi chapter clean (transition), Q5_05 (ending) |
| **Không interactable khi** | Trong lúc player đang cleanup/placement, khi dialogue khác đang chạy |

**`Đề xuất bổ sung` — Movement/Staging:**

| Scene | Vị trí đề xuất | Animation đề xuất |
|---|---|---|
| **Q1_02 Intro** | Đứng gần ảnh/bảng "Ven Sông Xanh" trong Nhà văn hóa, quay mặt về hướng player spawn | Idle đứng, tay sau lưng hoặc chắp trước |
| **Chapter transitions** | Vẫn đứng tại Nhà văn hóa, hoặc ở gần vị trí quest trước (nếu muốn Bác xuất hiện tại chỗ) | Idle đứng |
| **Ch4 Bờ sông** | Xuất hiện cùng player ở bờ sông (Bác Xanh có line cùng Ông Sáu) | `Chưa rõ / cần xác nhận`: Bác Xanh teleport/walk tới hay đã đứng sẵn? Đề xuất: Bác Xanh đứng sẵn gần bờ sông khi quest Ch4 active |
| **Ch5 Cống** | Xuất hiện gần cống để nói line cùng Chị Lan/Anh Hòa | `Đề xuất bổ sung`: Bác Xanh đứng sẵn khi player tới cống |
| **Ending** | Đứng ở trung tâm sân Nhà văn hóa, hướng về nhóm NPC | Idle → nói → kết thúc |
| **Idle animation** | `Đề xuất bổ sung`: Đứng nhìn xa, thỉnh thoảng nhìn ảnh cũ | Animation R15 cơ bản: idle stand |

### 7.2 Chị Lan

| Mục | Chi tiết |
|---|---|
| **Tính cách** | Thực tế, rõ ràng, hơi mệt vì lâu nay làm một mình |
| **Vai trò story** | Hệ thống rác/phân loại, biến cảm xúc thành cách làm |
| **Arc** | Hơi bất lực → thấy người dân hợp tác → tự tin hướng dẫn |
| **Location mặc định** | Gần Điểm tập kết rác |
| **Quest xuất hiện** | Q1_04, Q5_02-03, ending |
| **Interactable khi** | Q1_04 (sorting tutorial), Q5_02 (after drain clear) |
| **Không interactable khi** | Ch2-Ch4 (không phải mục tiêu chính) |

**`Đề xuất bổ sung` — Movement/Staging:**

| Scene | Vị trí đề xuất | Animation đề xuất |
|---|---|---|
| **Q1_04 Sorting** | Đứng gần thùng/giỏ phân loại tại Điểm tập kết rác | Idle đứng, hướng về phía thùng |
| **Ch5 Cống** | Xuất hiện gần cống sau khi player clear drain (có line reaction) | `Đề xuất bổ sung`: Teleport/walk tới cống khi quest Q5_02 complete |
| **Ending** | Đứng trong nhóm NPC tại Nhà văn hóa | Idle đứng |

### 7.3 Cô Tư

| Mục | Chi tiết |
|---|---|
| **Tính cách** | Bận rộn, thực tế, đáng mến. Ban đầu hơi phòng thủ |
| **Vai trò story** | Nhu cầu sinh hoạt tăng → bao bì tăng → rác đời thường |
| **Arc** | Phòng thủ nhẹ → nhận ra số lượng cộng dồn → chủ động nhắc khách |
| **Location mặc định** | Tạp hóa Cô Tư (`TapHoaCoTu_HouseOnly_Rural`) |
| **Quest xuất hiện** | Q2_01, Q2_05, Q5_04, ending |
| **Interactable khi** | Q2_01 (intro), Q2_05 (commitment), Q5_04 (gather) |
| **Không interactable khi** | Ch1, Ch3-4 (không phải mục tiêu chính) |

**`Đề xuất bổ sung` — Movement/Staging:**

| Scene | Vị trí đề xuất | Animation đề xuất |
|---|---|---|
| **Q2_01 Intro** | Đứng trước quầy tạp hóa hoặc trước cửa tiệm | Idle đứng, tay chắp sau hoặc lau quầy |
| **Q2_04 Commitment** | Vẫn trước tạp hóa | Idle → nói → player đặt thùng gần đó |
| **Q5_03 Gather** | `Chưa rõ / cần xác nhận`: Cô Tư vẫn ở tạp hóa hay player quay lại tạp hóa gặp? Đề xuất: player quay về tạp hóa, Cô Tư đứng sẵn | — |
| **Ending** | Đứng trong nhóm NPC tại Nhà văn hóa | `Đề xuất bổ sung`: Cô Tư được teleport về NVH khi ending trigger |

### 7.4 Anh Tùng

| Mục | Chi tiết |
|---|---|
| **Tính cách** | Vui, hơi xuề xòa, nói như thanh niên trong làng. Không xấu tính |
| **Vai trò story** | Thói quen "có người dọn" ở sân bóng |
| **Arc** | Vô tư → hơi ngại khi thấy hậu quả → rủ nhóm bạn dọn sân |
| **Location mặc định** | Sân bóng (gần `KhungThanh_01_Marker` hoặc `KhungThanh_02_Marker`) |
| **Quest xuất hiện** | Q3_01-05, Q5_03, ending |
| **Interactable khi** | Q3_02 (intro), Q5_04 (gather) |
| **Không interactable khi** | Ch1-2, Ch4 |

**`Đề xuất bổ sung` — Movement/Staging:**

| Scene | Vị trí đề xuất | Animation đề xuất |
|---|---|---|
| **Q3_02 Intro** | Đứng gần sân bóng, hướng về phía ghế ngồi | `Đề xuất bổ sung`: Idle chống hông hoặc cầm chai nước |
| **Q3_03 During** | Vẫn đứng gần sân, có thể chỉ hướng rác | Idle |
| **Q5_03 Gather** | `Chưa rõ / cần xác nhận`: Player quay lại sân bóng gặp Anh Tùng? Đề xuất: vẫn ở sân bóng | — |
| **Ending** | Đứng trong nhóm NPC tại Nhà văn hóa | Teleport về NVH |

### 7.5 Bé Na

| Mục | Chi tiết |
|---|---|
| **Tính cách** | Ngắn, thật, nhìn vấn đề bằng cảm giác trực tiếp |
| **Vai trò story** | Cảm xúc trong sáng, đại diện thế hệ sau |
| **Arc** | Khó chịu/buồn → gọi người lớn nhìn lại → vui khi cộng đồng hứa |
| **Location mặc định** | Gần sân bóng, rìa sân |
| **Quest xuất hiện** | Q3_02-04, ending |
| **Interactable khi** | Q3_04 (BeNa moment) |
| **Không interactable khi** | Ch1-2, Ch4-5 (trừ ending) |

**`Đề xuất bổ sung` — Movement/Staging:**

| Scene | Vị trí đề xuất | Animation đề xuất |
|---|---|---|
| **Q3_02** | Đứng ở rìa sân, hơi ngại bước vào | `Đề xuất bổ sung`: Idle nhìn xuống / ôm bóng |
| **Q3_04** | Vẫn gần sân, sau khi sân sạch | Idle vui hơn |
| **Ending** | Đứng trong nhóm NPC tại Nhà văn hóa | Teleport về NVH |
| **`Đề xuất bổ sung`** | Nếu có thể, cho Bé Na chạy nhặt bóng animation sau khi sân sạch | — |

### 7.6 Ông Sáu

| Mục | Chi tiết |
|---|---|
| **Tính cách** | Chậm, hoài niệm, hơi cứng đầu lúc đầu |
| **Vai trò story** | Ký ức bờ sông, hiểu nhầm nhân quả |
| **Arc** | Hoài niệm → thấy đường rác đi → trở thành người nhắc bờ sông sạch |
| **Location mặc định** | Bờ sông (`NPC_OngSau_Marker`) |
| **Quest xuất hiện** | Q4_01-03, Q5_03, ending |
| **Interactable khi** | Q4_01 (intro), Q4_04 (realization), Q5_04 (gather) |
| **Không interactable khi** | Ch1-3 |

**`Đề xuất bổ sung` — Movement/Staging:**

| Scene | Vị trí đề xuất | Animation đề xuất |
|---|---|---|
| **Q4_01 Intro** | Ngồi hoặc đứng bên bờ sông, nhìn về phía sông | `Đề xuất bổ sung`: Idle ngồi câu cá hoặc đứng nhìn sông |
| **Q4_02 During** | Vẫn ở bờ sông, chỉ hướng rác mắc | Idle + chỉ tay |
| **Q4_03 Realization** | Vẫn ở bờ sông | Idle |
| **Q5_03 Gather** | `Chưa rõ / cần xác nhận`: Player quay lại bờ sông gặp Ông Sáu? Đề xuất: player quay về | — |
| **Ending** | Đứng trong nhóm NPC tại Nhà văn hóa | Teleport về NVH |

---

## 8. CUTSCENE VÀ STAGING

**Nguồn chính:** `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`

### 8.1 Cutscene Style (Theo docs)

- Thời lượng lý tưởng: 20-60 giây.
- Chỉ dùng cinematic camera cho moment quan trọng.
- Các đoạn nhỏ dùng dialogue lock + camera focus nhẹ.
- Không dùng cutscene để giảng bài dài.
- Mỗi cutscene kết thúc bằng objective rõ ràng.

### 8.2 CS0 — Bước Qua Cổng

| Mục | Chi tiết |
|---|---|
| **ID** | CS0 |
| **Chapter** | Lobby → Main |
| **Trigger** | Player teleport từ lobby sang map chính |
| **Camera** | Nhìn từ sau player về hướng Nhà văn hóa |
| **Player control lock** | Có (fade in) |
| **NPC positioning** | Không NPC |
| **Dialogue/text** | Text on screen: "Thôn Ven Sông — Một nơi từng xanh hơn những gì bạn đang thấy." |
| **Fade/transition** | Fade in từ đen |
| **Objective before** | (không có) |
| **Objective after** | "Đi tới Nhà văn hóa" |
| **MVP implementation** | `Đã build` — CS0 plays once after teleport |
| **`Đề xuất bổ sung` Polish** | Thêm ambient sound (chim, gió nhẹ). Camera pan chậm qua cảnh Ven Sông trước khi unlock player |

### 8.3 CS1 — Bác Xanh Và Ảnh Cũ

| Mục | Chi tiết |
|---|---|
| **ID** | CS1 |
| **Chapter** | Ch1 |
| **Trigger** | Player tới vùng Nhà văn hóa lần đầu |
| **Camera** | Focus ảnh cũ → chuyển sang Bác Xanh |
| **Player control lock** | Có (dialogue lock) |
| **NPC positioning** | Bác Xanh đứng gần ảnh/bảng "Ven Sông Xanh" |
| **Dialogue** | Bác Xanh intro conversation (10 lines, xem Section 6.3) |
| **Fade/transition** | Không fade, chỉ camera focus |
| **Objective before** | "Đi tới Nhà văn hóa" |
| **Objective after** | "Nhặt rác quanh lối vào Nhà văn hóa" |
| **MVP implementation** | `Đã build` — CS1 plays once, dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Camera cinematic: zoom chậm vào ảnh cũ → pull back reveal Bác Xanh |

### 8.4 CS1B — Điểm Tập Kết Rác

| Mục | Chi tiết |
|---|---|
| **ID** | CS1B |
| **Chapter** | Ch1 |
| **Trigger** | Sau nhặt rác đầu / Bác Xanh dẫn tới Chị Lan |
| **Camera** | Nhìn Điểm tập kết rác |
| **Player control lock** | Có (dialogue lock) |
| **NPC positioning** | Chị Lan đứng gần thùng/giỏ phân loại |
| **Dialogue** | Chị Lan intro conversation (xem Section 6.4) |
| **Objective after** | "Phân loại rác đầu tiên" |
| **MVP implementation** | `Đã build` — dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Camera focus vào khu phân loại, highlight thùng khác loại |

### 8.5 CS2 — Cái Túi Nhỏ

| Mục | Chi tiết |
|---|---|
| **ID** | CS2 |
| **Chapter** | Ch2 |
| **Trigger** | Player gặp Cô Tư ở tạp hóa |
| **Camera** | `Đề xuất bổ sung`: Camera focus Cô Tư trước quầy, nhìn rác nhỏ quanh tiệm |
| **Player control lock** | Có (dialogue lock) |
| **NPC positioning** | Cô Tư đứng trước quầy, rác nhỏ quanh tạp hóa |
| **Dialogue** | Cô Tư intro conversation + player choice (xem Section 6.5) |
| **Objective after** | "Dọn rác quanh tạp hóa" |
| **MVP implementation** | `Đã build` — dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Camera sweep nhẹ từ quầy tạp hóa ra đường, cho thấy túi nilon bay |

### 8.6 CS3 — Sau Trận Bóng

| Mục | Chi tiết |
|---|---|
| **ID** | CS3 |
| **Chapter** | Ch3 |
| **Trigger** | Player tới sân bóng |
| **Camera** | `Đề xuất bổ sung`: Camera wide shot sân bóng, thấy rác rải rác |
| **Player control lock** | Có (dialogue lock) |
| **NPC positioning** | Anh Tùng gần sân, Bé Na ở rìa sân hơi ngại bước vào |
| **Dialogue** | Anh Tùng + Bé Na intro + player choice (xem Section 6.6) |
| **Objective after** | "Dọn rác quanh sân bóng" |
| **MVP implementation** | `Đã build` — dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Bé Na animation nhặt bóng bị kẹt gần rác, Anh Tùng gãi đầu |

### 8.7 CS4 — Rác Trôi Theo Nước

| Mục | Chi tiết |
|---|---|
| **ID** | CS4 |
| **Chapter** | Ch4 |
| **Trigger** | Player gặp Ông Sáu ở bờ sông |
| **Camera** | Nhìn từ sân bóng qua Ông Sáu rồi xuống bờ sông |
| **Player control lock** | Có (dialogue lock) |
| **NPC positioning** | Ông Sáu đứng/ngồi bờ sông. Rác mắc mép nước |
| **Dialogue** | Ông Sáu intro + Bác Xanh insight (xem Section 6.8) |
| **Objective after** | "Theo dấu rác dọc bờ sông" |
| **MVP implementation** | `Đã build` — dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Camera pan dọc sông cho thấy rác mắc dần dần. Ông Sáu nhìn sông, mặt buồn |

### 8.8 CS5A — Cống Nghẹt

| Mục | Chi tiết |
|---|---|
| **ID** | CS5A |
| **Chapter** | Ch5 |
| **Trigger** | Player tới Cống thoát nước cuối xóm |
| **Camera** | Camera thấp nhìn rác mắc ở miệng cống. Nước chảy chậm/màu tối |
| **Player control lock** | Có |
| **NPC positioning** | Anh Hòa đứng gần cống. Bác Xanh có thể đứng gần |
| **Dialogue** | Anh Hòa + Bác Xanh cống nghẹt conversation (xem Section 6.9) |
| **Objective after** | "Dọn rác mắc ở cống" |
| **MVP implementation** | `Đã build` — dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Nước đổi màu, particle mùi/bọt nổi. Sound effect nước ứ |

### 8.9 CS5B — Dọn Cống Không Đủ

| Mục | Chi tiết |
|---|---|
| **ID** | CS5B |
| **Chapter** | Ch5 |
| **Trigger** | Player clear cống |
| **Camera** | Nước chảy tốt hơn, camera không ăn mừng quá lớn, giữ tone suy nghĩ |
| **Player control lock** | Có (dialogue lock) |
| **NPC positioning** | Chị Lan + Bác Xanh gần cống |
| **Dialogue** | After clear drain conversation (xem Section 6.9) |
| **Objective after** | "Rủ mọi người cùng thay đổi" |
| **MVP implementation** | `Đã build` — dialogue-driven |
| **`Đề xuất bổ sung` Polish** | Nước đổi từ tối sang trong. Ánh sáng nhẹ hơn |

### 8.10 CS5C — Lời Hứa Nhà Văn Hóa (Ending)

| Mục | Chi tiết |
|---|---|
| **ID** | CS5C |
| **Chapter** | Ch5 (ending) |
| **Trigger** | Player quay về Nhà văn hóa, nói chuyện Bác Xanh |
| **Camera** | `Đề xuất bổ sung`: Camera wide shot NVH sáng hơn. NPC chính đứng thành nhóm |
| **Player control lock** | Có |
| **NPC positioning** | Bác Xanh trung tâm. Chị Lan, Cô Tư, Anh Tùng, Ông Sáu, Bé Na xung quanh. NPC phụ đã gặp đứng phía sau (nếu có) |
| **Dialogue** | Ending scene dialogue đầy đủ (xem Section 6.10) |
| **Fade/transition** | End text overlay → fade |
| **Objective after** | `PostEnding_FreeRoam` — "Giữ Ven Sông xanh" |
| **MVP implementation** | `Đã build` — ending fires once, end text overlay |
| **`Đề xuất bổ sung` Polish** | NVH thêm đèn/ánh sáng ấm. NPC có animation gật đầu khi nói commitment. Camera xoay chậm quanh nhóm NPC |

---

## 9. GAMEPLAY SYSTEMS

**Nguồn chính:** `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`, `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`

> **Lưu ý quan trọng:** Tất cả system hiện tại nằm trong `StoryRuntimeMVP` (server) và `StoryClientMVP` (client), **chưa tách module**. Implementation plan docs mô tả kiến trúc modular (QuestManager, DialogueService, etc.) nhưng MVP hiện tại gộp tất cả trong 2 script.

### 9.1 Story State

- Per-player story state lưu:
  - `currentQuestId` — quest đang active
  - `chapter` — chapter hiện tại
  - `cleanupCounts` — số rác đã nhặt trong quest cleanup hiện tại
  - `placementCounts` — số placement đã đặt
  - `communityProgress` — số NPC đã gather trong Q5_03
  - `notebookFlags` — chapter nào đã fire notebook
  - `endingFlag` — ending đã chạy chưa
- **Trạng thái:** `Đã build` trong `StoryRuntimeMVP`

### 9.2 Quest Manager

- Quản lý quest chain: start → advance → complete.
- Mỗi quest có `QuestId`, `Title`, `Chapter`, `ObjectiveText`, `TargetType`, `TargetId`, `CompleteTrigger`, `NextQuestId`.
- **Trạng thái:** `Đã build` trong `StoryRuntimeMVP` (chưa tách thành module riêng)

### 9.3 Dialogue Service

- Data-driven: dialogue lưu theo ID, gồm lines[], speaker, choices, onComplete.
- Server gửi dialogue data cho client qua remote event.
- Client hiển thị dialogue panel.
- **Trạng thái:** `Đã build` trong `StoryRuntimeMVP` + `StoryClientMVP`

### 9.4 Interaction Router

- Xử lý khi player interact (`E` key) với object trong map.
- Route tới đúng handler dựa trên object attributes: NPC talk, location enter, trash pickup, placement, drain.
- **Trạng thái:** `Đã build` trong `StoryRuntimeMVP`

### 9.5 Objective Event

- Server fire `OnObjectiveChanged` khi quest đổi.
- Client nhận và cập nhật quest tracker + marker.
- **Trạng thái:** `Đã build`

### 9.6 Runtime Cleanup Spawning

- Server spawn runtime trash models khi cleanup quest bắt đầu.
- Trash position đã được fix: spawn gần ground height.
- Khi player nhặt trash, trash ẩn/destroy, cleanup count tăng.
- **Trạng thái:** `Đã build`

### 9.7 Runtime Placement Spawning

- Server tạo runtime placement markers cho prevention/placement actions (Q3_05, Q5_04).
- Player interact với marker → placement count tăng.
- **Trạng thái:** `Đã build`

### 9.8 Drain Interaction

- Object `OngThoatNuoc` chỉ interactable khi Q5_02 active.
- Player interact → clear drain trash → quest advance.
- **Trạng thái:** `Đã build`

### 9.9 Community Gather

- Q5_03: Player quay lại gặp NPC chính (Cô Tư, Anh Tùng, Ông Sáu).
- Mỗi NPC talk → communityProgress tăng.
- Khi ≥ 3 NPC reactions → quest complete.
- **Trạng thái:** `Đã build`

### 9.10 Notebook Entry

- Fire 1 lần mỗi chapter khi quest liên quan complete.
- Client lưu entry thành trang của chapter tương ứng, tự mở cuốn nhật ký tới trang mới, và cho player lật lại các trang đã unlock.
- **Trạng thái:** `Đã build`

### 9.11 Ending / Free Roam

- Ending fires once khi Q5_05 complete.
- Ending dialogue sequence → end text overlay.
- Sau ending → `PostEnding_FreeRoam`: player tự do, không marker.
- **Trạng thái:** `Đã build`

### 9.12 Sprint

- `SprintStaminaScript` trong `StarterCharacterScripts`.
- Giữ Shift → chạy nhanh hơn (walk speed thay đổi).
- Stamina bar UI đã xóa.
- **Trạng thái:** `Đã build`

---

## 10. UI/UX SPEC ĐẦY ĐỦ

**Nguồn chính:** `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`

### 10.1 Quest Tracker

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Khi player đã vào main map VÀ có quest active |
| **Khi ẩn** | Khi player ở lobby/khu nối. Khi `PostEnding_FreeRoam` active (không còn quest tracker rõ) |
| **Text hiển thị** | Chapter + quest title + objective text. Ví dụ: "Ch1 — Gặp Bác Xanh / Nói chuyện với Bác Xanh" |
| **Input liên quan** | Không (passive display) |
| **Visual style** | Nhỏ, ít intrusive. `Đã build` — UI updated to be smaller and cleaner |
| **Edge cases** | Phải ẩn hoàn toàn khi ở lobby, không hiện placeholder |
| **Mobile** | `Đề xuất bổ sung`: Responsive scale đã thêm cho smaller screens |
| **Accessibility** | `Đề xuất bổ sung`: Font đủ lớn, contrast cao trên nền game |

### 10.2 Objective Marker

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Khi có quest active VÀ player ở main map |
| **Khi ẩn** | Khi player ở lobby/khu nối. Khi `PostEnding_FreeRoam`. Khi dialogue đang mở |
| **Text hiển thị** | Tên target tiếng Việt (ví dụ: "Bác Xanh", "Tạp hóa Cô Tư", "Cống thoát nước cuối xóm") |
| **Visual style** | Hình thoi xanh nhỏ (green diamond) + tên. **KHÔNG có distance text** |
| **Số lượng** | **Chỉ MỘT marker** active tại một thời điểm |
| **Input** | Không |
| **Edge cases** | Marker KHÔNG hiện ở khu nối/lobby. Marker chỉ hiện sau teleport vào main map |
| **Mobile** | Responsive |
| **Accessibility** | Tên rõ ràng, màu nổi bật |

### 10.3 Interaction Prompt

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Khi player đứng gần object interactable VÀ object đó đúng quest state |
| **Khi ẩn** | Khi player xa object. Khi dialogue đang mở. Khi object không interactable |
| **Text hiển thị** | Format: `[E]  Action - Object`. Ví dụ: `[E] Nói chuyện - Bác Xanh` |
| **Input** | `E` key (keyboard). `Đề xuất bổ sung`: Tap button (mobile) |
| **Visual style** | Nhỏ, gần dưới giữa màn hình |
| **Edge cases** | Chỉ hiện khi object đang ở trạng thái quest đúng |
| **Mobile** | `Chưa rõ / cần xác nhận`: Có nút tap riêng không? Đề xuất: thêm nút tap |

### 10.4 Dialogue Panel

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Khi dialogue được trigger bởi interaction |
| **Khi ẩn** | Khi dialogue kết thúc (tự đóng) |
| **Text hiển thị** | Speaker name + dialogue text + line progress (`1 / 4`) |
| **Input** | `E` key hoặc nút continue để next line. Click/tap choice button nếu có |
| **Visual style** | Panel rộng, dễ đọc. Speaker name nổi bật |
| **Edge cases** | Debounce: dialogue đã complete không mở lại ngay. Không cho spam `E` qua hết dialogue |
| **Mobile** | `Đã build` — responsive scale |
| **Accessibility** | Font đủ lớn, contrast cao |

### 10.5 Choice Buttons

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Khi dialogue có choices (chỉ 1-2 lựa chọn) |
| **Khi ẩn** | Sau khi player chọn |
| **Text** | Text của từng choice option |
| **Input** | Click/tap |
| **Visual style** | `Đề xuất bổ sung`: Buttons rõ ràng, hover highlight |
| **Edge cases** | Choices không phân nhánh lớn — cả 2 option dẫn tới cùng kết quả story |

### 10.6 Feedback Toast

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Khi player hoàn thành action (nhặt rác, đặt thùng, etc.) |
| **Khi ẩn** | Auto-dismiss sau vài giây |
| **Text** | Feedback ngắn (ví dụ: confirmation text) |
| **Visual style** | Consistent với HUD mới |

### 10.7 Notebook Book

| Mục | Chi tiết |
|---|---|
| **Khi mở khóa** | 1 lần mỗi chapter khi quest liên quan complete |
| **Khi hiện** | Client tự mở cuốn nhật ký tới trang chương vừa unlock; sau đó player có thể mở lại bằng nút `Nhật ký` hoặc phím `N` |
| **Khi ẩn** | Player bấm `Đóng`, phím `Esc`, hoặc UI story bị ẩn khi vào menu/minigame/dialogue |
| **Text** | Notebook entry text (xem Section 5, mỗi chapter có entry riêng) |
| **Visual style** | Panel dạng cuốn sổ hai trang: bìa Green Again bên trái, nội dung chương bên phải, nút `Trước`/`Sau` để lật lại các trang đã unlock |
| **Edge cases** | Chỉ fire 1 lần/chapter — tracked bằng `notebookFlags`; client giữ các trang đã unlock trong session để xem lại |

### 10.8 Ending Overlay

| Mục | Chi tiết |
|---|---|
| **Khi hiện** | Sau ending dialogue sequence |
| **Khi ẩn** | Sau player dismiss hoặc auto-transition tới free roam |
| **Text** | "Ven Sông chưa sạch mãi mãi. Nhưng Ven Sông đã có người cùng chăm." |
| **Visual style** | Full screen overlay, text centered |
| **Edge cases** | Chỉ chạy 1 lần (ending flag) |

### 10.9 Sprint UI

| Mục | Chi tiết |
|---|---|
| **Trạng thái** | `Đã xóa` — Stamina bar UI không còn |
| **Sprint logic** | Vẫn hoạt động (Shift = chạy nhanh) |
| **UI** | Không hiển thị gì |

---

## 11. BUILD GUIDE DÀNH CHO CODEX

**Nguồn chính:** `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`, `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`, `README.md`

### 11.1 Cách đọc docs

1. Đọc `docs/README.md` trước — hiểu vai trò từng file.
2. Đọc document tổng hợp này (file hiện tại) để nắm toàn bộ bức tranh.
3. Khi cần chi tiết cụ thể, tham khảo file nguồn:
   - Quest IDs/triggers → `GDD_GreenAgain_v5_QUEST_FLOW.md`
   - Dialogue lines → `GDD_GreenAgain_NPC_DIALOGUE_v5.md`
   - Cutscene staging → `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`
   - Story/character → `GDD_GreenAgain_v5_STORY_BIBLE.md`
   - Map → `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
   - Trash asset library → `GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md`

### 11.2 Cách kiểm tra Roblox Studio workspace

1. Mở Roblox Studio, load project Green Again.
2. Trong Explorer, tìm `Workspace["=== GREEN AGAIN V5 ==="]`.
3. Xác nhận `MAP_ROUTE` tồn tại.
4. Xác nhận `MAP_ROUTE.06_NPCs` chứa: `BacXanh`, `ChiLan`, `CoTu`, `AnhTung`, `BeNa`, `OngSau`.
5. Xác nhận `NhaVanHoa_ThonNoiChuan`, `DiemTapKetRacThai_ThonVenSong`, `TapHoaCoTu_HouseOnly_Rural` tồn tại.
6. Xác nhận `OngThoatNuoc` tại `SYSTEMS_REVIEW.Doors_Vehicles_And_AssetScripts`.
7. Nếu làm với model rác, xác nhận chỉ có một `Workspace.Trash` dạng `Folder`, source templates có `Interactable=false`, và runtime clone sẽ nằm trong `Workspace.GreenAgainV5_StoryRuntime`.

### 11.3 Cách xác nhận object path

```lua
-- Trong Command Bar hoặc script:
local root = workspace:FindFirstChild("=== GREEN AGAIN V5 ===")
print(root and "Root OK" or "ROOT MISSING")

local npcs = root and root:FindFirstChild("MAP_ROUTE") and root.MAP_ROUTE:FindFirstChild("06_NPCs")
print(npcs and "NPCs folder OK" or "NPCs MISSING")

-- Kiểm tra từng NPC:
for _, name in {"BacXanh","ChiLan","CoTu","AnhTung","BeNa","OngSau"} do
    print(name, npcs and npcs:FindFirstChild(name) and "OK" or "MISSING")
end
```

### 11.4 Quy tắc quan trọng

#### KHÔNG tạo placeholder

- **KHÔNG** tạo placeholder model cho sân bóng/cống. Dùng object thật đã có trong workspace.
- Sân bóng = khu vực giữa `KhungThanh_01_Marker` và `KhungThanh_02_Marker`.
- Cống = `OngThoatNuoc` đã có.

#### Dùng object thật

- Luôn `FindFirstChild` hoặc search trong workspace thật.
- Nếu object không tìm thấy, **dừng lại và báo** — không tạo mới.

#### Anti-drift rules

- KHÔNG gọi `PicnicArea` là "Công viên" trong story/UI.
- KHÔNG gọi `Dam_C1/C2/C3` là "Đập" trong story/UI.
- KHÔNG dùng scanner làm objective chính.
- KHÔNG bắt đầu quest bằng nhặt rác nếu chưa có dialogue/cutscene mở lý do.

### 11.5 Cách thêm quest mới

1. Thêm quest data vào quest table trong `StoryRuntimeMVP`:
   ```lua
   {
       id = "Q_NEW_ID",
       title = "Tên quest",
       chapter = N,
       objectiveText = "Objective text tiếng Việt",
       targetType = "NPC" | "Location" | "Cleanup" | "Placement",
       targetId = "ObjectName",
       completeTrigger = "DialogueComplete" | "TrashCount" | "PlacementCount" | "EnterZone",
       nextQuestId = "Q_NEXT_ID"
   }
   ```
2. Wire target object: đảm bảo object có attributes đúng (`InteractId`, `Interactable`, etc.).
3. Test: Play mode, advance tới quest mới, verify marker + objective + completion.

### 11.6 Cách thêm dialogue mới

1. Thêm dialogue data vào dialogue table trong `StoryRuntimeMVP`:
   ```lua
   {
       id = "DialogueID",
       speaker = "NPC Name",
       lines = {
           {speaker = "NPC", text = "..."},
           {speaker = "Player", text = "..."},
       },
       choices = nil or { {text = "...", next = "..."}, ... },
       onComplete = { completeQuest = "...", startQuest = "..." }
   }
   ```
2. Link dialogue tới quest: quest trigger mở dialogue, dialogue complete triggers quest complete.

### 11.7 Cách thêm marker objective

1. Xác nhận target object path.
2. Trong quest data, set `targetId` tới object name.
3. `StoryClientMVP` tự tạo marker dựa trên current quest target.
4. Marker dùng tên hiển thị tiếng Việt.

### 11.8 Cách thêm cleanup runtime

1. Trong `StoryRuntimeMVP`, khi quest cleanup bắt đầu:
   - Xác định vị trí spawn gần ground height.
   - Tạo runtime trash parts/models.
   - Set attributes: `GreenAgainV5 = true`, `GreenAgainKind = "Trash"`, `Interactable = true`.
2. Khi player interact → ẩn/destroy → tăng cleanup count.
3. Khi count đạt threshold → quest complete.

### 11.9 Cách thêm placement action

1. Xác định placement zone (vị trí đặt thùng/biển).
2. Tạo runtime placement marker tại zone khi quest active.
3. Player interact → marker thay bằng placed object → placement count tăng.

### 11.10 Cách test Play mode

1. Click Play trong Roblox Studio.
2. Sau teleport, verify:
   - Quest tracker hiện đúng.
   - Marker hiện tại đúng vị trí.
   - Interact `E` hoạt động.
   - Dialogue mở đúng, advance đúng.
   - Quest complete → next quest start.
   - Sorting quest: tới điểm tập kết, interact một thùng rác, kéo từng item vào đúng thùng trong mini game.
3. Chạy toàn bộ route từ Q1_01 → PostEnding_FreeRoam.

### 11.11 Cách tránh duplicate UI/dialogue

- Chỉ dùng `StoryClientMVP` cho UI — KHÔNG thêm UI script mới.
- Xác nhận không còn `GreenAgainHUD_V5`, `GreenAgainObjectiveClient`, `MapWiringBootstrap`.
- Debounce dialogue: không mở lại dialogue vừa complete.

### 11.12 Cách kiểm tra console

1. Mở Output window trong Studio.
2. Tìm errors liên quan "GreenAgain", "Story", "Quest", "Dialogue".
3. Console noise từ imported assets (texture permission, asset script warnings) là KHÔNG liên quan.

### 11.13 Cách xử lý nếu object path thay đổi

1. Nếu object bị di chuyển/rename trong Studio, sửa path reference trong `StoryRuntimeMVP`.
2. Sửa `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md` trước, rồi sửa code.
3. KHÔNG đổi tên quest/object/script tự ý.

### 11.14 Checklist Build

#### Preflight

- [ ] Đọc document tổng hợp này.
- [ ] Mở Studio, xác nhận workspace mapping (Section 4).
- [ ] Xác nhận `StoryRuntimeMVP` và `StoryClientMVP` tồn tại.
- [ ] Xác nhận không còn old scripts/UI gây duplicate.

#### Runtime Changes

- [ ] Thêm quest data nếu cần.
- [ ] Thêm dialogue data nếu cần.
- [ ] Thêm runtime trash/placement spawning nếu cần.
- [ ] Wire target objects với đúng attributes.

#### Client UI Changes

- [ ] Nếu thêm UI mới, thêm vào `StoryClientMVP` — KHÔNG tạo script mới.
- [ ] Verify marker hiển thị đúng tên tiếng Việt.
- [ ] Verify prompt format đúng `[E] Action - Object`.

#### Map Wiring

- [ ] Xác nhận target objects tồn tại trong workspace.
- [ ] Xác nhận positions gần ground height.
- [ ] Xác nhận NPC ở đúng vị trí.
- [ ] Nếu dùng asset từ `Workspace.Trash`, clone sang `Workspace.GreenAgainV5_StoryRuntime` rồi mới set `Interactable=true`.
- [ ] Không bật interaction trực tiếp trên source templates trong `Workspace.Trash`.

#### Dialogue Validation

- [ ] Mỗi dialogue mở đúng lúc.
- [ ] Dialogue advance đúng (E/continue).
- [ ] Choices hoạt động.
- [ ] Dialogue complete → quest complete.
- [ ] Dialogue không lặp lại sau khi complete.

#### Playthrough Validation

- [ ] Fresh play từ Q1_01 → PostEnding_FreeRoam.
- [ ] Mỗi quest advance đúng.
- [ ] Marker luôn chỉ đúng target.
- [ ] Notebook book unlock đúng chapter và nút `Trước`/`Sau` xem lại được các trang đã mở.
- [ ] Ending chỉ chạy 1 lần.

#### Polish Pass

- [ ] Không có text hiện tên kỹ thuật cũ (PicnicArea, Dam, Scanner).
- [ ] Font/size đủ đọc trên mobile.
- [ ] Camera focus không kẹt.
- [ ] Player input luôn trả lại sau dialogue/cutscene.

---

## 12. CURRENT TECHNICAL DETAILS

**Nguồn chính:** `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`, `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`

### 12.1 Remote Events / Bindable Events

| Event | Hướng | Mục đích |
|---|---|---|
| `OnInteractRequested` | Client → Server | Player nhấn E trên object → server xử lý |
| `OnQuestStarted` | Server → Client | Thông báo quest mới bắt đầu |
| `OnQuestCompleted` | Server → Client | Thông báo quest hoàn thành |
| `OnObjectiveChanged` | Server → Client | Cập nhật objective text + marker target |
| `OnDialogueOpen` | Server → Client | Gửi dialogue data để client hiển thị panel |
| `OnDialogueClose` | Client → Server (hoặc Server → Client) | Dialogue kết thúc, unlock player |
| `OnFeedbackToast` | Server → Client | Hiện feedback toast ngắn |
| `OnNotebookEntry` | Server → Client | Hiện notebook entry toast |
| `OnEndText` | Server → Client | Hiện ending overlay text |

### 12.2 Attributes

| Attribute | Áp dụng cho | Giá trị | Mục đích |
|---|---|---|---|
| `InteractId` | Objects interactable | String (NPC name, object name) | ID để interaction router nhận diện |
| `ObjectName` | Objects | String | Tên hiển thị tiếng Việt |
| `Action` | Objects | String ("Talk", "Pickup", "Place", "Clear") | Loại action |
| `Interactable` | Objects | Boolean | Có đang interactable không |
| `GreenAgainV5` | Map objects | Boolean | Đánh dấu thuộc V5 system |
| `GreenAgainKind` | Objects | String ("NPC", "Trash", "Placement", "Location", "Drain") | Phân loại object |
| `NpcId` | NPC models | String | ID của NPC |
| `StoryLocation` | Location objects | String | ID location |
| `StoryQuestId` | Objects liên quan quest | String | Quest ID liên quan |
| `Collected` | Trash objects | Boolean | Đã nhặt chưa |
| `Placed` | Placement objects | Boolean | Đã đặt chưa |

### 12.3 Data Shape tham khảo

#### Quest Data

```lua
{
    id = "Q1_02_MeetBacXanh",
    title = "Gặp Bác Xanh",
    chapter = 1,
    objectiveText = "Nói chuyện với Bác Xanh",
    targetType = "NPC",
    targetId = "BacXanh",
    completeTrigger = "DialogueComplete",
    onStartDialogue = nil,
    onCompleteDialogue = "BacXanh_Ch1_Intro",
    notebookEntry = nil,
    nextQuestId = "Q1_03_CleanEntrance"
}
```

#### Dialogue Data

```lua
{
    id = "BacXanh_Ch1_Intro",
    speaker = "Bác Xanh",
    lines = {
        {speaker = "Bác Xanh", text = "Cháu mới tới Ven Sông phải không?"},
        {speaker = "Player", text = "Dạ. Cháu thấy quanh đây có nhiều rác quá."},
        -- ... more lines
    },
    choices = nil,
    onComplete = {
        completeQuest = "Q1_02_MeetBacXanh",
        startQuest = "Q1_03_CleanEntrance",
    }
}
```

---

## 13. TEST PLAN

**Nguồn chính:** `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md` (Section Test Results), `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md` (Section QA)

### 13.1 Fresh Playthrough Test

| # | Test Case | Expected Result | Trạng thái |
|---|---|---|---|
| 1 | Fresh play từ lobby → teleport → Q1_01 → ... → PostEnding_FreeRoam | Toàn bộ quest chain advance đúng, không stuck | ✅ Tested |
| 2 | Mỗi quest có đúng marker + objective text | Marker hiện đúng vị trí, text đúng tiếng Việt | ✅ Tested |
| 3 | Dialogue mở, advance, complete đúng | Dialogue hiện speaker, lines, choices đúng | ✅ Tested |
| 4 | Cleanup quests: nhặt đủ rác → quest complete | Count đúng, quest advance | ✅ Tested |
| 5 | Placement quests: đặt đủ items → quest complete | Count đúng, quest advance | ✅ Tested |
| 6 | Drain interaction: chỉ ở Ch5 | Drain không interactable trước Ch5 | ✅ Tested |
| 7 | Community gather: 3+ NPC reactions | Quest advance sau đủ reactions | ✅ Tested |
| 8 | Ending chỉ chạy 1 lần | Ending overlay hiện 1 lần, không repeat | ✅ Tested |
| 9 | PostEnding: free roam, không marker | Player tự do, no marker, no quest tracker | ✅ Tested |

### 13.2 Marker Tests

| # | Test Case | Expected Result | Trạng thái |
|---|---|---|---|
| 10 | Marker ở lobby/khu nối | KHÔNG hiện | ✅ Tested |
| 11 | Marker hiện khi teleport tới main map | Marker hiện đúng | ✅ Tested |
| 12 | Marker chỉ 1 active tại một thời điểm | Không có 2 markers | ✅ Tested |
| 13 | Marker có tên, không có distance | Tên hiện, distance KHÔNG hiện | ✅ Tested |

### 13.3 Height/Position Tests

| # | Test Case | Expected Result | Trạng thái |
|---|---|---|---|
| 14 | Q1 marker không ở trên cao (pivot NhaVanHoa) | Marker ở gần mặt đất | ✅ Tested |
| 15 | Q1 cleanup trash spawn gần ground | Trash ở ~Y=52.2, không floating | ✅ Tested |

### 13.4 UI Tests

| # | Test Case | Expected Result | Trạng thái |
|---|---|---|---|
| 16 | Old HUD không còn | `GreenAgainHUD_V5` không spawn | ✅ Tested |
| 17 | Old connection text không hiện | "Đang nối map..." không hiện | ✅ Tested |
| 18 | Stamina UI không hiện | Stamina bar không có | ✅ Tested |
| 19 | Sprint Shift vẫn chạy | Giữ Shift tăng speed | ✅ Tested |

### 13.5 Dialogue Edge Cases

| # | Test Case | Expected Result | Trạng thái |
|---|---|---|---|
| 20 | Dialogue không lặp sau complete | Debounce hoạt động | `Đề xuất bổ sung` — Cần test kỹ hơn |
| 21 | Spam E không skip dialogue | Dialogue advance từng line, không skip hết | `Đề xuất bổ sung` — Cần test |
| 22 | Camera/control trả lại sau dialogue | Player input hoạt động bình thường | ✅ Tested |

### 13.6 Regression Tests

| # | Test Case | Expected Result | Trạng thái |
|---|---|---|---|
| 23 | Không có text hiện "PicnicArea", "Dam", "Scanner" | Tất cả tên hiển thị đúng tiếng Việt V5 | `Đề xuất bổ sung` — Cần verify toàn bộ |
| 24 | Rejoin/respawn không reset story sai | Story state consistent | `Chưa rõ / cần xác nhận` — MVP chưa có save/load |
| 25 | NPC dialogue state đổi sau quest complete | NPC nói line "after" thay vì "before" | `Đề xuất bổ sung` — Cần verify |

### 13.7 Playtest Questions (Qualitative)

- Player có biết vì sao mình đang dọn rác không?
- Player có biết đi đâu tiếp không?
- Mỗi NPC có cảm giác là một người thật không?
- Chapter 5 có cảm giác là cao trào, không phải cleanup grind?
- Ending có cảm giác earned (xứng đáng)?

---

## 14. GAPS / CHƯA RÕ / ĐỀ XUẤT BỔ SUNG

### 14.1 Docs chưa nói rõ

| Mục | Chi tiết | Đề xuất |
|---|---|---|
| **Bác Xanh movement giữa chapters** | Bác Xanh xuất hiện ở nhiều nơi (NVH, bờ sông, cống) nhưng docs không nói rõ Bác teleport hay walk | `Đề xuất bổ sung`: Bác Xanh teleport/đứng sẵn tại location cần thiết khi quest trigger |
| **Q5_03 Gather — NPC vị trí** | Player quay lại gặp NPC ở đâu? NPC ở vị trí ban đầu hay di chuyển? | `Đề xuất bổ sung`: NPC ở vị trí ban đầu, player quay lại từng nơi |
| **Ending NPC positioning** | NPC xuất hiện ở NVH ending — teleport hay walk? Vị trí chính xác? | `Đề xuất bổ sung`: Teleport về NVH khi ending trigger. Đứng bán nguyệt trước sân NVH |
| **Anh Hòa trong MVP** | Anh Hòa có dialogue ở cống nhưng chưa rõ có NPC model không | `Chưa rõ / cần xác nhận`: Nếu không có model, dùng Bác Xanh hoặc Chị Lan nói line Anh Hòa |
| **Mobile input** | Docs không nói rõ mobile interaction. Hiện chỉ có E key | `Đề xuất bổ sung`: Thêm on-screen button cho mobile |
| **NPC idle animations** | Docs không specify animation cụ thể | `Đề xuất bổ sung`: Dùng R15 default idle, hoặc custom idle nếu có |
| **Before/After dialogue cho NPC chính** | NPC chính có Before/After line nhưng chưa rõ system trigger | `Đề xuất bổ sung`: Dựa trên quest state — nếu NPC chưa phải target, show Before line. Sau quest xong, show After line |

### 14.2 Implementation hiện tại còn MVP

| Mục | Trạng thái MVP | Cần làm tiếp |
|---|---|---|
| **Tách module** | Tất cả gộp trong 2 script | Tách thành QuestManager, DialogueService, StoryStateService, etc. theo implementation plan |
| **Save/load** | Không có — story reset mỗi session | Thêm DataStore save cho story state |
| **NPC phụ** | Chưa implement | Thêm NPC phụ theo implementation plan M10 |
| **Camera cinematic** | Chỉ có dialogue lock, chưa có cinematic camera | Thêm CutsceneService với camera steps |
| **Cutscene system** | Dialogue-driven, chưa có fade/letterbox/camera focus | Thêm cutscene step types: Fade, Letterbox, CameraFocus, CameraLookAt, Wait |
| **NPC phụ ending attendance** | Chưa có | NPC phụ đã gặp có thể xuất hiện tại ending |
| **Visual change sau cleanup** | `Đề xuất bổ sung` | Thêm visual change: cây mọc, đường sáng hơn, sau khi dọn xong |
| **Sorting interaction** | `Chưa rõ / cần xác nhận` | Hiện Q1_04 interact với Chị Lan. Cần xác nhận có drag-drop phân loại hay chỉ talk |

### 14.3 Polish nên làm tiếp

| Mục | Mức ưu tiên | Chi tiết |
|---|---|---|
| **Ambient NPC lines** | Trung bình | NPC phụ nói ngẫu nhiên khi player đi qua |
| **Particle effects** | Thấp | Bụi, lá bay, bọt nước ở cống, ánh sáng NVH ending |
| **Sound design** | Trung bình | Ambient sounds: chim, gió, nước chảy. SFX: nhặt rác, đặt thùng |
| **Camera cinematic polish** | Trung bình | Camera pan, zoom, focus cho cutscene moments |
| **Art polish runtime trash** | Thấp | Thay thế basic parts bằng mesh models cho rác |
| **Art polish placement** | Thấp | Thùng rác, biển nhắc có model chi tiết |
| **NPC walking animation** | Thấp | Bé Na chạy nhặt bóng, Ông Sáu đi dọc bờ |
| **Post-ending visual** | Trung bình | Map sáng hơn / sạch hơn ở post-ending |
| **Notebook persistence** | Thấp | UI cuốn nhật ký đã mở lại được trong session; cần DataStore nếu muốn giữ trang đã unlock giữa các lần vào game |

### 14.4 Câu hỏi cần user xác nhận

1. **Q5_03 Gather flow:** Player quay lại gặp từng NPC ở vị trí ban đầu, hay NPC tụ lại ở một nơi?
2. **Anh Hòa:** Có NPC model cho Anh Hòa không, hay gộp line vào Bác Xanh/Chị Lan?
3. **Mobile:** Có cần support mobile ngay không? Nếu có, cần thêm on-screen buttons.
4. **Save/load:** Có cần save story state giữa sessions không?
5. **Sorting interaction Q1_04:** Chỉ talk Chị Lan, hay có mini-game phân loại?
6. **NPC movement:** NPC có cần walk animation, hay chỉ đứng idle?
7. **Visual change sau cleanup:** Map có cần đổi visual (sáng/sạch hơn) sau mỗi chapter?
8. **Post-ending content:** Post-ending có thêm mini-quest giữ Ven Sông xanh không, hay chỉ free roam?

---

> **Document này được tạo bằng cách tổng hợp từ 8 file nguồn V5 + README trong `docs/`. Mọi phần đánh dấu `Đề xuất bổ sung` hoặc `Chưa rõ / cần xác nhận` là do thông tin chưa có trong docs gốc.**
