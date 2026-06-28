# GREEN AGAIN v4: THỊ TRẤN VEN SÔNG
## Game Design Document — v4.0 (Map kiểu Việt Nam)

> **Nền tảng:** Roblox
> **Thể loại:** Educational Simulation / Adventure
> **Đối tượng:** 10–16 tuổi
> **Thời lượng:** ~55-70 phút (3 buổi chơi ~20 phút)
> **Thông điệp cốt lõi:** Dọn rác chỉ là bước đầu. Thị trấn xanh bền vững cần hạ tầng đúng, nguyên nhân được xử lý và cộng đồng thay đổi cùng nhau.
> **Dựa trên:** GDD v2 + v3 changes + 6 audit (Emotional Canvas, Flow, Peak-End, FTUE, Goal Density, Design Pillars)

---

## PHẦN 1: TỔNG QUAN

### 1.1 Concept một câu

> Người chơi là tình nguyện viên môi trường đến một thị trấn ven sông đang ô nhiễm, phải phục hồi nó bằng cách dọn rác, xử lý nguyên nhân, cứu động vật và thuyết phục người dân thay đổi thói quen.

### 1.2 Bốn cột trụ thiết kế

| # | Cột trụ | Ý nghĩa | Ưu tiên | Hy sinh |
|---|---------|---------|---------|---------|
| 1 | **Nhân quả hữu hình** | Mỗi hành động có phản hồi thấy được trong thế giới. Đập tắc → sông đục → cá yếu. | Visual feedback hơn UI số | Trừu tượng — game từ chối giải thích bằng text những gì có thể cho thấy |
| 2 | **Giáo dục nhúng** | Kiến thức là kết luận người chơi tự rút ra từ feedback loop. Không bài giảng. | "Aha!" moments hơn instruction | Giảng dạy trực tiếp — không có quiz, không có chuyên gia đứng nói |
| 3 | **Không bế tắc** | Không fail state, không load lại, không mất tiến trình. Mọi đường đều đi tiếp được. | Tiến trình vĩnh viễn hơn high-stakes tension | Căng thẳng — game chọn an toàn hơn là kịch tính |
| 4 | **Gắn bó được vun đắp** | Người chơi trở thành một phần của thị trấn qua hành động. Từ người lạ → người nhà. | Quan hệ hơn nhiệm vụ, di sản hơn điểm số | Power fantasy — không phải anh hùng, chỉ là người quan tâm |

**Pillar 4 (Gắn bó được vun đắp) — chi tiết:**

*Đây là pillar mới xuất hiện trong v4, được củng cố bởi map làng quê VN, Nhà văn hóa làm trung tâm, và Bác Xanh có hồn.*

| Yếu tố | Cách pillar này chi phối thiết kế |
|--------|----------------------------------|
| Không gian | Nhà văn hóa là "nhà" — nơi Bác Xanh luôn đợi, nơi ending diễn ra, nơi NPC tụ họp |
| Mentor | Bác Xanh không phải quest kiosk — có tên, có lịch sử, có cảm xúc, nhớ người chơi |
| NPC | Mối quan hệ tiến triển (Unaware → Aware → Considerate), NPC nhớ hành động của người chơi |
| Tiến trình | Spawn tách khỏi Bác Xanh → hành trình outsider → insider. Chapter breaks duy trì quan hệ qua thời gian |
| Ending | Nhà văn hóa sáng đèn + NPC tụ họp = visual payoff của "mình thuộc về nơi này" |

**Target feeling:** Earned Belonging — Sự gắn bó được vun đắp.

**Design heuristics:**
- Warmth over instruction — Lời Bác Xanh dạy nhiều hơn tutorial popup
- Presence over popup — NPC phản ứng trong thế giới thay vì UI notification
- Suggestion over explanation — Context clue thay vì text dài
- Tenderness over force — Cứu động vật là hành động nhẹ nhàng
- Community over hero — Cả thị trấn cùng thay đổi, không chỉ mình người chơi
- Wood over metal — Vật liệu tự nhiên (gỗ, tre, đá, ngói) thay vì nhựa, kim loại bóng
- Relationship over task — Thuyết phục NPC là xây dựng lòng tin, không phải "làm quest"

### 1.3 Session Structure (từ Goal Density Audit)

Game được chia thành **3 buổi chơi** với explicit chapter breaks:

| Buổi | Chapter | Thời gian | Kết thúc bằng |
|------|---------|-----------|---------------|
| Buổi 1 | C1 + C2 | ~20 phút | Chapter break: Bác Xanh "Ngày mai quay lại nhé" |
| Buổi 2 | C3 + C4 | ~25 phút | Chapter break: Bác Xanh "Ngày mai mình làm nốt nhé" |
| Buổi 3 | C5 + Ending | ~15 phút | Ending A/B/C |

---

## PHẦN 2: BẢN ĐỒ THỊ TRẤN VEN SÔNG (v4)

> Game dùng **một thị trấn duy nhất**. Không loading screen. Chapter là trạng thái tiến trình, không phải map riêng.

### 2.1 Tổng quan địa lý

Thị trấn Ven Sông nằm trong thung lũng nhỏ, bao bọc bởi đồi núi và rừng cây tứ phía (Bắc, Nam, Tây, Đông Bắc). Một con sông chảy từ Bắc (gần Công viên) uốn lượn xuống Đông Nam, qua một con đập có 3 cống xả ở phía Nam. Đường trục chính nằm ngang (Y~50%) chia nửa trên (Khu dân cư, Nhà cô Tư, Công viên) và nửa dưới (Spawn, Nhà văn hóa, Trung tâm Tái chế).

### 2.2 Sơ đồ bố cục

```
┌──────────────────────────────────────────────────────────────────┐
│                    🌲 RỪNG CÂY — ĐỒI NÚI BAO QUANH                │
│                                                                   │
│  ┌──────────────────────┬──────────┬──────────────────────────┐  │
│  │   🏘️ KHU DÂN CƯ     │ 🏚️ NHÀ   │     🌳 CÔNG VIÊN         │  │
│  │   PL: 60             │ CÔ TƯ    │     PL: 55               │  │
│  │   🟠 Residential St. │          │     🟠 Picnic Area       │  │
│  │   🐿️ Sóc (C4)       │ 👩 Cô Tư │     🧑 Anh Tùng         │  │
│  │                      │          │     👧 Bé Na             │  │
│  │                      │          │     🐦 Chim (C4)         │  │
│  │                      │          │     [Cối xay gió] 🪨    │  │
│  └──────────────────────┴──────────┴──────────────────────────┘  │
│                                                                   │
│ ════════════════════ ĐƯỜNG TRỤC CHÍNH (~Y=50%) ══════════════════ │
│                                                                   │
│  ┌─────────────────────────┬────────────────────────────┐        │
│  │  ⚡ SPAWN (góc dưới trái)│  🏛️ NHÀ VĂN HÓA            │  ♻️ RC │
│  │                         │  Mái ngói đỏ               │        │
│  │                         │  🧓 Bác Xanh               │  4 thùng│
│  │                         │  👩‍🔧 Chị Lan              │        │
│  └─────────────────────────┴────────────────────────────┘        │
│                                                                   │
│                    ≈ ≈ ≈ ≈ ≈ SÔNG ≈ ≈ ≈ ≈ ≈                       │
│                                                                   │
│  ┌──────────────────────────────────────────────────────────┐    │
│  │              🏗️ ĐẬP NƯỚC (3 cống xả) — PL: 80            │    │
│  │    ┌─────────┐    ┌─────────┐    ┌─────────┐             │    │
│  │    │ Cống 1  │    │ Cống 2  │    │ Cống 3  │             │    │
│  │    │  🔴 80   │    │  🔴 80   │    │  🔴 80   │            │    │
│  │    └─────────┘    └─────────┘    └─────────┘             │    │
│  │    🐟 Cá (C4) — dưới chân đập                             │    │
│  └──────────────────────────────────────────────────────────┘    │
│                                                                   │
│                    🌲 RỪNG CÂY — ĐỒI NÚI                            │
└──────────────────────────────────────────────────────────────────┘
```

### 2.3 Zones & Hotspots

| Zone | Vị trí | PL ban đầu | Hotspot | Mở khóa |
|------|--------|-----------|---------|---------|
| Khu dân cư | NW (0-35%, 20-50%) | 60 | 🟠 Residential St. | C2C |
| Nhà cô Tư | N-center (35-45%, 20-50%) | — | — (zone phụ) | C3 |
| Công viên | NE (45-70%, 15-50%) | 55 | 🟠 Picnic Area | C2A |
| Nhà văn hóa | SW (20-45%, 50-75%) | — | 🟢 Bác Xanh (neo) | C1 |
| Trung tâm Tái chế | SE (45-65%, 50-75%) | — | Hub phân loại | C2B |
| Đập nước | S (45-75%, 75-95%) | 80 | 🔴 Cống 1, 2, 3 | C2C/C3 |
| Ven sông NE | NE (70-80%, 20-35%) | 45 | 🟡 Riverside NE | C2C |
| Ven sông khúc quanh | Giữa dòng | 40 | 🟡 Riverside Bend | C3 |

### 2.4 NPC Positions (v4)

| NPC | Vị trí | Tọa độ (%) | Phạm vi | Xuất hiện |
|-----|--------|-----------|---------|-----------|
| Bác Xanh | Ghế đá trước Nhà văn hóa | 32, 62 | Sân Nhà văn hóa | C1→C5 |
| Cô Tư | Trước tiệm tạp hóa, Nhà cô Tư | 40, 35 | ~15 studs | C2→C5 |
| Anh Tùng | Thảm picnic, Công viên | 58, 30 | ~20 studs | C2→C5 |
| Ông Sáu | Bờ sông NE, cạnh mỏm đá | 75, 25 | ~25 studs | C3→C5 |
| Chị Lan | Nhà văn hóa / RC | 55, 65 | ~25 studs | C2B→C5 |
| Bé Na | Gần cây lớn, Công viên | 60, 40 | ~10 studs | C2→C5 |

### 2.5 Khoảng cách chính

| Tuyến | Khoảng cách | Thời gian đi bộ |
|-------|------------|-----------------|
| Spawn → Nhà văn hóa | ~80 studs | ~5 giây |
| Nhà văn hóa → RC | ~70 studs | ~4 giây |
| Nhà văn hóa → Công viên | ~160 studs | ~10 giây |
| Nhà văn hóa → Khu dân cư | ~130 studs | ~8 giây |
| Công viên → RC | ~100 studs | ~6 giây |
| RC → Đập nước | ~120 studs | ~7 giây |
| Khu dân cư → Đập nước | ~380 studs | ~22 giây (dài nhất) |
| Bờ sông NE → Nhà văn hóa | ~180 studs | ~11 giây |

---

## PHẦN 3: HỆ THỐNG GAMEPLAY

### 3.1 Eco Scanner

**Mở khóa:** Cuối Chapter 1 | **Phím:** Q toggle | **Phạm vi:** 50 studs

| Màu marker | PL khu vực | Ý nghĩa |
|-----------|-----------|---------|
| 🟡 Vàng | < 40 | Ô nhiễm nhẹ — theo dõi |
| 🟠 Cam | 40–70 | Ô nhiễm trung bình — nhặt rác + phân loại |
| 🔴 Đỏ | > 70 | Ô nhiễm nghiêm trọng — ưu tiên xử lý ngay |
| ✅ Xanh | < 20 | Đã xử lý — không cần can thiệp |

### 3.2 Inventory & Sorting

- **Inventory:** 5 ô, bắt đầu từ C2B
- **Sorting:** 4 thùng tại RC — Hữu cơ (xanh lá) / Tái chế (xanh dương) / Vô cơ (vàng) / Độc hại (đỏ)
- **Spill effect (v3):** Sort sai → vệt bẩn xuất hiện → [E] dọn 1 giây → thử lại. Không phạt điểm. Tích tụ 3+ vệt → Bác Xanh nhắc nhẹ. Tự reset khi rời RC >30s hoặc sort đúng 3 lần liên tiếp
- **Inventory exception C4 (v4 MỚI):** Khi vào C4, inventory mở rộng tạm thời lên 8 ô. Cho phép nhặt rác cứu hộ ở cả 3 điểm (Công viên, Đập, Khu dân cư) trước khi về RC sort 1 lần duy nhất. Sau khi sort, inventory trở về 5 ô

### 3.3 Đập nước & 3 cống xả (v4 MỚI)

Thay thế cống đơn của v3. Đập nước nằm ở cuối dòng sông (mép Nam), gồm 3 cống độc lập:

| Cống | PL ban đầu | Mở khóa phát hiện | Mở khóa thông |
|------|-----------|-------------------|---------------|
| Cống 1 (trái) | 80 | C2C (Bác Xanh dẫn đến) | C3 |
| Cống 2 (giữa) | 80 | C2C | C3 |
| Cống 3 (phải) | 80 | C2C | C3 |

**Cơ chế thông cống:**
1. Nhặt sạch rác trong bán kính 15 studs quanh cống đó
2. Giữ E 3 giây để thông
3. Mỗi cống thông → PL khu vực Đập giảm 25 điểm
4. Thông cả 3 → Đập hoạt động bình thường, nước chảy sạch

**Pollution Spread Event (3 giai đoạn):**

| Giai đoạn | Điều kiện | Cảnh báo | Hậu quả |
|-----------|-----------|----------|---------|
| 1 | 1 cống tắc, PL > 75% | "⚠ Một cống xả đang tắc. Nước bắt đầu ứ đọng." | — |
| 2 | 2 cống tắc, sau 3 phút | "🚨 2 cống đã tắc! Rác tràn ra khúc quanh sông. Ô nhiễm sông +10." | Riverside PL +10 |
| 3 | 3 cống tắc, sau 5 phút | "🔴 NGUY CẤP: Toàn bộ đập tắc! Cá dưới chân đập bị ảnh hưởng nghiêm trọng." | Cá khó cứu hơn |

### 3.4 Animal Rescue System

| Động vật | Vị trí (v4) | Vấn đề | Điều kiện cứu | Phạm vi dọn |
|----------|------------|--------|---------------|------------|
| 🐦 Chim | Công viên, gần cây lớn | Mắc túi nhựa | Nhặt sạch rác nhựa | 15 studs |
| 🐟 Cá | Dưới chân đập | Nước bẩn, cá yếu | Ít nhất 2/3 cống đã thông + PL Đập < 40 | — |
| 🐿️ Sóc | Khu dân cư, cạnh bụi rác | Rác độc hại quanh | Nhặt toàn bộ rác độc hại + phân loại đúng | 20 studs |

> **v4 improvement:** Gate cá xảy ra ngay tại Đập — người chơi đã ở sẵn, không cần quay lại nơi khác để thông cống thêm.

### 3.5 Placement System

| Vật phẩm | Ảnh hưởng | Bán kính |
|----------|-----------|----------|
| Thùng rác | Giảm Spawn Rate 50% | 25 studs |
| Biển cấm xả rác | Tăng CA +3, NPC có thoại mới | 30 studs |
| Cây xanh (C5) | Tăng ES +5, visual thay đổi | 15 studs |

**Hệ thống feedback vị trí:**
- 🟢 Good Location — tối ưu, +5 ES
- 🟡 Low Impact — được nhưng hiệu quả thấp, +1 ES
- 🔴 Invalid — không đặt được

---

## PHẦN 4: THIẾT KẾ TỪNG CHAPTER

### 📘 CHAPTER 1: KHỞI ĐẦU (5-8 phút)

**Mục tiêu học:** Di chuyển, nhặt rác, gặp mentor, nhận Scanner
**Chỉ số đầu:** ES 10, PL 70, CA 0

#### Flow:

```
[SPAWN góc dưới trái]
  → Text mờ: "Thị trấn Ven Sông — một buổi chiều tháng Sáu..." (fade 4s)
  → Camera zoom nhẹ: thấy đường đất, mái ngói đỏ phía xa, dòng sông đục
  → Rác đầu tiên nằm ngay trước mặt (5-8 studs), có particle nhẹ

  ↓ Đi dọc đường dưới, men rừng trái

[ĐƯỜNG ĐẤT DẪN VÀO LÀNG] (~80 studs)
  → Nhặt rác rải rác trên đường (auto-disappear)
  → Món rác đầu tiên: tiếng "tinh" nhẹ + particle xanh lá + text: "Tình nguyện viên — đã đến lúc dọn dẹp."
  → Optional: 1 tấm biển quảng cáo cũ đổ bên đường — nhặt được, text: "Biển quảng cáo từ 5 năm trước... thị trấn này từng đông vui hơn."

  ↓

[NHÀ VĂN HÓA — mái ngói đỏ]
  → Gặp Bác Xanh ngồi ghế đá trước cửa
  → Hội thoại 3 beat có tương tác:

  Beat 1 (2 đoạn — tên + khen):
    "Chà! Cháu là tình nguyện viên mới... Bác là Bác Xanh — bác đã sống ở
     thị trấn Ven Sông này từ hồi nó còn xanh mướt, chim hót đầy công viên..."
    "Mà cháu vừa dọn sạch đường vào làng một mình đấy! Nhanh thật! Cảm ơn cháu."
    → [E] "Cháu cảm ơn bác"

  Beat 2 (2 đoạn — vấn đề):
    "Nhưng bác phải nói thật: rác sạch hôm nay, ngày mai lại đầy.
     Không phải tại cháu — tại mấy cái cống bị tắc, tại người dân chưa hiểu..."
    → Camera pan nhẹ về phía dòng sông đục, cánh đồng héo

  Beat 3 (3 đoạn — Scanner):
    "Bác có cái này — Máy Quét Sinh Thái. Hồi xưa bác dùng nó để giữ cho
     thị trấn luôn xanh. Giờ đến lượt cháu. Cháu muốn thử không?"
    → [E] Nhận Scanner — flash xanh, icon Q hiện
    "Bấm Q để bật. Đi về phía công viên đằng kia — máy sẽ đổi màu khi
     cháu đến gần điểm ô nhiễm. Có gì không hiểu thì quay lại đây."

Chapter 1 hoàn thành — Unlock: Eco Scanner (Q), UI 3 chỉ số
```

---

### 📗 CHAPTER 2: TÌM NGUỒN Ô NHIỄM (11-14 phút)

**Mục tiêu học:** Dùng Scanner, quản lý inventory, phân loại rác
**Chỉ số đầu:** ES 25, PL 65, CA 5

Chia thành 3 mini-phase để tránh vách đá độ phức tạp:

#### Phase 2A: Làm quen Scanner (3-4 phút)

**Mở khóa:** Scanner chủ động
**Chưa mở:** Inventory, Sorting, Dynamic spawn

```
Nhà văn hóa → Băng qua đường trục chính → Công viên (~160 studs)
  → Trên đường: camera pan toàn cảnh — thấy Khu dân cư (trái), Công viên + cối xay gió (phải)
  → Đến Picnic Area, bật Scanner (Q) → thấy marker 🟠 cam
  → Scanner tutorial popup: "🟡 Vàng = nhẹ | 🟠 Cam = trung bình | 🔴 Đỏ = nghiêm trọng"
  → Nhặt 3-4 món rác trong hotspot (auto-disappear)

Bác Xanh (qua UI): "Tốt lắm! Cháu thấy chưa — có những chỗ bẩn hơn mắt thường thấy."
```

#### Phase 2B: Học phân loại (4-5 phút)

**Mở khóa:** Inventory 5 ô + Sorting system

```
Bác Xanh dẫn từ Công viên → RC

Tại RC:
  → Inventory limit kích hoạt (5 ô)
  → Bác Xanh đưa 3 món mẫu (1 hữu cơ, 1 tái chế, 1 vô cơ)
  → Highlight đúng thùng 1 giây — mỗi lần đúng: feedback + giải thích

Sau 3 món mẫu:
  → Bác Xanh đưa thêm 2 món: "Lần này cháu thử tự chọn đi, sai bác sửa."
  → Vẫn highlight nhưng trễ hơn (2 giây) — bước chuyển tiếp trước khi thả tự do

Sau 5 món (3 mẫu + 2 bán hướng dẫn):
  "Giỏi lắm! Giờ cháu thử tự làm nhé."
  → Spawn 2-3 món rác ngay trong/ngoài RC → người chơi tự nhặt và sort
  → Lần đầu mỗi loại rác MỚI: auto-highlight 1 giây
  → Từ lần 2: tự chọn không gợi ý
```

#### Phase 2C: Đối mặt thực tế (4-5 phút)

**Mở khóa:** Full 3 hotspot + Dynamic Trash Spawn

```
Scanner cập nhật: 2 marker mới — Residential St. (🟠), Dam C1 (🔴)

Bác Xanh dẫn đến Đập nước:
  "Cái đập này là chỗ ô nhiễm nặng nhất. Nó đỏ trên máy quét là có lý do —
   nếu bỏ mặc, rác sẽ theo nước tràn ra sông. Nhớ chỗ này, cháu sẽ phải quay lại."

→ Người chơi tự do:
  → Khu dân cư: nhặt rác Residential St.
  → Về RC sort (nếu đầy)
  → Quay lại Công viên: thấy rác ĐÃ QUAY LẠI!

  "Cháu thấy không? Rác đã quay lại. Dọn mà không ngăn nguyên nhân thì sẽ phải dọn mãi."

→ Dynamic spawn active toàn bản đồ
→ Inventory loop đầy đủ

Chapter 2 hoàn thành
```

#### 📌 CHAPTER BREAK 1 (cuối C2)

```
Bác Xanh (tại Nhà văn hóa):
  "Hôm nay cháu đã học được nhiều rồi — máy quét, phân loại rác, và quan trọng
   nhất là hiểu rằng rác sẽ quay lại nếu mình không ngăn nguyên nhân.
   Ngày mai cháu quay lại nhé — bác vẫn ở Nhà văn hóa. Có gì mình làm tiếp."

  → Màn hình tối 2 giây
  → Text: "Ngày hôm sau..."
  → Màn hình sáng lại — người chơi đứng trước Nhà văn hóa
  → Bác Xanh: "Cháu quay lại rồi! Hôm qua mình đã dọn dẹp và học phân loại rác.
     Giờ đến lúc ngăn rác quay lại vĩnh viễn."
```

---

### 📙 CHAPTER 3: NGĂN RÁC QUAY LẠI (10-15 phút)

**Mục tiêu học:** Placement system, xử lý đập nước, hiểu nhân quả dài hạn
**Chỉ số đầu:** ES 40, PL 55, CA 10

#### Flow (Spatial Circuit — kim đồng hồ NW→N→NE→SE):

```
Nhà văn hóa: Nhận 3 thùng rác + 2 biển báo từ Bác Xanh
  Tooltip: "Túi còn 5 ô. Có thể bỏ qua Nhà cô Tư nếu muốn — quay lại sau."

  ↓

[1] KHU DÂN CƯ: Đặt thùng rác + nhặt rác

  ↓

[2] NHÀ CÔ TƯ (OPTIONAL — có skip flag):
    Đặt biển báo gần tiệm

  ↓

[3] CÔNG VIÊN: Đặt thùng rác + nhặt rác

  ↓

[4] BỜ SÔNG NE (Ông Sáu): Đặt biển báo

  ↓

[5] ĐẬP NƯỚC: Nhặt rác quanh Cống 1 + thông cống 1 (giữ E 3s)
    → Nếu inventory đầy trước đó: về RC sort rồi quay lại

  ↓

[6] TRUNG TÂM TÁI CHẾ: Sort toàn bộ inventory

  ↓

Eco Scanner cập nhật: Picnic Area → ✅, Dam C1 → ✅
Bác Xanh: "Đó mới là xử lý đúng cách. Thùng rác để rác có chỗ về.
  Biển báo để người ta nhớ. Thông cống để nước không ứ đọng."

Chapter 3 hoàn thành — Unlock: Cống 2, 3 có thể thông; Bờ sông tiếp cận được để cứu cá
```

---

### 📕 CHAPTER 4: CỨU SINH VẬT (10-15 phút)

**Mục tiêu học:** Environmental gating, hậu quả ô nhiễm lên sinh vật
**Chỉ số đầu:** ES 55, PL 40, CA 20

> **v4 MỚI:** Inventory mở rộng tạm thời lên 8 ô. Cho phép gom rác cứu hộ ở cả 3 điểm, sort 1 lần duy nhất.

#### Flow:

```
Nhà văn hóa: Scanner hiện tín hiệu sinh vật — chim, cá, sóc
Bác Xanh: "Cháu có thấy tín hiệu mới không? Chúng vẫn còn sống — nhưng yếu lắm."

  ↓ Người chơi tự chọn thứ tự (cả 3 điểm mở cùng lúc)

[A] CÔNG VIÊN — Cứu chim:
    → Nhặt rác nhựa trong 15 studs (6-8 món)
    → Rác nhựa vào inventory mở rộng (8 ô)
    → E để cứu → chim bay lên ✓

[B] ĐẬP NƯỚC — Cứu cá:
    → Kiểm tra: ít nhất 2/3 cống đã thông? PL Đập < 40?
    → Nếu bị gate: đã ở sẵn Đập → thông thêm cống 2, 3 ngay tại chỗ
    → Đủ điều kiện → E để cứu → cá bơi lại ✓

[C] KHU DÂN CƯ — Cứu sóc:
    → Dùng Scanner tìm rác độc hại ẩn trong bụi cây (không visible bằng mắt thường)
    → Nhặt 4-5 món, phân loại đúng (cần nhận diện loại độc hại)
    → E để cứu → sóc chạy lên cây ✓

  ↓ Sau khi gom đủ rác cứu hộ ở cả 3 điểm

TRUNG TÂM TÁI CHẾ: Sort toàn bộ rác cứu hộ 1 lần duy nhất

  ↓

Sau khi cứu đủ 3 con:
  → ES tăng mạnh (+24)
  → Động vật xuất hiện tự nhiên trong khu vực liên quan
  → Visual map thay đổi rõ ràng

Bác Xanh (sau con đầu): "Cháu cứu được nó rồi!"
Bác Xanh (sau con thứ hai): "Một con nữa! Bác cứ tưởng thị trấn này hết cứu được rồi."
Bác Xanh (sau cả ba): "Ba con... Ngày cháu đến bác chỉ mong cháu dọn được cái đường vào làng.
  Mà giờ chim bay lại, cá bơi lại, sóc chạy trên cây. Cảm ơn cháu. Thật lòng đấy."

Chapter 4 hoàn thành
```

#### 📌 CHAPTER BREAK 2 (cuối C4)

```
Bác Xanh (tại Nhà văn hóa):
  "Thị trấn đã thay đổi nhiều rồi — công viên xanh, sông trong, động vật về.
   Nhưng vẫn còn một việc... quan trọng nhất. Ngày mai cháu quay lại nhé."

  → Màn hình tối 2 giây
  → Text: "Ngày hôm sau..."
  → Màn hình sáng lại — người chơi đứng trước Nhà văn hóa
  → Bác Xanh: "Cháu quay lại rồi! Hôm qua mình đã cứu được chim, cá, sóc.
     Giờ đến việc khó nhất — thay đổi con người."
```

---

### 📒 CHAPTER 5: CỘNG ĐỒNG VÀ KẾT THÚC (10-15 phút)

**Mục tiêu học:** Dialogue system, cộng đồng là yếu tố bền vững, trồng cây
**Chỉ số đầu:** ES 70-75, PL 30, CA 20-30

#### Flow:

```
Nhà văn hóa — Bác Xanh mở đầu:
  "Thị trấn đã sạch hơn nhiều. Nhưng mấy người dân — Cô Tư, Anh Tùng, Ông Sáu —
   họ vẫn chưa thay đổi thói quen. Nếu cháu rời đi mà họ vẫn vậy, một tháng nữa
   thị trấn sẽ lại như lúc cháu mới đến. Dọn rác là việc của tay.
   Thay đổi con người mới là việc của người thực sự quan tâm."

  ↓ Người chơi tự chọn thứ tự

[1] NHÀ CÔ TƯ — Thuyết phục Cô Tư:
    Context clue: ảnh con gái chơi ở công viên xanh trên quầy
    Lựa chọn tốt nhất: "50 hộ trong khu này, mỗi ngày một ít — cô thử tính
    một tháng có bao nhiêu rác trước cửa tiệm?"
    → CA +10, Cô Tư bỏ rác vào thùng

[2] CÔNG VIÊN — Thuyết phục Anh Tùng:
    Context clue: chim bay quanh, không dám đậu vì rác
    Lựa chọn tốt nhất: "Nếu ai cũng tự dọn, công viên sạch cho chính mình —
    với lại chim không bị mắc rác nhựa."
    → CA +10, cả nhóm cùng dọn

[3] BỜ SÔNG NE — Thuyết phục Ông Sáu:
    Context clue: rãnh nước nhỏ chảy từ đường xuống sông
    Lựa chọn tốt nhất: "Khi mưa, nước cuốn rác theo rãnh này xuống sông.
    Cá phải sống trong nước đó, ông ạ."
    → CA +10, Ông Sáu nhận ra "hóa ra cá bỏ đi là tại mình"

  ↓

[4] Trồng cây ở các khu đất sạch (3-7 vị trí, PL khu đó < 50%)
    → Mỗi cây: ES +5, visual đổi ngay

  ↓

[5] VỀ NHÀ VĂN HÓA — Ending
```

---

## PHẦN 5: HỆ THỐNG ENDING

### 5.1 Điều kiện

| Chỉ số | Ending A (Green Again) | Ending B (Đang phục hồi) | Ending C (Chưa bền) |
|--------|----------------------|------------------------|---------------------|
| Environment Score | ≥ 90 | 65–89 | < 65 |
| Pollution Level (TB) | < 20 | 20–45 | > 45 |
| Community Awareness | ≥ 70 | 40–69 | < 40 |
| Động vật đã cứu | 3/3 | 2–3/3 | 0–1/3 |
| Cây đã trồng | ≥ 3 | 1–2 | 0 |

### 5.2 Ending Payoff: Nhà văn hóa sáng đèn (v4 MỚI)

> Thay thế đài phun nước (v3) — phù hợp làng quê Việt Nam.

**Payoff visual sequence:**

```
Người chơi về Nhà văn hóa...

1. Từ xa, thấy Nhà văn hóa KHÔNG còn tối om như mọi lần:
   → Đèn lồng / đèn dầu thắp sáng bên trong, ánh vàng ấm hắt qua cửa sổ
   → Khói bếp nhẹ bay lên từ mái ngói đỏ

2. Đến gần, thấy NPC tụ họp:
   → Cô Tư ngồi trong sân, đang sắp hàng rau
   → Anh Tùng và nhóm bạn treo đèn lồng trước cửa
   → Bé Na chạy quanh sân, chim đậu trên vai
   → Ông Sáu ngồi ghế đá, cầm con cá vừa câu được
   → Chị Lan đứng ở cửa, vẫy tay chào

2. Bác Xanh đứng ở cửa Nhà văn hóa (thay vì ghế đá như mọi lần):
   "Cháu thấy không? Nhà văn hóa — nó tối om từ hồi thị trấn xuống dốc.
    Sáng nay bác ra đây, thấy đèn sáng, thấy người ta tụ tập lại...
    Bác đứng cả buổi không nói nên lời."

3. "Cháu đến thị trấn này là một người lạ. Mà giờ nhìn quanh đi —
    không còn lạ nữa. Mỗi cái cây, mỗi con chim, mỗi người dân...
    đều có một phần của cháu trong đó."

4. Camera pan chậm:
   → Nhà văn hóa sáng đèn, người tụ họp
   → Công viên xanh, chim bay, cối xay gió quay chậm (nếu ES > 85)
   → Dòng sông trong xanh, cá bơi
   → Đập nước chảy sạch qua 3 cống
   → Những cây non đã trồng

   Mỗi điểm dừng 2-3 giây, kèm text nhỏ ở góc:
   "Công viên — xanh trở lại" / "Dòng sông — trong trở lại" / "Cộng đồng — gắn kết trở lại"

5. EndingManager tổng kết → Nhận Ending A, B hoặc C
```

### 5.3 Nội dung Ending

**Ending A — Green Again:**
> "Môi trường bền vững không đến từ một mình ai. Nó cần hành động cá nhân, hạ tầng đúng chỗ và cả một cộng đồng cùng nhìn về một hướng. Cháu đã làm được cả ba. Thị trấn Ven Sông — xanh trở lại rồi. Nhờ cháu."

**Ending B — Đang trên đường phục hồi:**
> "Thị trấn đã sạch hơn nhiều so với lúc đầu. Nhưng để giữ vững điều này, cần nhiều người hơn — và cần tiếp tục. Cháu đã làm được nhiều rồi. Phần còn lại... biết đâu có ngày cháu quay lại?"

**Ending C — Sạch nhưng chưa bền:**
> "Thị trấn sạch hơn hôm cháu đến. Nhưng nếu không có gì thay đổi sâu hơn, chỉ cần vài tuần là rác sẽ quay lại. Cháu làm tốt phần của mình rồi. Chỉ tiếc là... chưa đủ. Nhưng biết đâu — mai cháu quay lại, mọi thứ sẽ khác?"

---

## PHẦN 6: BA CHỈ SỐ CHÍNH

```
ENVIRONMENT SCORE    ████████░░  45/100  ↑
POLLUTION LEVEL      ██████░░░░  62/100  ↓
COMMUNITY AWARENESS  ███░░░░░░░  30/100  ↑
```

**Visual progress trong thế giới:** Một bức tranh thị trấn treo trên tường Nhà văn hóa thay đổi theo ES/PL/CA — từ xám mờ → có màu nhạt → rực rỡ. 3 cây non trong sân Nhà văn hóa lớn dần theo từng chỉ số.

### Environment Score (ES) — 0-100 ↑

| Hành động | Điểm |
|-----------|------|
| Nhặt rác thông thường | +1 |
| Phân loại đúng | +2 |
| Phân loại đúng rác độc hại | +4 |
| Đặt thùng rác đúng vị trí (Good Location) | +5 |
| Đặt biển báo đúng vị trí | +3 |
| Thông cống (mỗi cống) | +10 |
| Cứu động vật | +8 |
| Trồng cây | +5 |
| Thuyết phục NPC thành công | +5 |

### Pollution Level (PL) — 0-100 ↓

| PL khu vực | Hậu quả |
|-----------|---------|
| < 25 | Ổn định, không sinh thêm rác |
| 25–50 | Rác sinh bình thường |
| 51–75 | Rác sinh nhanh hơn 50% |
| > 75 | Cảnh báo; nếu là cống → Pollution Spread Event |

### Community Awareness (CA) — 0-100 ↑

| CA | Hệ quả |
|----|--------|
| 0–30 | NPC xả rác bình thường |
| 31–60 | NPC trung lập, rác tái sinh bình thường |
| 61–80 | NPC ngừng xả rác, rác tái sinh chậm |
| 81–100 | NPC bỏ rác vào thùng, rác hầu như không tái sinh |

---

## PHẦN 7: TỔNG KẾT THAY ĐỔI v3 → v4

| # | Thay đổi | Audit nguồn | Impact |
|---|----------|------------|--------|
| 1 | **Map làng quê VN:** sông uốn lượn, đập 3 cống, Nhà văn hóa, rừng bao quanh | Map v4 doc | Toàn bộ layout + navigation |
| 2 | **Spawn tách khỏi Bác Xanh** (góc dưới trái → đi bộ vào làng) | Map v4 + FTUE | Narrative "người lạ vào làng", thêm 1-2 trip C1 |
| 3 | **Đập 3 cống** thay cống đơn | Map v4 | Pollution Spread 3 giai đoạn, gate cá tại chỗ |
| 4 | **2 Chapter breaks** cuối C2 và C4 | Flow + Goal Density | Game chia 3 buổi ~20 phút, phù hợp trẻ 10-12t |
| 5 | **Nhà văn hóa sáng đèn** thay đài phun nước | Peak-End Audit | Payoff phù hợp làng quê VN, ending có visual anchor |
| 6 | **C4: gom rác cứu hộ, sort 1 lần** (inventory mở rộng 8 ô) | Flow + Friction | Giảm 2 trip RC, trip 380s không bị ngắt |
| 7 | **C2B: thêm 2 món bán hướng dẫn** (highlight 2s) | Flow Audit | Scaffold removal từ từ, giảm sorting anxiety |
| 8 | **C1: opening hook** (text mờ + rác to + feedback món đầu) | FTUE Audit | Giảm "không biết làm gì" 10s đầu |
| 9 | **C3: Nhà cô Tư optional** (skip flag) | Flow + Friction | Circuit linh hoạt hơn, giảm inventory pressure |
| 10 | **Bác Xanh → Nhà văn hóa** (mái ngói đỏ) | Map v4 | Mentor space ấm cúng hơn Quảng trường |
| 11 | **Ông Sáu → bờ sông NE** (gần mỏm đá) | Map v4 | C5 NPC circuit NW→NE→NE gọn hơn |
| 12 | **RC cạnh Nhà văn hóa** (cùng nửa dưới) | Map v4 | Giảm ~40% số lần về RC (8-10 → 5-7) |
| 13 | **Cối xay gió quay** khi ES > 85 | Peak-End Audit | Secondary visual payoff, thấy từ mọi khu vực |
| 15 | **4 pillars** (thêm "Gắn bó được vun đắp") | Design Pillars Audit | Cột trụ thứ 4 định hướng mọi decision về NPC, narrative, emotional design |
| 16 | **Decision guidance:** KHÔNG thêm fast travel, achievement popup, daily reward | Design Pillars Audit | Giữ design sạch, không pha tạp |

---

*GREEN AGAIN v4 — Thị trấn Ven Sông — Game Design Document*
*Tháng 6/2026 — Tổng hợp từ 6 audit + Map v4*
