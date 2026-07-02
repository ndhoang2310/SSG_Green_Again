# GREEN AGAIN v4 — IMPLEMENTATION BLUEPRINT

> Mục đích: tài liệu này là bản tổng hợp để AI agent/dev đọc vào là biết chính xác phải làm gì trong Roblox Studio, không tự diễn giải sai GDD.
> Nguồn bắt buộc bám sát: `GDD_GreenAgain_v4.md`, `GDD_GreenAgain_NPC_Dialogue_v4.md`, `GDD_GreenAgain_Map_v4.md`, `GDD_GreenAgain_Flow_Audit_v4.md`, `GDD_GreenAgain_Friction_Audit_v4.md`, `context.md`.
> Trạng thái ghi nhận: sau audit hiện tại trong Roblox place `thử nghiệm`, tháng 6/2026.

---

## 0. Luật Bất Biến Cho Agent

### 0.1 Không được tự ý đổi thiết kế

- Không tự viết lại thoại. Dialogue phải dùng nguyên văn từ `GDD_GreenAgain_NPC_Dialogue_v4.md`.
- Không rút gọn chapter flow nếu không được yêu cầu.
- Không thêm fast travel, achievement popup, daily reward, quiz, leaderboard, shop, combat, timer fail state.
- Không tạo spawn mới. Spawn gốc đang ở `Workspace.=== SYSTEMS ===.SpawnLocation`, vị trí khoảng `(34, 16, -95)`.
- Không build lại Nhà văn hóa. Nhà văn hóa đã có: `Workspace.=== BUILDINGS ===.NhaVanHoa_ThonNoiChuan`.
- Không tạo thùng rác duplicate nếu RC đã có thùng. Dùng thùng hiện có trong `DiemTapKetRacThai_ThonVenSong`.
- Không thay cổng teleport/lobby nếu chưa có yêu cầu. Place hiện tại có 2 khu: lobby và làng.
- Không phá scripts cũ không liên quan nếu không gây lỗi trực tiếp. Nhưng nếu script cũ phá visual/gameplay GDD thì phải note rõ trước khi sửa.

### 0.2 Nền tảng và scope

- Đây là game Roblox, không phải Unity.
- Không dùng lại BMAD/Unity docs cũ.
- Tài liệu core hiện tại nằm trong `GA/docs/`.
- Asset Roblox place chính: `GA/assets/fullproject.rbxl`.

### 0.3 Thứ tự ưu tiên khi có xung đột

1. Gameplay flow trong `GDD_GreenAgain_v4.md`.
2. Dialogue nguyên văn trong `GDD_GreenAgain_NPC_Dialogue_v4.md`.
3. Map intent trong `GDD_GreenAgain_Map_v4.md`.
4. Map thực tế đang có trong Roblox Studio.
5. Tối ưu/cải thiện của agent.

Nếu map thực tế khác map doc, agent phải bám gameplay/doc nhưng đặt object theo map thực tế. Không được tự di chuyển công trình lớn nếu chưa hỏi.

---

## 1. Tầm Nhìn Game Cần Đạt

### 1.1 Concept

Người chơi là tình nguyện viên môi trường đến thị trấn Ven Sông đang ô nhiễm. Người chơi phục hồi thị trấn bằng cách dọn rác, dùng Eco Scanner tìm nguồn ô nhiễm, phân loại rác, đặt hạ tầng, thông đập 3 cống, cứu động vật, thuyết phục người dân và trồng cây.

### 1.2 Thông điệp cốt lõi

Dọn rác chỉ là bước đầu. Muốn thị trấn xanh bền vững cần 3 thứ cùng lúc:

- Hành động cá nhân.
- Hạ tầng đúng chỗ.
- Cộng đồng thay đổi thói quen.

### 1.3 Cảm xúc đích

Earned Belonging — người chơi từ người lạ trở thành một phần của thị trấn.

Điều này phải thể hiện bằng gameplay và visual:

- Bắt đầu từ ngoài làng/lobby, đi vào làng.
- Gặp Bác Xanh ở Nhà văn hóa.
- NPC dần nhớ và phản ứng với việc người chơi làm.
- Ending ở Nhà văn hóa sáng đèn, NPC tụ họp.

---

## 2. Map Thực Tế Hiện Tại Và Khác Biệt So Với Doc

### 2.1 Doc gốc nói gì

GDD v4 mô tả một thị trấn duy nhất, không loading screen, với các khu:

- Spawn góc dưới trái.
- Nhà văn hóa ở SW, Bác Xanh ở trước cửa/ghế đá.
- Trung tâm Tái chế cạnh Nhà văn hóa.
- Khu dân cư NW.
- Nhà Cô Tư N-center.
- Công viên NE.
- Bờ sông NE, Ông Sáu cạnh mỏm đá.
- Đập nước phía Nam có 3 cống xả.
- Sông uốn lượn Bắc đến Đông Nam.

### 2.2 Map thực tế trong Roblox hiện tại

Place thực tế có 2 khu:

- Map 1: lobby/sảnh chờ, player spawn tại đây.
- Map 2: làng/gameplay, đi qua portal để tới.

Object quan trọng đã xác nhận:

- Spawn gốc: `Workspace.=== SYSTEMS ===.SpawnLocation`, khoảng `(34, 16, -95)`.
- Portal vào làng: `Workspace.=== SYSTEMS ===.Portals.Portal1`, khoảng `(39.427, 18.879, -280.607)`, attribute `Destination="Portal1Destination"`.
- Destination vào làng: `Workspace.=== SYSTEMS ===.Destinations.Portal1Destination`, khoảng `(455.475, 48.703, -3514.401)`.
- Nhà văn hóa: `Workspace.=== BUILDINGS ===.NhaVanHoa_ThonNoiChuan`, pivot khoảng `(281.25, 67.29, -3566.854)`.
- Bác Xanh: `Workspace.=== NPCS ===.Bác Xanh`, pivot khoảng `(281, 49, -3532)`.
- Trung tâm Tái chế: `Workspace.=== BUILDINGS ===.DiemTapKetRacThai_ThonVenSong`, pivot khoảng `(93.57, 58.06, -3533.43)`.
- Tạp hóa Cô Tư: `Workspace.=== BUILDINGS ===.TapHoaCoTu_HouseOnly_Rural`, pivot khoảng `(78.78, 49.06, -3187.65)`.
- Cô Tư: `Workspace.=== NPCS ===.Cô Tư`, khoảng `(79, 49, -3168)`.
- Anh Tùng: `Workspace.=== NPCS ===.Anh Tùng`, khoảng `(450, 52, -3300)`.
- Bé Na: `Workspace.=== NPCS ===.Bé Na`, khoảng `(480, 52, -3320)`.
- Ông Sáu: `Workspace.=== NPCS ===.Ông Sáu`, khoảng `(650, 48, -3150)`.
- Chị Lan: `Workspace.=== NPCS ===.Chị Lan`, khoảng `(60, 58, -3550)`.

### 2.3 Quyết định xử lý khác biệt map

- Giữ 2-map flow thực tế: lobby -> portal -> làng.
- Không biến place về một-map nếu chưa có yêu cầu.
- Chapter 1 gameplay bắt đầu sau khi player qua portal vào làng.
- Rác đầu làng cần đặt gần vùng destination hoặc đường từ `Portal1Destination` về Nhà văn hóa.
- Không tạo spawn trong làng. Nếu cần điểm đứng sau chapter break, teleport player tạm thời đến trước Nhà văn hóa bằng script, không tạo `SpawnLocation` mới.
- RC thực tế đang xa hơn/khác layout doc, nhưng phải dùng RC hiện có.
- Cây đa đã thay cối xay gió. Nếu doc nhắc cối xay gió, trong implementation dùng cây đa/landmark hiện có, không tự đổi lại.

### 2.4 Việc người dùng cần làm thủ công về map

- Xác nhận chính thức đường đi Chapter 1 từ `Portal1Destination` đến Nhà văn hóa: tuyến nào là “đường vào làng”.
- Nếu muốn đúng doc một-map hoàn toàn, người dùng phải quyết định bỏ lobby/portal hoặc giữ 2-map flow.
- Xác nhận vị trí thực tế của đập nước. Hiện agent chỉ thấy hotspot `Dam_C1/C2/C3`, chưa thấy model đập/cống tương tác rõ.
- Xác nhận vị trí sông thật. Hiện search chỉ thấy hotspot River và vài sound/bridge assets, chưa thấy river system rõ theo doc.
- Nếu muốn ending Nhà văn hóa sáng đèn đẹp, người dùng nên chọn/duyệt vị trí NPC tụ họp, đèn lồng/đèn dầu, khói bếp, chim/cá/sóc visual.

---

## 3. Hệ Thống Gameplay Bắt Buộc

### 3.1 Interaction system

Yêu cầu đúng:

- Player thấy prompt `[E]` khi gần object tương tác.
- Bấm E phải tương tác thật.
- ClickDetector có thể giữ lại làm fallback, nhưng không được là cách chính nếu UI nói `[E]`.
- Server phải validate khoảng cách và object target.

Object interactable cần có attribute chuẩn:

- `Interactable=true`.
- `InteractId` unique.
- `Action`, ví dụ `Nhặt`, `Nói chuyện`, `Phân loại`, `Thông cống`, `Cứu`, `Đặt thùng`, `Đặt biển`, `Trồng cây`.
- `ObjectName` hiển thị UI.

Không được để một object vừa là rác vừa là thùng phân loại, trừ khi có logic ưu tiên rõ.

### 3.2 Eco Scanner

Yêu cầu đúng:

- Unlock cuối Chapter 1 sau dialogue Bác Xanh.
- Phím Q toggle.
- Nếu bấm Q trước unlock, hiện toast: `Chưa có Máy Quét Sinh Thái — gặp Bác Xanh trước.`
- Scanner range: 50 studs.
- Marker theo pollution:
  - Xanh: PL < 20, đã xử lý.
  - Vàng: PL < 40, ô nhiễm nhẹ.
  - Cam: PL 40-70, ô nhiễm trung bình.
  - Đỏ: PL > 70, ưu tiên xử lý.
- Hotspot phải unlock theo chapter, không hiện toàn bộ ngay từ đầu.

Hotspot bắt buộc:

- `PicnicArea`, PL 55, mở C2A.
- `ResidentialSt`, PL 60, mở C2C.
- `Dam_C1`, PL 80, phát hiện C2C, thông C3.
- `Dam_C2`, PL 80, mở C3.
- `Dam_C3`, PL 80, mở C3.
- `RiverNE`, PL 45, mở C2C/C3.
- `RiverBend`, PL 40, mở C3.

### 3.3 Inventory và sorting

Yêu cầu đúng:

- C1 và C2A: rác nhặt auto-disappear, chưa dùng inventory.
- Từ C2B: inventory 5 ô.
- C4: inventory mở rộng tạm thời 8 ô để gom rác cứu hộ, sort một lần.
- Có UI inventory bar.
- Khi túi gần đầy: warning.
- Khi túi đầy: không cho nhặt thêm, hướng người chơi về RC.

Sorting bins:

- Hữu cơ: xanh lá, `BinType=Organic`.
- Tái chế: xanh dương, `BinType=Recycle`.
- Vô cơ: vàng, `BinType=Inorganic`.
- Độc hại: đỏ, `BinType=Hazardous`.

Trash rules:

- `Organic` -> `Organic`.
- `Plastic` -> `Recycle`.
- `Paper` -> `Recycle`.
- `Metal` -> `Recycle`.
- `Hazardous` -> `Hazardous`.
- Nếu dùng loại `Rest`/`Inorganic`, phải map đúng sang thùng vô cơ và không lẫn với `TrashType=rest` trên bin.

Sorting tutorial C2B bắt buộc:

- 3 món mẫu có highlight đúng thùng 1 giây.
- 2 món bán hướng dẫn, highlight trễ 2 giây.
- Sau đó spawn 2-3 rác gần/trong RC để tự nhặt và sort, không bắt quay lại công viên ngay.
- Lần đầu mỗi loại rác mới có auto-highlight 1 giây.
- Từ lần 2 tự chọn.

### 3.4 Đập nước 3 cống

Yêu cầu đúng:

- 3 cống là 3 object riêng, không chỉ là marker.
- Mỗi cống có `CulvertId=1/2/3`.
- Mỗi cống có state clogged/cleared.
- Điều kiện thông cống:
  1. Nhặt sạch rác trong bán kính 15 studs quanh cống đó.
  2. Giữ E 3 giây.
  3. Cống chuyển visual sang thông.
  4. PL khu đập giảm 25.
  5. ES +10.
- Thông cả 3 cống: nước chảy sạch qua, disable pollution spread từ đập.

Pollution spread:

- Stage 1: một cống tắc, PL > 75, warning nhẹ.
- Stage 2: hai cống tắc sau 3 phút, Riverside PL +10.
- Stage 3: ba cống tắc sau 5 phút, cá khó cứu hơn/urgent warning.
- Không fail state. Người chơi luôn sửa được.

### 3.5 Animal rescue

Yêu cầu đúng:

- C4 mở cùng lúc 3 animal signals.
- Chim ở công viên gần cây lớn.
- Cá dưới chân đập.
- Sóc ở khu dân cư cạnh bụi rác.

Chim:

- Vấn đề: mắc túi nhựa.
- Điều kiện: nhặt sạch rác nhựa trong 15 studs.
- Sau đó E để cứu, chim bay lên.

Cá:

- Vấn đề: nước bẩn, cá yếu.
- Điều kiện: ít nhất 2/3 cống đã thông và PL đập < 40.
- Nếu chưa đủ, prompt nói rõ phải thông thêm cống.
- Sau đó E để cứu, cá bơi lại.

Sóc:

- Vấn đề: rác độc hại quanh bụi cây.
- Điều kiện: dùng scanner tìm rác độc hại ẩn, nhặt 4-5 món, phân loại đúng.
- Sau đó E để cứu, sóc chạy lên cây.

### 3.6 Placement system

Yêu cầu đúng:

- C3 nhận 3 thùng rác + 2 biển báo từ Bác Xanh.
- C5 trồng 3-7 cây, mỗi cây ES +5.
- Có feedback vị trí:
  - Good Location: +5 ES.
  - Low Impact: +1 ES.
  - Invalid: không đặt được.
- Không cho đặt vô hạn.
- Không cho đặt sai chapter.
- Nhà Cô Tư optional trong C3: có thể bỏ qua và quay lại sau.

### 3.7 Community dialogue

Yêu cầu đúng:

- C5 mới thuyết phục 3 NPC chính.
- Có 3 lựa chọn A/B/C.
- Lựa chọn B là tốt nhất, CA +10.
- Lựa chọn C là ép/ok, CA +3.
- Lựa chọn A không thay đổi, CA +0.
- UI phải cho người chơi chọn thật, không auto chọn B khi bấm E.
- Sau khi thuyết phục, NPC state đổi từ `Unaware` sang `Aware`.
- Nếu có hạ tầng gần đó, NPC có thể lên `Considerate`.

### 3.8 Ending

Yêu cầu đúng:

- Ending diễn ra tại Nhà văn hóa.
- Nhà văn hóa sáng đèn, có ánh vàng, NPC tụ họp.
- Bác Xanh đứng ở cửa, không còn ngồi ghế đá.
- Camera pan qua các điểm phục hồi.
- Ending A/B/C theo điều kiện:
  - A: ES >= 90, PL < 20, CA >= 70, cứu 3/3, trồng >= 3 cây.
  - B: ES 65-89, PL 20-45, CA 40-69, cứu 2-3, trồng 1-2 cây.
  - C: ES < 65 hoặc PL > 45 hoặc CA < 40 hoặc cứu 0-1 hoặc trồng 0.

---

## 4. Chapter 1 — Khởi Đầu

### 4.1 Mục tiêu chapter

- Dạy di chuyển và nhặt rác.
- Tạo cảm giác người lạ bước vào làng.
- Gặp Bác Xanh.
- Nhận Eco Scanner.
- Unlock UI 3 chỉ số.

### 4.2 Flow bắt buộc

1. Player spawn ở lobby.
2. Player đi qua Portal1 vào làng.
3. Player xuất hiện tại `Portal1Destination`.
4. Text mờ/toast/cinematic: `Thị trấn Ven Sông — một buổi chiều tháng Sáu...`.
5. Camera/visual hướng player về đường đất, Nhà văn hóa phía xa, sông đục nếu thấy được.
6. Rác đầu tiên nằm trước mặt hoặc trên tuyến vào làng, cách 5-8 studs.
7. Player nhặt 10 món rác tutorial dọc đường vào Nhà văn hóa.
8. Món rác đầu tiên có feedback: `Tình nguyện viên — đã đến lúc dọn dẹp.`
9. Sau khi đủ rác, quest chuyển sang gặp Bác Xanh.
10. Player nói chuyện với Bác Xanh ở Nhà văn hóa.
11. Bác Xanh nói full dialogue C1 nguyên văn.
12. Scanner unlock, toast/icon Q hiện.
13. Chapter 1 hoàn thành, chuyển Chapter 2.

### 4.3 Dialogue bắt buộc

Dùng nguyên văn `Bác Xanh — Chapter 1: Lần đầu gặp gỡ` từ `GDD_GreenAgain_NPC_Dialogue_v4.md`.

Không được dùng câu tự viết kiểu ngắn gọn nếu câu đó đã có trong doc.

### 4.4 Object cần có

- 10 rác C1 trên tuyến Portal1Destination -> Nhà văn hóa.
- Bác Xanh interactable.
- Nhà văn hóa làm landmark.
- Optional: biển quảng cáo cũ đổ bên đường.

### 4.5 Agent cần implement

- Sửa E interaction để nhặt rác và nói chuyện chạy thật.
- Đảm bảo rác C1 không dùng inventory.
- Khi đủ 10 rác mới cho Bác Xanh trao scanner.
- Gating: nếu nói chuyện Bác Xanh trước khi đủ rác, Bác Xanh nhắc dọn rác trước.
- Scanner không hoạt động trước khi unlock.

### 4.6 Task cho người dùng

- Xác nhận tuyến đường từ Portal1Destination về Nhà văn hóa là đường nào.
- Nếu 10 rác hiện đặt sai tuyến hoặc khó thấy, người dùng cần chỉ vị trí mong muốn hoặc duyệt cho agent dời rác.
- Duyệt style của opening hook: toast đơn giản hay cinematic/fade/camera pan.

### 4.7 Acceptance checklist

- Player vào làng thấy rác đầu tiên trong 5-8 studs.
- Bấm E nhặt rác được.
- Quest tracker tăng 0/10 đến 10/10.
- Bác Xanh không trao scanner trước khi đủ 10 rác.
- Sau full dialogue, Q bật scanner được.
- Không có spawn mới xuất hiện trong làng.

---

## 5. Chapter 2 — Tìm Nguồn Ô Nhiễm

Chapter 2 chia thành 3 phase. Không được gộp sai.

### 5.1 Phase 2A — Làm quen Scanner

#### Mục tiêu

- Player dùng Q lần đầu.
- Tìm `PicnicArea` ở công viên.
- Hiểu màu marker scanner.
- Nhặt 3-4 rác trong hotspot, vẫn auto-disappear.

#### Flow bắt buộc

1. Bác Xanh bảo player đi về công viên.
2. Player đi từ Nhà văn hóa đến công viên.
3. Khi bật scanner trong range, thấy marker cam `PicnicArea`, PL 55.
4. UI tutorial hiện: `🟡 Vàng = nhẹ | 🟠 Cam = trung bình | 🔴 Đỏ = nghiêm trọng | ✅ Xanh = đã sạch`.
5. Player nhặt 3-4 món rác trong hotspot.
6. Bác Xanh qua UI nói: `Tốt lắm! Cháu thấy chưa — có những chỗ bẩn hơn mắt thường thấy. Máy quét không nói dối đâu. Màu càng đậm, vấn đề càng nặng.`

#### Agent cần implement

- Hotspot `PicnicArea` chỉ hiện từ C2A.
- Rác C2A ở công viên cần spawn/đặt sẵn.
- Progress quest bằng pickup trong hotspot.
- Scanner marker không hiện toàn map ngay.

#### Task cho người dùng

- Xác nhận khu công viên thực tế quanh Anh Tùng/Bé Na có đủ visual để player nhận ra.
- Nếu cần, người dùng đặt/duyệt thêm landmark cây đa/cây lớn/thảm picnic.

#### Acceptance checklist

- Q sau unlock bật overlay và marker.
- Marker cam hiện ở công viên, không phải toàn bộ hotspot cùng lúc.
- Nhặt đủ rác C2A tự chuyển sang phase sorting.

### 5.2 Phase 2B — Học phân loại

#### Mục tiêu

- Unlock inventory 5 ô.
- Dạy 4 loại thùng.
- Giảm anxiety bằng 3 mẫu + 2 bán hướng dẫn.

#### Flow bắt buộc

1. Bác Xanh/Chị Lan dẫn player đến RC.
2. Inventory 5 ô bật.
3. Bác Xanh nói intro sorting.
4. Mẫu 1: hữu cơ, highlight thùng Organic 1 giây.
5. Mẫu 2: tái chế, highlight thùng Recycle 1 giây.
6. Mẫu 3: vô cơ, highlight thùng Inorganic 1 giây.
7. Bác Xanh đưa thêm 2 món bán hướng dẫn.
8. Mỗi món bán hướng dẫn highlight trễ 2 giây.
9. Sau 5 món: Bác Xanh nói `Giỏi lắm! ... Giờ cháu thử tự làm nhé...`.
10. Spawn 2-3 rác gần/trong RC.
11. Player tự nhặt và sort.

#### Agent cần implement

- Quest riêng cho sorting tutorial phải progress khi sort đúng/sai theo tutorial step.
- Không dùng `Q03_SortTrash` hoặc `Q04_PlaceBins` vì các quest ID đó không tồn tại.
- Không để player kẹt ở Q04.
- Remove `TrashType` khỏi bin body hoặc đổi logic ưu tiên `BinType`.
- UI inventory phải hiển thị số ô.
- Sorting feedback đúng/sai rõ ràng.

#### Task cho người dùng

- Xác nhận tên thùng trong RC hiện tại tương ứng:
  - `ThungRac_Organic_Body` = hữu cơ.
  - `ThungRac_Recycle_Body` = tái chế.
  - `ThungRac_Rest_Body` = vô cơ.
  - `ThungRac_Hazard_Body` = độc hại.
- Nếu muốn dùng drop zone thay vì body thùng, người dùng cần duyệt chính xác part nào là vùng tương tác.

#### Acceptance checklist

- Player sort 5 món tutorial xong không bị kẹt.
- Sai không fail, chỉ feedback nhẹ.
- Sort đúng tăng ES.
- Inventory giảm khi sort.
- Thùng không biến mất khi click/E.

### 5.3 Phase 2C — Đối mặt thực tế

#### Mục tiêu

- Mở marker Residential và Dam C1.
- Cho player thấy rác quay lại nếu không xử lý nguyên nhân.
- Mở dynamic trash spawn.

#### Flow bắt buộc

1. Scanner cập nhật thêm marker `ResidentialSt` cam và `Dam_C1` đỏ.
2. Bác Xanh dẫn/nhắc player đến Đập nước.
3. Bác Xanh nói nguyên văn về đập 3 cống.
4. Player nhặt rác khu dân cư.
5. Nếu túi đầy, về RC sort.
6. Player quay lại công viên thấy rác đã quay lại.
7. Bác Xanh nói câu `Cháu thấy không? Rác đã quay lại...`.
8. Dynamic spawn active toàn bản đồ.
9. Chapter break cuối C2 tại Nhà văn hóa.

#### Agent cần implement

- Dynamic spawn theo zone pollution, không spawn bừa ở 2 tọa độ hard-coded không kiểm soát.
- Rác quay lại phải là scripted event, không chỉ random spawn.
- Chapter break C2 phải fade 2 giây, text `Ngày hôm sau...`, đưa player đứng trước Nhà văn hóa.

#### Task cho người dùng

- Xác nhận vị trí đập thật và đường đi từ RC đến đập.
- Nếu chưa có model đập/cống, người dùng cần cung cấp/duyệt asset hoặc cho phép agent tạo primitive cống.

#### Acceptance checklist

- C2 kết thúc bằng chapter break, không nhảy thẳng sang C3 lặng lẽ.
- Sau break, player đứng trước Nhà văn hóa.
- Bác Xanh nói return recap đầu C3.

---

## 6. Chapter 3 — Ngăn Rác Quay Lại

### 6.1 Mục tiêu chapter

- Dạy prevention, không chỉ cleanup.
- Đặt thùng rác và biển báo.
- Thông cống 1.
- Giải thích nhân quả: thùng rác + biển báo + cống.

### 6.2 Flow bắt buộc

1. Bác Xanh tại Nhà văn hóa đưa 3 thùng rác + 2 biển báo.
2. Tooltip: `Túi còn 5 ô. Có thể bỏ qua Nhà cô Tư nếu muốn — quay lại sau.`
3. Khu dân cư: đặt thùng rác + nhặt rác.
4. Nhà Cô Tư optional: đặt biển báo gần tiệm.
5. Công viên: đặt thùng rác + nhặt rác.
6. Bờ sông NE: đặt biển báo gần Ông Sáu.
7. Đập nước: nhặt rác quanh Cống 1, giữ E 3 giây để thông.
8. RC: sort toàn bộ inventory.
9. Scanner cập nhật Picnic Area và Dam C1 sang xanh nếu PL đủ thấp.
10. Bác Xanh nói `Đó mới là xử lý đúng cách...`.
11. Unlock Cống 2 và Cống 3.

### 6.3 Agent cần implement

- Quest C3 riêng cho placement + cống, không để C3 thành animal rescue.
- Item inventory cho placement: số thùng/biển hữu hạn.
- Placement zones gated theo chapter.
- Good/Low/Invalid feedback.
- Cống 1 object thật với `CulvertId=1`.
- Hold E 3 giây.
- Clear cống gọi `GameState:ClearCulvert(1)` và update UI/visual.

### 6.4 Task cho người dùng

- Xác nhận placement zones hiện tại đúng vị trí không:
  - `BinZone_1` khoảng `(160, 56, -3180)`.
  - `BinZone_2` khoảng `(220, 56, -3180)`.
  - `SignZone_1` khoảng `(350, 50, -3120)`.
  - `SignZone_2` khoảng `(400, 50, -3120)`.
  - `SignZone_3` khoảng `(450, 50, -3120)`.
- Xác nhận những zone này đại diện cho khu nào. Hiện tên zone generic, agent không biết zone nào là khu dân cư/công viên/bờ sông.
- Nếu muốn item đẹp, người dùng cần cung cấp/duyệt model thùng/biển thay vì primitive part.

### 6.5 Acceptance checklist

- Player không thể đặt cây ở C3.
- Player không thể đặt thùng/biển trước C3.
- Đặt đúng vị trí có feedback xanh.
- Đập C1 thông được bằng E hold.
- Cống 2/3 chỉ unlock sau C3.

---

## 7. Chapter 4 — Cứu Sinh Vật

### 7.1 Mục tiêu chapter

- Cho thấy ô nhiễm ảnh hưởng tới sinh vật.
- Dùng environmental gating.
- C4 không được thành loop sort lặp mệt. Phải dùng inventory 8 ô tạm thời và sort một lần.

### 7.2 Flow bắt buộc

1. Bắt đầu tại Nhà văn hóa.
2. Scanner hiện tín hiệu chim/cá/sóc.
3. Bác Xanh nói nguyên văn phát hiện động vật.
4. Player chọn thứ tự cứu 3 con, tất cả mở cùng lúc.
5. Công viên: cứu chim bằng cách nhặt rác nhựa trong 15 studs, E cứu.
6. Đập: cứu cá nếu 2/3 cống đã thông và PL đập < 40. Nếu chưa, thông thêm cống ngay tại đập.
7. Khu dân cư: cứu sóc bằng cách dùng scanner tìm rác độc hại, nhặt và phân loại đúng.
8. Sau khi gom rác cứu hộ, về RC sort một lần.
9. Sau mỗi con, Bác Xanh có phản ứng theo số con đã cứu.
10. Sau 3 con, ES +24, animals appear naturally, visual map thay đổi.
11. Chapter break cuối C4 tại Nhà văn hóa.

### 7.3 Agent cần implement

- Animal objects có `AnimalId=Bird/Fish/Squirrel`.
- Rescue zones có bán kính và trash requirement.
- Inventory max chuyển 5 -> 8 khi C4 bắt đầu, sau sort cứu hộ trở lại 5.
- Fish gate check `GetClearedCulvertCount() >= 2` và `ZonePollution.Dam < 40`.
- Nếu fish chưa đủ điều kiện, prompt phải dùng system dialogue trong doc.
- Rescue progress không được xảy ra nếu chưa dọn/sort đủ.

### 7.4 Task cho người dùng

- Cần cung cấp hoặc duyệt model placeholder cho chim, cá, sóc.
- Chỉ rõ vị trí đặt animal:
  - Chim gần cây lớn/cây đa trong công viên.
  - Cá dưới chân đập.
  - Sóc cạnh bụi rác khu dân cư.
- Nếu muốn visual đẹp, người dùng cần duyệt animation đơn giản: chim bay, cá bơi, sóc chạy lên cây.

### 7.5 Acceptance checklist

- C4 có inventory 8 ô.
- Cứu cá bị chặn đúng nếu chưa thông đủ cống.
- Cứu 1/2/3 con trigger đúng thoại Bác Xanh.
- Sau C4 có chapter break và recap đầu C5.

---

## 8. Chapter 5 — Cộng Đồng Và Kết Thúc

### 8.1 Mục tiêu chapter

- Chuyển từ môi trường sang con người.
- Thuyết phục Cô Tư, Anh Tùng, Ông Sáu.
- Trồng cây.
- Ending Nhà văn hóa sáng đèn.

### 8.2 Flow bắt buộc

1. Player trước Nhà văn hóa.
2. Bác Xanh nói recap đầu C5 và intro C5 nguyên văn.
3. Player tự chọn thứ tự thuyết phục 3 NPC.
4. Cô Tư tại tạp hóa: context clue ảnh con gái ở công viên xanh.
5. Anh Tùng tại công viên: context clue chim bay quanh rác.
6. Ông Sáu bờ sông NE: context clue rãnh nước chảy xuống sông.
7. Mỗi NPC có 3 lựa chọn A/B/C.
8. Sau thuyết phục đủ 3 người, Bác Xanh khen.
9. Player trồng 3-7 cây ở khu sạch.
10. Về Nhà văn hóa.
11. Ending visual sequence.
12. Ending A/B/C theo chỉ số thật.

### 8.3 Agent cần implement

- C5 conviction UI thật, không auto chọn B khi bấm E.
- Hiển thị lựa chọn A/B/C rõ ràng.
- Dùng response đúng theo từng NPC, không title chung `NPC`.
- CA meter phải hiển thị và update.
- Context clue cần có object hoặc visual prompt.
- NPC state sau convinced phải lưu trong `GameState`.
- Ending condition phải xét ES, PL, CA, animals, trees, không chỉ ES.

### 8.4 Task cho người dùng

- Duyệt vị trí context clue:
  - Ảnh con gái của Cô Tư trên quầy.
  - Chim/nhựa gần Anh Tùng.
  - Rãnh nước cạnh Ông Sáu.
- Duyệt vị trí 3-7 cây trồng. Hiện có `TreeZone_1..5`, cần xác nhận khu tương ứng.
- Duyệt visual ending Nhà văn hóa sáng đèn và NPC tụ họp.

### 8.5 Acceptance checklist

- Người chơi có thể chọn A/B/C thật.
- Chọn A không tăng CA.
- Chọn B tăng CA +10.
- Chọn C tăng CA +3.
- Ending A chỉ đạt khi đủ tất cả điều kiện, không chỉ ES.
- Nhà văn hóa có payoff visual trước ending text.

---

## 9. UI Bắt Buộc

### 9.1 HUD cần có

- Quest tracker: chapter, quest title, progress.
- 3 chỉ số riêng hoặc rõ ràng: ES, PL, CA.
- Inventory bar 5 ô, C4 chuyển 8 ô.
- Scanner overlay khi Q active.
- Interaction prompt `[E]`.
- Dialogue panel.
- Choice panel A/B/C.
- Chapter break fade.
- Optional/minimum later: minimap.

### 9.2 UI hiện tại thiếu gì

- Thiếu CA meter.
- Thiếu inventory bar.
- Thiếu minimap.
- Choice UI hiện chưa đúng vì E auto chọn B.
- Quest titles hiện dùng không dấu trong code ở nhiều chỗ, cần thống nhất tiếng Việt có dấu như UI hiện tại hoặc ít nhất không sai nghĩa.

---

## 10. Lỗi Hiện Tại Đã Gặp Và Cần Note Lại

### 10.1 Interaction E không xử lý thật

Hiện trạng:

- `InteractionDetector` tìm nearest interactable và hiện prompt.
- Khi bấm E, client gọi `events.OnInteractionPrompt:FireServer("INTERACT", true, interactId)`.
- `InteractionServer` chỉ dùng `OnInteractionPrompt` để fire lại UI prompt, không resolve `interactId` thành object.
- Kết quả: bấm E không gọi `handleInteraction`.

Fix bắt buộc:

- Tạo RemoteEvent riêng `OnInteractRequested` hoặc đổi handler hiện tại để nhận `interactId`.
- Server tìm object có `InteractId`, validate distance, rồi gọi `handleInteraction(player, object)`.

### 10.2 Quest flow sai so với GDD

Hiện trạng trong `QuestManager`:

- `Q06_PlaceBins` đang chapter 2, nhưng placement chính phải là C3.
- `Q07_RescueAnimals` đang chapter 3, nhưng animal rescue phải là C4.
- `Q08_ConvinceResident` đang chapter 3, nhưng thuyết phục NPC phải là C5.
- `Q09_PlaceSigns` đang chapter 4, nhưng biển báo thuộc C3.
- `Q10_ConvinceCommunity` đang chapter 4, nhưng thuyết phục cộng đồng thuộc C5.

Fix bắt buộc:

- Rebuild quest list đúng 5 chapter và 3 phase C2.
- Không chỉ đổi title; phải đổi trigger, unlock, chapter break, gating.

### 10.3 Q04 Sorting Tutorial có thể kẹt

Hiện trạng:

- `Q04_SortingTutorial` trigger là `SortTrash`, required 5.
- `TrashInteraction.SortTrash()` không gọi generic `QuestManager.ReportProgress()` cho Q04.
- `ReportSortingCorrect()` chỉ xử lý riêng `Q05_SortChallenge`.

Fix bắt buộc:

- Khi active quest là Q04, sort action phải progress tutorial step.
- Sau 5 tutorial sorts, complete Q04.

### 10.4 DialogueManager dùng quest ID không tồn tại

Hiện trạng:

- Check `Q03_SortTrash` không tồn tại.
- Check `Q04_PlaceBins` không tồn tại.

Fix bắt buộc:

- Đổi sang quest ID thật sau khi rebuild quest flow.
- Tốt nhất dùng explicit phase state, không hard-code sai ID.

### 10.5 Bin có cả `TrashType` và `BinType`

Hiện trạng:

- Một số thùng RC body có `TrashType=organic/recycle/rest/hazard` và `BinType=...`.
- `InteractionServer` ưu tiên `TrashType` trước, nên thùng có thể bị xử lý như rác.

Fix bắt buộc:

- Gỡ `TrashType` khỏi bin/dropzone.
- Hoặc đổi priority: `BinType` trước `TrashType`.
- Tốt nhất: bin chỉ có `BinType`, rác chỉ có `TrashType`.

### 10.6 Không có animal objects

Hiện trạng:

- Audit không thấy object nào có `AnimalId`.

Fix bắt buộc:

- Thêm/đánh dấu chim/cá/sóc theo Chapter 4.

### 10.7 Không có culvert objects

Hiện trạng:

- Có hotspot `Dam_C1/C2/C3`, nhưng không thấy object có `CulvertId`.

Fix bắt buộc:

- Tạo hoặc đánh dấu 3 cống thật.

### 10.8 Portal/Destination duplicate

Hiện trạng:

- `Portal1` có 2 instance cùng path/name.
- `Portal1Destination` có 2 instance cùng path/name.

Rủi ro:

- Script dùng `FindFirstChild` có thể lấy object không mong muốn.
- Khó debug teleport.

Task cần xử lý:

- Người dùng/agent cần dọn duplicate sau khi xác nhận instance nào là bản đúng.

### 10.9 Runtime asset errors

Console hiện báo:

- `The experience doesn't have access permission to use asset id 77816723936944.`
- `The experience doesn't have access permission to use asset id 109757070637810.`
- `The current thread cannot require using asset ID (lacking capability LoadUnownedAsset)` tại `Workspace.=== VEGETATION ===.Jungle Tree.Configuration.CoreSystem`, line 265.
- Texture pack errors từ Sketchfab/SurfaceAppearance.

Rủi ro:

- Không phải lỗi gameplay GreenAgain trực tiếp, nhưng làm console bẩn.
- Có thể gây performance/visual issue.

Task cho người dùng:

- Chia sẻ quyền asset nếu muốn dùng asset đó.
- Hoặc cho phép agent xóa/disable scripts từ imported vegetation/Sketchfab assets.

### 10.10 DayNightCycle có thể phá chapter lighting

Hiện trạng:

- `HUDHandler` tween Lighting theo chapter.
- `ServerScriptService.DayNightCycle` liên tục tăng `Lighting.ClockTime` mỗi 0.05s.

Rủi ro:

- Chapter visual preset không ổn định.

Fix đề xuất:

- Disable DayNightCycle trong GreenAgain flow, hoặc chỉ chạy khi không ở gameplay.
- Nếu muốn day/night, phải tích hợp với EnvironmentManager, không chạy độc lập.

---

## 11. Refactor Kỹ Thuật Được Khuyến Nghị

### 11.1 Quest state nên rõ phase

Đề xuất quest/phase chuẩn:

- `C1_PICKUP_ARRIVAL_TRASH`
- `C1_TALK_BAC_XANH_UNLOCK_SCANNER`
- `C2A_SCAN_PICNIC_AREA`
- `C2A_CLEAN_PICNIC_AREA`
- `C2B_SORTING_SAMPLES`
- `C2B_SORTING_SEMI_GUIDED`
- `C2B_SORTING_FREE_RC`
- `C2C_REVEAL_RESIDENTIAL_AND_DAM`
- `C2C_CLEAN_RESIDENTIAL`
- `C2C_TRASH_RETURNS_REVEAL`
- `C2_BREAK`
- `C3_INFRA_START`
- `C3_PLACE_BIN_RESIDENTIAL`
- `C3_OPTIONAL_SIGN_COTU`
- `C3_PLACE_BIN_PARK`
- `C3_PLACE_SIGN_RIVER_NE`
- `C3_CLEAR_CULVERT_1`
- `C3_SORT_REMAINING_TRASH`
- `C4_DETECT_ANIMALS`
- `C4_RESCUE_BIRD`
- `C4_RESCUE_FISH`
- `C4_RESCUE_SQUIRREL`
- `C4_SORT_RESCUE_TRASH`
- `C4_BREAK`
- `C5_INTRO_COMMUNITY`
- `C5_CONVINCE_COTU`
- `C5_CONVINCE_ANH_TUNG`
- `C5_CONVINCE_ONG_SAU`
- `C5_PLANT_TREES`
- `C5_RETURN_NHA_VAN_HOA`
- `ENDING_SEQUENCE`

### 11.2 Data-driven definitions

Nên gom config vào ModuleScript rõ ràng:

- `QuestDefinitions`.
- `DialogueDefinitions` hoặc giữ `DialogueManager` nhưng không hard-code sai quest IDs.
- `MapDefinitions`: zone IDs, positions, unlock chapter.
- `TrashDefinitions`: trash type, correct bin, display name.
- `InteractionRegistry`: lookup `InteractId` -> instance.

### 11.3 Server authoritative

- Server quyết định progress, inventory, score, NPC state.
- Client chỉ hiển thị UI và gửi request.
- Không dùng `_G` trên client cho choices nếu có thể tránh. Dùng local state trong `HUDHandler`.

---

## 12. Task Tổng Hợp Theo Chương

### Chapter 1 tasks

Agent làm:

- Sửa E interaction.
- Đặt/gate rác C1 đúng tuyến.
- Sửa scanner unlock sau Bác Xanh.
- Sửa dialogue C1 trigger.

Người dùng làm:

- Xác nhận tuyến Portal1Destination -> Nhà văn hóa.
- Duyệt opening hook/camera style.

### Chapter 2 tasks

Agent làm:

- Implement scanner phase gating.
- Fix sorting tutorial 3+2.
- Fix bin attributes/priority.
- Add inventory UI 5 ô.
- Implement dynamic trash reveal đúng C2C.
- Implement C2 chapter break.

Người dùng làm:

- Xác nhận RC interaction parts.
- Xác nhận công viên/picnic area visual.
- Xác nhận vị trí đập thật hoặc cho phép tạo primitive.

### Chapter 3 tasks

Agent làm:

- Rebuild quest flow C3.
- Implement placement validation.
- Add item counts 3 bins/2 signs.
- Implement culvert 1 clear.
- Add C3 feedback dialogue.

Người dùng làm:

- Gán placement zones generic hiện tại vào khu cụ thể.
- Duyệt model thùng/biển nếu muốn đẹp hơn placeholder.

### Chapter 4 tasks

Agent làm:

- Add animal rescue system.
- Add inventory temporary 8 slots.
- Add fish gate to culvert/PL.
- Add C4 chapter break.

Người dùng làm:

- Cung cấp/duyệt model chim/cá/sóc.
- Chỉ vị trí chính xác của 3 animal objects.
- Duyệt animation/visual đơn giản.

### Chapter 5 tasks

Agent làm:

- Fix conviction UI A/B/C.
- Add CA meter.
- Implement NPC state and ending condition.
- Implement tree planting validation.
- Implement ending manager.

Người dùng làm:

- Duyệt context clues của 3 NPC.
- Duyệt Nhà văn hóa ending staging: NPC đứng đâu, đèn ở đâu, cây/animal visual nào xuất hiện.

### Global cleanup tasks

Agent làm nếu được phép:

- Dọn duplicate Portal1/Portal1Destination sau khi xác nhận bản đúng.
- Disable/xóa scripts imported asset gây `LoadUnownedAsset` nếu không cần.
- Disable DayNightCycle hoặc tích hợp vào chapter lighting.

Người dùng làm:

- Cấp quyền asset thiếu nếu muốn giữ asset Marketplace.
- Quyết định giữ hay bỏ lobby/portal về lâu dài.

---

## 13. Definition Of Done Cho Bản Bám GDD v4

Game được xem là bám GDD v4 khi đạt toàn bộ điều kiện sau:

- Player chơi được từ C1 đến Ending không dùng Studio/exploit/debug.
- Tất cả tương tác chính dùng E đúng UI.
- Dialogue chính dùng nguyên văn từ dialogue doc.
- Scanner unlock cuối C1, marker unlock theo phase.
- Sorting tutorial có 3 mẫu + 2 bán hướng dẫn.
- Inventory 5 ô từ C2B, C4 tạm 8 ô.
- Dynamic trash reveal xảy ra đúng C2C.
- C3 có placement + thông ít nhất Cống 1.
- Có 3 cống riêng, thông được từng cống.
- C4 cứu được chim/cá/sóc với gate đúng.
- C5 thuyết phục 3 NPC bằng lựa chọn A/B/C thật.
- Có ES, PL, CA visible và ending xét đủ 3 chỉ số + animals + trees.
- Có chapter breaks cuối C2 và C4.
- Ending tại Nhà văn hóa sáng đèn, NPC tụ họp.
- Không có blocker console từ GreenAgain scripts.
- Không có spawn duplicate do agent tạo.
- Không có asset/interaction object duplicate gây nhầm logic.

---

## 14. Đánh Giá Hiện Trạng Khi Viết Doc Này

Mức hoàn thiện tổng thể so với GDD v4: khoảng 30/100.

Chi tiết:

- Map/asset nền: 45-55%.
- UI/HUD khung: 35-40%.
- Core gameplay end-to-end: 15-25%.
- Bám flow GDD v4: 20-25%.
- Dialogue content đã nhập: 50-60%, nhưng trigger thực tế chưa đúng.
- Playable từ đầu đến cuối: chưa đạt.

Các điểm tốt:

- Có khung script GreenAgain.
- Có HUD cơ bản.
- Có NPC và một số map objects đúng vibe.
- Có RC và thùng phân loại.
- Có hotspots.
- Play mode không crash do GreenAgain scripts.

Các blocker cần sửa trước tiên:

1. E interaction không xử lý thật.
2. Quest flow sai chapter.
3. Q04 sorting có thể kẹt.
4. DialogueManager check quest ID không tồn tại.
5. Bin có `TrashType` gây nhầm thành rác.
6. Chưa có animal/cống gameplay thật.
7. UI thiếu CA/inventory/choice đúng.
8. Ending chỉ là fade text, chưa có payoff Nhà văn hóa.

---

*File này là checklist triển khai. Khi agent code, đọc file này trước, sau đó đối chiếu từng thay đổi với GDD gốc và dialogue doc.*
