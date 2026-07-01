# GREEN AGAIN v3 — FRICTION JOURNEY AUDIT

> **Ngày:** Tháng 6/2026  
> **Audit target:** Toàn bộ 5 Chapter, từ spawn đến ending, qua 6 khu vực bản đồ  
> **Player segment:** 10-16 tuổi, lần đầu chơi

---

## Journey Breakdown

### Chapter 1: Khởi đầu (5-8 phút)
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Spawn | Xuất hiện ở Quảng trường | — |
| 2 | Nhặt rác tutorial | Nhặt 8 món rác chặn đường quanh Quảng trường | Nội bộ Quảng trường |
| 3 | Gặp Bác Xanh | Hội thoại 7 đoạn, nhận Scanner | Đứng tại chỗ |
| 4 | C1 kết thúc | Scanner active, UI 3 chỉ số hiện | — |

**Số trip về RC:** 0 (rác auto-disappear)

### Chapter 2A: Làm quen Scanner (3-4 phút)
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nghe hướng dẫn | Bác Xanh bảo đi về phía công viên | — |
| 2 | Đi đến Picnic Area | Đi bộ Quảng trường → Công viên | Trip 1: SQ → Park |
| 3 | Bật Scanner | Q, thấy marker cam | Tại chỗ |
| 4 | Nhặt rác hotspot | 3-4 món, vẫn auto-disappear | Nội bộ Park |
| 5 | Kết thúc 2A | Bác Xanh khen | — |

### Chapter 2B: Học phân loại (4-5 phút)
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nghe hướng dẫn | Bác Xanh dẫn đến RC | Trip 2: Park → SQ → RC (follow NPC) |
| 2 | Tutorial sorting | 3 món mẫu với Bác Xanh | Tại RC |
| 3 | Quay lại công viên nhặt rác | Tự nhặt 3-4 món | Trip 3: RC → Park |
| 4 | Quay lại RC sort | Inventory đầy → về sort | Trip 4: Park → RC |
| 5 | Kết thúc 2B | Đã sort 6-7 món | — |

### Chapter 2C: Đối mặt thực tế (4-5 phút)
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Scanner cập nhật | 2 marker mới: Residential, Drainage | — |
| 2 | Bác Xanh dẫn đến Drainage | Follow NPC đến cống | Trip 5: RC → Drainage |
| 3 | Nhặt rác Residential Street | Tự tìm, nhặt rác | Trip 6: Drainage → Residential |
| 4 | Về RC sort (nếu đầy) | Inventory loop | Trip 7: Residential → RC |
| 5 | Quay lại Picnic Area | Thấy rác đã quay lại | Trip 8: RC → Park |
| 6 | Kết thúc C2 | Dynamic spawn active | — |

### Chapter 3: Ngăn rác quay lại (10-15 phút) — Spatial Circuit
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nhận vật phẩm | 3 thùng rác + 2 biển báo từ Bác Xanh tại SQ | — |
| 2 | Khu dân cư | Đặt thùng rác + nhặt rác | Trip 9: SQ → Residential |
| 3 | Cống thoát nước | Nhặt 5-7 món + thông cống | Trip 10: Residential → Drainage |
| 4 | Bờ sông | Đặt 2 biển báo | Trip 11: Drainage → Riverside |
| 5 | Công viên | Đặt thùng rác + nhặt rác | Trip 12: Riverside → Park |
| 6 | Về RC sort | Sort toàn bộ inventory | Trip 13: Park → RC |
| 7 | Kết thúc C3 | Hoàn thành circuit | — |

### Chapter 4: Cứu sinh vật (10-15 phút)
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Scanner tín hiệu mới | 3 marker động vật | — |
| 2 | Cứu chim (Park) | Nhặt rác nhựa 15 studs → sort → cứu | Trip 14: SQ → Park |
| 3 | Về RC sort rác nhựa | — | Trip 15: Park → RC |
| 4 | Cứu cá (Riverside) | Kiểm tra điều kiện → cứu (hoặc bị gate) | Trip 16: RC → Riverside |
| 5 | Nếu bị gate → thông cống | Quay lại Drainage | Trip 17: Riverside → Drainage |
| 6 | Cứu sóc (Residential) | Nhặt rác độc hại → sort → cứu | Trip 18: Drainage → Residential |
| 7 | Về RC sort rác độc hại | — | Trip 19: Residential → RC |
| 8 | Kết thúc C4 | 3 con đã cứu | — |

### Chapter 5: Cộng đồng và kết thúc (10-15 phút)
| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nghe Bác Xanh | Hội thoại mở đầu C5 | SQ |
| 2 | Thuyết phục Cô Tư | Residential | Trip 20: SQ → Residential |
| 3 | Thuyết phục Anh Tùng | Park | Trip 21: Residential → Park |
| 4 | Thuyết phục Ông Sáu | Riverside | Trip 22: Park → Riverside |
| 5 | Trồng 3 cây | Rải rác ở 3 khu | Nội bộ các khu |
| 6 | Gặp Bác Xanh | Về SQ | Trip 23: Riverside → SQ |
| 7 | Ending cutscene | UI tổng kết | — |

---

## Friction Map

| Step | Friction Point | Type | Cause | Intensity | Visibility | Fairness |
|------|---------------|------|-------|-----------|------------|----------|
| C1→C2A | Đi bộ SQ→Park lần đầu | Mixed | Người chơi chưa quen bản đồ, chưa có minimap | Low | Partially hidden | Fair |
| C2B T3 | Park→RC→Park→RC (2 vòng) | **Harmful** | Backtrack lặp: đi RC học → về Park nhặt → lại về RC sort | **Medium** | Obvious | Borderline |
| C2C T2 | RC→Drainage (follow NPC) | Productive | Bác Xanh dẫn đường cho hotspot nguy hiểm nhất | Low | Obvious | Fair |
| C2C T5 | Về Park thấy rác quay lại | **Productive** | Shock có chủ đích — "dọn mà không ngăn = dọn mãi" | Low | Obvious | Fair |
| C3 Circuit | 4 zone liên tiếp trước khi về RC | Mixed | Inventory 5 ô có thể đầy giữa circuit → phải về RC sớm → gãy circuit | **Medium** | Partially hidden | Borderline |
| C3→C4 | Cứu cá bị gate nếu chưa thông cống | **Productive** | Environmental gating — nhân quả rõ ràng | Medium | Obvious | Fair |
| C4 multi | Park→RC→Riverside→(Drainage)→Residential→RC | **Harmful** | 3 con vật ở 3 góc map, mỗi con cần RC trip để sort rác đặc thù | **High** | Obvious | Borderline |
| C5 NPC | Residential→Park→Riverside (3 NPC) | Mixed | Spatial circuit hợp lý nhưng 3 hội thoại dài + context clue = cognitive load | Medium | Obvious | Fair |
| C5 End | Riverside→SQ (xa nhất) | Mixed | Trip cuối cùng dài nhất nếu đang ở Riverside | Low | Obvious | Fair |
| **Toàn game** | **Tổng ~23 trip, ~8-10 lần về RC** | **Mixed** | RC là hub bắt buộc của inventory loop | Medium | Obvious | Fair |

---

## Accumulation Analysis

### Vùng tích tụ #1: C2B — Backtrack kép
```
Park → RC (học sort) → Park (nhặt rác) → RC (sort)
```
- **Stack:** 2 vòng Park↔RC liên tiếp trong 4-5 phút
- **Tác động:** Người chơi 10-12 tuổi đi bộ 4 trip liên tục, chưa có dynamic spawn để tạo variety
- **Đã giảm nhẹ bởi v3:** Bác Xanh dẫn đường trip đầu, RC ở trung tâm → khoảng cách ngắn hơn

### Vùng tích tụ #2: C3 Circuit — Inventory đầy giữa đường
```
SQ → Residential → Drainage → Riverside → Park → RC
```
- **Stack:** 5 zone trong 1 circuit, inventory 5 ô, mỗi zone sinh 3-7 món rác
- **Nguy cơ:** Inventory đầy ở Drainage → buộc về RC → circuit gãy → quay lại Drainage → tăng 2 trip
- **Tác động:** Circuit lý thuyết 5 bước có thể thành 7-8 bước nếu inventory management kém
- **Đã giảm nhẹ bởi v3:** "Không cần về RC trước khi thông cống", nhưng rác vẫn cần sort

### Vùng tích tụ #3: C4 — 3 cứu hộ = 3 RC trip
```
Park(chim) → RC → Riverside(cá) → [Drainage nếu bị gate] → Residential(sóc) → RC
```
- **Stack:** Mỗi con vật yêu cầu: đến zone → nhặt rác đặc thù → về RC sort → quay lại zone → cứu
- **Worst case:** Cá bị gate → thêm trip Drainage → tổng có thể 6-7 trip
- **Tác động:** Backtrack fatigue ở phút 35-50 của game
- **Chưa có mitigation trong v3**

### Vùng tích tụ #4: Toàn game — Snowball timer
- **Tổng ~23 trip di chuyển** trong ~55-70 phút
- Trung bình mỗi 2.5-3 phút có 1 trip di chuyển
- Trip dài nhất: Riverside ↔ Residential (~350 studs)
- **Người chơi 10 tuổi:** Attention span ~15-20 phút — game dài 55-70 phút cần checkpoint/pause point rõ ràng

---

## Breakpoints

| # | Vị trí | Chuyển từ... | Sang... | Tại sao gãy |
|---|--------|-------------|---------|-------------|
| 1 | **C2B, lần 2 về RC** | Học thú vị | Backtrack mệt | Vừa mới học sort xong, chưa kịp apply đã phải đi bộ về Park rồi lại về RC |
| 2 | **C3, giữa circuit** | Flow mượt | Gãy circuit | Inventory đầy giữa Drainage/Riverside → phải về RC → mất đà |
| 3 | **C4, sau con thứ 2** | Hứng thú cứu | Mệt mỏi lặp | Pattern "đến→nhặt→về RC→quay lại→cứu" lặp 3 lần với 3 góc map |
| 4 | **C5, từ Riverside về SQ** | Cao trào | Đi bộ dài | Trip cuối cùng dài nhất, ngay trước ending — giảm emotional momentum |

---

## Diagnosis

### Friction nào là cốt lõi, nên giữ?
1. **Inventory limit 5 ô → buộc về RC** — Đây là trụ cột của gameplay loop. Không có nó, sorting system vô nghĩa. **GIỮ.**
2. **Environmental gating (cá cần cống sạch)** — Nhân quả rõ ràng, Pillar 1. **GIỮ.**
3. **Dynamic spawn → rác quay lại** — Shock giáo dục có chủ đích. **GIỮ.**
4. **C3 spatial circuit** — Tổ chức objectives theo vòng tròn địa lý là thiết kế tốt. **GIỮ.**

### Friction nào đang gây hại?
1. **C2B backtrack kép (Park↔RC×2)** — Vừa học vừa đi bộ 4 trip trong 4 phút. Trip thứ 2 (tự đi nhặt rồi về sort) có thể gộp.
2. **C4: 3 RC trip riêng biệt** — Mỗi con vật cần sort rác đặc thù TRƯỚC KHI cứu. Có thể gộp rác từ 2-3 con vào 1 trip RC.
3. **Không có fast-travel hoặc movement boost** — Sau C3, đi bộ giữa các zone không còn tính khám phá, chỉ còn là thủ tục.

### Friction nào đang ở mức chấp nhận được?
1. **C1→C2A đi bộ lần đầu** — Khám phá, hợp lý.
2. **Bác Xanh dẫn đường C2B, C2C** — Follow NPC giảm cognitive load, không tính là friction.
3. **C5 NPC circuit** — 3 hội thoại ở 3 zone, nhưng không cần về RC, không có inventory pressure.

---

## Recommendations

### 1. Gộp C2B trip 3+4 thành 1 trip
**Issue:** Sau khi học sort 3 món mẫu, phải đi Park nhặt rồi về RC sort — 2 trip lặp.  
**Change:** Spawn 2-3 món rác NGAY trong/ngoài RC để người chơi nhặt và sort luôn — không cần về Park.  
**Expected effect:** Tiết kiệm 1 trip Park↔RC. Vẫn có trải nghiệm "tự nhặt → tự sort". Park trip vẫn xảy ra ở C2C.  
**Priority:** P1 | **Dev cost:** Thấp

### 2. C4: Cho phép gom rác 2-3 con trước khi về RC
**Issue:** 3 RC trip riêng biệt cho 3 con vật — lặp pattern mệt mỏi.  
**Change:** Cho phép người chơi nhặt rác ở Park (chim), Riverside (cá), Residential (sóc) — tất cả trước khi về RC. Khi về RC, sort tất cả một lần. Tăng inventory lên 8 ô tạm thời trong C4, hoặc cho rác cứu hộ vào "túi phụ".  
**Expected effect:** Tiết kiệm 1-2 trip RC.  
**Priority:** P1 | **Dev cost:** Trung bình

### 3. Thêm "shortcut path" mở sau C3
**Issue:** Không có fast-travel hoặc movement boost late game.  
**Change:** Sau khi thông cống (C3), mở cầu gỗ nối Residential ↔ Riverside, và đường mòn sau RC nối thẳng RC → Park.  
**Expected effect:** Giảm ~15-20% thời gian di chuyển từ C4 trở đi. Phù hợp narrative.  
**Priority:** P2 | **Dev cost:** Trung bình

### 4. C3 Circuit: Cảnh báo sớm khi inventory sắp đầy
**Issue:** Inventory đầy giữa circuit → circuit gãy.  
**Change:** Khi ở đầu C3 circuit (Residential), nếu inventory đạt 3/5 — hiện tooltip: "Còn 2 chỗ trống. Cân nhắc nhặt ít hơn để khỏi về RC giữa chừng."  
**Expected effect:** Người chơi có quyền chọn: nhặt ít giữ circuit, hoặc nhặt nhiều chấp nhận về RC.  
**Priority:** P2 | **Dev cost:** Thấp

### 5. Thêm checkpoint/pause point rõ ràng giữa các Chapter
**Issue:** 55-70 phút không có natural stopping point cho trẻ 10-12 tuổi.  
**Change:** Cuối mỗi Chapter, Bác Xanh nói 1 câu như "Ngày mai cháu quay lại nhé" — tạo psychological chapter break.  
**Expected effect:** Người chơi có thể tự ngừng mà không cảm thấy "đang dở". Giảm drop rate.  
**Priority:** P3 | **Dev cost:** Thấp

---

## Tổng kết Impact

| # | Khuyến nghị | Trip tiết kiệm | Dev cost | Priority |
|---|------------|---------------|----------|----------|
| 1 | Gộp C2B trip 3+4 | 1 trip | Thấp (spawn rác gần RC) | **P1** |
| 2 | C4 gom rác đa con | 1-2 trip | Trung bình (inventory exception) | **P1** |
| 3 | Shortcut path sau C3 | 0 trip, giảm ~20% walk time | Trung bình (2-3 path mới) | **P2** |
| 4 | Cảnh báo inventory sớm C3 | 0-2 trip (người chơi tự chọn) | Thấp (UI text) | **P2** |
| 5 | Chapter break narrative | 0 trip | Thấp (1 câu thoại) | **P3** |

---

*GREEN AGAIN v3 — Friction Journey Audit — Tháng 6/2026*
