# GREEN AGAIN v3 — 3 THAY ĐỔI ƯU TIÊN CAO NHẤT

> Dựa trên kết quả 4 audit: Failure Loop, FTUE Hero's Journey, Flow, Player Motivation
> Tháng 6/2026

---

## THAY ĐỔI #1: CHIA CHAPTER 2 THÀNH 3 MINI-PHASE

**Vấn đề:** C1→C2 hiện tại kích hoạt 4 hệ thống mới cùng lúc (Inventory 5 ô + Sorting 4 loại + Scanner chủ động + Dynamic Trash Spawn) — tạo vách đá độ phức tạp khiến người chơi 10-12 tuổi dễ bỏ cuộc.

**Giải pháp:** Chia C2 thành 3 phase tuần tự, mỗi phase mở khóa 1-2 hệ thống, có thời gian thực hành trước khi phase tiếp theo.

### Phase 2A: "Làm quen Scanner" (3–4 phút)

**Mở khóa:** Eco Scanner chủ động  
**Chưa mở:** Inventory limit (vẫn auto-disappear như C1), Sorting system, Dynamic spawn

**Flow:**
```
Bác Xanh:
💬 "Máy quét sẽ cho cháu thấy những điểm ô nhiễm mà mắt thường không thấy.
    Đi về phía công viên đi — máy sẽ tự đổi màu khi cháu đến gần."

Objective 1: Dùng Scanner tìm Hotspot đầu tiên (Picnic Area, cam)
  → Đi bộ đến công viên
  → Bật Scanner (Q) — thấy marker cam đầu tiên
  → Đến gần marker → UI hotspot info hiện lên (như GDD line 352-360)
  → Scanner tutorial popup: "Màu cam = ô nhiễm trung bình. Màu đỏ = nghiêm trọng."
  → Nhặt 3-4 món rác trong bán kính hotspot (rác vẫn auto-disappear, không vào inventory)

Hoàn thành → Bác Xanh khen:
💬 "Tốt lắm! Cháu thấy chưa — có những chỗ bẩn hơn mắt thường thấy."
```

**Kết thúc Phase 2A:** Người chơi hiểu Scanner, biết màu marker, đã thấy 1 hotspot.

---

### Phase 2B: "Học phân loại" (4–5 phút)

**Mở khóa:** Inventory 5 ô + Sorting system  
**Chưa mở:** Dynamic spawn  
**Giữ lại:** Scanner

**Flow:**
```
Bác Xanh:
💬 "Giờ cháu đã biết tìm rác ở đâu. Nhưng nhặt lên rồi — vứt đi đâu?
    Mỗi loại rác cần được xử lý khác nhau. Bác sẽ chỉ cho cháu."

→ Dẫn người chơi đến Trung tâm Tái chế (Bác Xanh đi trước, người chơi follow)

Tại Trung tâm Tái chế:
  → Inventory limit kích hoạt (5 ô) — tutorial popup nhỏ: "Túi của cháu chứa được 5 món"
  → Bác Xanh đưa 3 món rác mẫu (1 hữu cơ, 1 tái chế, 1 vô cơ)
  → Mở Sorting UI — highlight đúng thùng cho từng món (1 giây delay như GDD line 568)
  → Mỗi lần đúng: feedback + giải thích ngắn

Sau khi sort xong 3 món mẫu:
💬 "Giờ cháu thử tự tìm và phân loại nhé. Ra công viên nhặt thêm 3-4 món rồi quay lại đây."

Objective 2: Tự nhặt rác ở Picnic Area → inventory đầy → quay lại Trung tâm → tự sort
  → Lần đầu mỗi loại rác MỚI (chưa gặp trong tutorial): vẫn auto-highlight 1 giây
  → Từ lần 2: tự chọn
```

**Kết thúc Phase 2B:** Người chơi đã sort ít nhất 6-7 món, hiểu 4 loại rác, quen với inventory.

---

### Phase 2C: "Đối mặt thực tế" (4–5 phút)

**Mở khóa:** Full 3 hotspot requirement + Dynamic Trash Spawn  
**Giữ lại:** Tất cả hệ thống phase trước

**Flow:**
```
Scanner cập nhật: hiện 2 marker mới (Residential Street vàng/cam, Drainage đỏ)
Bác Xanh:
💬 "Còn 2 điểm ô nhiễm nữa. Và cháu nên biết — rác sẽ không đứng yên mãi.
    Ở những nơi người dân chưa ý thức, rác sẽ xuất hiện trở lại."

Objective 3: Tìm và dọn sạch cả 3 hotspot
  → Residential Street (vàng/cam)
  → Drainage (đỏ) — drainage không cần thông ngay, chỉ nhặt rác xung quanh
  → Picnic Area (đã dọn trước đó — nhưng giờ rác ĐÃ quay lại một ít!)

  → Khi thấy rác quay lại ở công viên:
  💬 "Cháu thấy không? Rác đã quay lại. Dọn mà không ngăn nguyên nhân thì sẽ phải dọn mãi."

→ Dynamic spawn chính thức active trên toàn bản đồ
→ Inventory loop đầy đủ: nhặt → đầy → về tái chế → sort → quay lại

Chapter 2 hoàn thành: mở Chapter 3
```

### Tổng thời gian C2 mới: ~11–14 phút (giữ nguyên 10-15 phút)

### Bảng so sánh C2 cũ vs mới

| Tiêu chí | C2 cũ | C2 mới (3 phase) |
|----------|-------|-----------------|
| Số hệ thống kích hoạt cùng lúc | 4 | 1-2 mỗi phase |
| Có tutorial sorting? | Chỉ highlight lần đầu | Có 3 món mẫu + Bác Xanh hướng dẫn trực tiếp |
| Khi nào dynamic spawn bắt đầu? | Ngay đầu C2 | Cuối C2, sau khi người chơi đã hiểu hệ thống |
| Cảm giác "bị úp" | Có | Không — mỗi phase là một bước nhỏ |
| Lần đầu thấy rác quay lại | Sau khi đã dọn hết → shock | Trong phase 2C, có context từ 2 phase trước |

---

## THAY ĐỔI #2: VIẾT LẠI LỜI THOẠI BÁC XANH

**Vấn đề:** Bác Xanh hiện tại là "quest kiosk biết nói" — không tự giới thiệu, không
khen người chơi, chỉ thuyết giảng. Chapter 1 thiếu kết nối cảm xúc trầm trọng.

**Giải pháp:** Viết lại toàn bộ hội thoại Bác Xanh trong Chapter 1 với 3 nguyên tắc:
1. Tự giới thiệu bản thân (tên, vai trò, lịch sử với thị trấn)
2. Công nhận hành động của người chơi (khen đã dọn quảng trường)
3. Tạo mục đích lớn hơn trước khi trao Scanner (gọi người chơi vào sứ mệnh)

---

### Hội thoại mới — Chapter 1

**Bối cảnh:** Người chơi vừa dọn 8 món rác, đường mở, bước đến gần Bác Xanh.
Bác Xanh đang đứng cạnh đài phun nước khô ở quảng trường.

```
[Bác Xanh quay lại, mỉm cười]

BÁC XANH:
"Chà! Cháu là tình nguyện viên mới mà hội đồng thị trấn gửi đến phải không?
 Bác là Bác Xanh — bác đã sống ở thị trấn Ven Sông này từ hồi nó còn xanh mướt,
 chim hót đầy công viên, cá bơi đầy sông..."

[Nhìn quanh quảng trường]

"Giờ thì nhìn quanh đi — xám xịt, rác ngập đường. Mà cháu vừa dọn sạch
 cả quảng trường một mình đấy! Nhanh thật! Cảm ơn cháu."

[Giọng trầm xuống]

"Nhưng bác phải nói thật với cháu: rác sạch hôm nay, ngày mai lại đầy.
 Không phải tại cháu đâu — mà tại mấy cái cống bị tắc đằng kia,
 tại mấy người dân chưa hiểu rác của họ đi đâu về đâu.
 Dọn rác là bước đầu — nhưng chỉ là bước đầu thôi."

[Rút Eco Scanner ra, đưa về phía người chơi]

"Bác có cái này — Máy Quét Sinh Thái. Nó sẽ cho cháu thấy những thứ
 mắt thường không thấy: chỗ nào ô nhiễm nặng nhất, nguyên nhân từ đâu.
 Hồi xưa bác dùng nó để giữ cho thị trấn luôn xanh. Giờ đến lượt cháu.

 Cháu muốn thử không?"

[Người chơi nhận Scanner — hiệu ứng UI: màn hình flash xanh nhẹ,
 Scanner xuất hiện trong tay nhân vật, icon Q hiện ở góc]

BÁC XANH:
"Bấm Q để bật máy quét. Đi về phía công viên đằng kia đi —
 máy sẽ đổi màu khi cháu đến gần điểm ô nhiễm.
 Có gì không hiểu thì quay lại đây, bác luôn ở quảng trường này."
```

### Phân tích cải thiện

| Yếu tố | Cũ | Mới |
|--------|-----|-----|
| Tự giới thiệu | ❌ Không có | ✅ "Bác là Bác Xanh — bác đã sống ở thị trấn Ven Sông này từ hồi nó còn xanh mướt" |
| Công nhận người chơi | ❌ Không có | ✅ "Cháu vừa dọn sạch cả quảng trường một mình đấy! Nhanh thật! Cảm ơn cháu." |
| Tên thị trấn | ❌ Không có | ✅ "Thị trấn Ven Sông" |
| Lịch sử + lý do có Scanner | ❌ Không giải thích | ✅ "Hồi xưa bác dùng nó để giữ cho thị trấn luôn xanh. Giờ đến lượt cháu." |
| Scanner là quà tặng hay giao dịch? | Giao dịch | ✅ Quà tặng — "Cháu muốn thử không?" (tạo micro-choice) |
| Người chơi được gọi vào sứ mệnh? | ❌ Không | ✅ "Giờ đến lượt cháu" — người chơi là người được chọn |
| Có hướng dẫn sau khi nhận Scanner? | ❌ Chapter kết thúc ngay | ✅ "Đi về phía công viên... máy sẽ đổi màu" — C1 nối tiếp vào C2 Phase 2A |
| Số câu / độ dài | 4 câu gộp 1 đoạn | 7 đoạn hội thoại, mỗi đoạn 1-2 câu |
| Cảm xúc | Trung tính, thuyết giáo | Ấm áp, biết ơn, trao niềm tin |

---

## THAY ĐỔI #3: HIỆU ỨNG SPILL KHI PHÂN LOẠI SAI

**Vấn đề:** Phân loại sai hiện tại không có hậu quả gì trong thế giới game — người chơi
có thể brute-force đoán mò đến khi đúng. Điều này phá vỡ Pillar 1 (Nhân quả rõ ràng).

**Giải pháp:** Khi phân loại sai, spawn một hiệu ứng "spill" nhỏ tại chỗ —
thấy được, sửa được trong 2 giây, không phạt điểm, nhưng tạo nhân quả thực tế.

---

### Cơ chế Spill

```
┌─────────────────────────────────────────────────┐
│  Khi người chơi chọn sai thùng:                  │
│                                                   │
│  1. UI feedback văn bản (giữ nguyên GDD):         │
│     ❌ "Chưa đúng. Pin cũ chứa hóa chất độc hại,  │
│         phải xử lý đặc biệt..."                   │
│                                                   │
│  2. HIỆU ỨNG SPILL (MỚI):                        │
│     - Rác trong UI "rơi ra" khỏi thùng sai        │
│     - Xuất hiện một vệt bẩn nhỏ trên mặt đất      │
│       (decal tròn, bán kính ~2 studs, màu tùy      │
│       loại rác: nâu/vàng/xám/đỏ)                  │
│     - Particle nhỏ (3-5 hạt) rơi xuống             │
│     - Âm thanh "tách" nhẹ                          │
│     - Thời gian: 0.5 giây animation               │
│                                                   │
│  3. TƯƠNG TÁC DỌN SPILL (MỚI):                   │
│     - Prompt hiện trên vệt bẩn: [E] Dọn sạch      │
│     - Giữ E 1 giây → vệt bẩn biến mất             │
│     - CÓ THỂ dọn NGAY LẬP TỨC hoặc để lại         │
│     - Nếu KHÔNG dọn: vệt bẩn tồn tại, không ảnh   │
│       hưởng đến chỉ số, nhưng tích tụ visual       │
│       → sau 3+ vệt bẩn: Bác Xanh có thoại nhắc    │
│                                                   │
│  4. SAU KHI DỌN SPILL (hoặc không):               │
│     - Sorting UI mở lại ngay                      │
│     - Người chơi chọn lại thùng đúng               │
│     - Khi chọn đúng: hiệu ứng "đúng" như cũ +      │
│       tất cả vệt bẩn còn lại TỰ ĐỘNG biến mất     │
│       (cảm giác "cuối cùng cũng đúng")            │
│                                                   │
│  ĐIỂM:                                            │
│  - Sai: 0 điểm (không đổi so với cũ)              │
│  - Dọn spill: KHÔNG được điểm                     │
│  - Đúng: +2 ES, -2 PL (giữ nguyên)                │
│  - Sort đúng rác độc hại: +4 ES, -4 PL (giữ nguyên)│
└─────────────────────────────────────────────────┘
```

### Quy tắc tích tụ spill

| Số vệt bẩn trong Trung tâm | Hiệu ứng |
|---|---|
| 1-2 | Không có gì — bình thường |
| 3-4 | Bác Xanh (nếu đang ở gần): 💬 "Cẩn thận cháu nhé, phân loại sai sẽ làm bẩn cả khu tái chế." |
| 5+ | Visual Trung tâm Tái chế hơi xám đi một chút (nhưng không ảnh hưởng gameplay) |

**Reset:** Tất cả vệt bẩn tự động biến mất khi:
- Người chơi rời Trung tâm Tái chế > 30 giây
- Hoặc khi sort đúng liên tiếp 3 lần (streak bonus — dọn sạch tự động)

### Phân tích tác động

| Yếu tố | Trước (v2) | Sau (v3) |
|--------|-----------|----------|
| Có hậu quả khi sai? | Không | Có — visual, thấy được |
| Có phạt điểm không? | Không | Không (giữ nguyên) |
| Có cản trở thử lại không? | Không | Mất 1 giây dọn spill — đủ để tạo "tôi không muốn sai nữa" |
| Giáo dục qua feedback? | Chỉ đọc text | Đọc text + thấy hậu quả + tự sửa |
| Phù hợp Pillar 1 (nhân quả)? | ❌ Yếu | ✅ Mạnh — sai = bẩn, đúng = sạch |
| Có gây frustration không? | — | Không — dọn spill mất 1 giây, không phạt điểm |
| Dev cost (Roblox) | — | 1 decal + 1 particle + 1 short audio + 1 prompt |
| Có phù hợp "không dead end"? | — | ✅ Spill không chặn tiến trình, có thể bỏ qua |

---

## TÓM TẮT IMPACT

| Thay đổi | Audit nguồn | Vấn đề giải quyết | Dev cost | Priority |
|----------|------------|-------------------|----------|----------|
| #1: C2 3-phase | Flow | Vách đá độ phức tạp C1→C2 | Trung bình (reflow logic) | **P0** |
| #2: Bác Xanh dialogue | FTUE | Thiếu hook cảm xúc, mentor yếu | Thấp (text only) | **P0** |
| #3: Spill effect | Failure Loop | Phân loại sai vô nghĩa | Thấp (1 decal + 1 SFX) | **P1** |
