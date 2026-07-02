# GREEN AGAIN v4 — FRICTION JOURNEY AUDIT (MAP KIỂU VIỆT NAM)

> **Ngày:** Tháng 6/2026
> **Audit target:** Toàn bộ 5 Chapter với bản đồ v4 mới (Sông uốn lượn Bắc→Đông Nam, Đập 3 cống, Đường trục chính Y~50%)
> **Player segment:** 10-16 tuổi, lần đầu chơi
> **So sánh với:** Friction Audit v3

---

## Audit Target

- **Journey:** Toàn bộ trải nghiệm di chuyển từ Spawn → 5 Chapter → Ending (~55-70 phút)
- **Expected player goal:** Dọn sạch thị trấn, xử lý nguyên nhân, cứu động vật, thuyết phục người dân
- **Player context:** 10-16 tuổi, lần đầu chơi game giáo dục, chưa quen bản đồ
- **Map version:** v4 — kiểu Việt Nam (sông uốn lượn, đập 3 cống, rừng bao quanh, đường trục chính)

---

## Journey Breakdown

### Chapter 1: Khởi đầu (5-8 phút)

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Spawn | Xuất hiện ở góc dưới trái (x=10%, y=60%) | — |
| 2 | Đi dọc đường dưới | Thấy rác rải rác trên đường, men theo rừng trái | Trip 1: Spawn → dọc đường dưới |
| 3 | Nhặt rác trên đường | Nhặt 3-4 món rác dọc đường (auto-disappear) | Dọc đường dưới |
| 4 | Đến Nhà văn hóa | Thấy tòa nhà mái ngói đỏ, gặp Bác Xanh | Trip 1 tiếp: đến Nhà văn hóa |
| 5 | Hội thoại + nhận Scanner | Bác Xanh nói 7 đoạn, trao Scanner | Tại Nhà văn hóa |
| 6 | C1 kết thúc | Scanner active, UI 3 chỉ số hiện | — |

**Số trip:** 1 | **Về RC:** 0

> ⚠️ **Khác v3:** Spawn không ở cùng chỗ Bác Xanh. Người chơi phải đi bộ từ góc dưới trái đến Nhà văn hóa (~80 studs). Đây là trip đầu tiên có chủ đích — "người lạ đi vào làng."

---

### Chapter 2A: Làm quen Scanner (3-4 phút)

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nghe hướng dẫn | Bác Xanh bảo đi về phía công viên | — |
| 2 | Đi đến Công viên | Men đường trục chính lên Bắc → rẽ vào Công viên | Trip 2: Nhà văn hóa → Công viên |
| 3 | Bật Scanner | Q, thấy marker cam Picnic Area | Tại chỗ |
| 4 | Nhặt rác hotspot | 3-4 món, auto-disappear | Nội bộ Công viên |
| 5 | Kết thúc 2A | Bác Xanh khen (qua UI hoặc quay về) | — |

**Số trip:** 1 | **Về RC:** 0

> ⚠️ **Khác v3:** Trip dài hơn v3 (Nhà văn hóa→Công viên ~160 studs vs v3 SQ→Park ~80 studs). Người chơi phải băng qua đường trục chính — đây là lần đầu thấy toàn cảnh map.

---

### Chapter 2B: Học phân loại (4-5 phút)

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Bác Xanh dẫn đến RC | Follow NPC từ Công viên → Nhà văn hóa/RC | Trip 3: Park → Nhà văn hóa (follow) |
| 2 | Tutorial sorting | 3 món mẫu với Bác Xanh tại RC | Tại RC |
| 3 | Quay lại Công viên nhặt rác | Tự nhặt 3-4 món | Trip 4: RC → Công viên |
| 4 | Quay lại RC sort | Inventory đầy → về sort | Trip 5: Công viên → RC |
| 5 | Kết thúc 2B | Đã sort 6-7 món | — |

**Số trip:** 2 (+ follow) | **Về RC:** 1

> ⚠️ **Khác v3:** RC cách Công viên ~100 studs (ngắn hơn v3), nhưng Bác Xanh phải đi từ Nhà văn hóa ra Công viên rồi dẫn về — thêm 1 đoạn follow dài hơn.

---

### Chapter 2C: Đối mặt thực tế (4-5 phút)

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Scanner cập nhật | 2 marker mới: Residential (NW), Dam (SE) | — |
| 2 | Bác Xanh dẫn đến Đập | Follow NPC từ RC → Đập | Trip 6: RC → Đập (follow) |
| 3 | Nhặt rác Khu dân cư | Tự tìm, nhặt rác Residential St. | Trip 7: Đập → Khu dân cư |
| 4 | Về RC sort (nếu đầy) | Inventory loop | Trip 8: Khu dân cư → RC |
| 5 | Quay lại Công viên | Thấy rác đã quay lại | Trip 9: RC → Công viên |
| 6 | Kết thúc C2 | Dynamic spawn active | — |

**Số trip:** 4 | **Về RC:** 1-2

> ⚠️ **Khác v3:** Trip 7 (Đập→Khu dân cư) là cross-map NW←SE (~300+ studs) — dài hơn v3 đáng kể. Bù lại, Trip 6 (RC→Đập) rất ngắn (~120 studs).

---

### Chapter 3: Ngăn rác quay lại (10-15 phút) — Spatial Circuit v4

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nhận vật phẩm | 3 thùng rác + 2 biển báo từ Bác Xanh tại Nhà văn hóa | — |
| 2 | Khu dân cư | Đặt thùng rác + nhặt rác | Trip 10: Nhà văn hóa → Khu dân cư |
| 3 | Nhà cô Tư | Đặt biển báo gần tiệm (đi ngang) | Trip 11: Khu dân cư → Nhà cô Tư (ngắn) |
| 4 | Công viên | Đặt thùng rác + nhặt rác | Trip 12: Nhà cô Tư → Công viên |
| 5 | Bờ sông NE (Ông Sáu) | Đặt biển báo | Trip 13: Công viên → Bờ sông NE |
| 6 | Đập nước | Nhặt rác quanh Cống 1 + thông cống 1 | Trip 14: Bờ sông NE → Đập |
| 7 | Về RC sort | Sort toàn bộ inventory | Trip 15: Đập → RC |
| 8 | Kết thúc C3 | Hoàn thành circuit | — |

**Số trip:** 6-7 | **Về RC:** 1 (cuối circuit)

> ⚠️ **Khác v3:** Circuit dài hơn v3 (7 steps vs 6), nhưng flow tự nhiên hơn: theo chiều kim đồng hồ từ NW→N→NE→SE. Không còn zig-zag như v3. Trip 14 (Bờ sông NE→Đập) có thể dài (~200 studs dọc sông).

---

### Chapter 4: Cứu sinh vật (10-15 phút)

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Scanner tín hiệu mới | 3 marker động vật | — |
| 2 | Cứu chim (Công viên) | Nhặt rác nhựa 15 studs → sort → cứu | Trip 16: Nhà văn hóa → Công viên |
| 3 | Về RC sort rác nhựa | — | Trip 17: Công viên → RC |
| 4 | Cứu cá (Đập nước) | Kiểm tra 2/3 cống đã thông → cứu (hoặc bị gate) | Trip 18: RC → Đập |
| 5 | Nếu bị gate → thông cống 2,3 | Ở lại Đập thông thêm cống | Tại Đập |
| 6 | Cứu sóc (Khu dân cư) | Nhặt rác độc hại → sort → cứu | Trip 19: Đập → Khu dân cư |
| 7 | Về RC sort rác độc hại | — | Trip 20: Khu dân cư → RC |
| 8 | Kết thúc C4 | 3 con đã cứu | — |

**Số trip:** 5-6 | **Về RC:** 2-3

> ⚠️ **Khác v3:** Cứu cá giờ ở Đập (SE) thay vì Riverside (giữa-phải). Trip 19 (Đập→Khu dân cư) là cross-map dài nhất (~380 studs). Bù lại, nếu bị gate cá, người chơi ĐÃ Ở SẴN Đập — không cần đi đâu để thông cống thêm.

---

### Chapter 5: Cộng đồng và kết thúc (10-15 phút)

| # | Bước | Hành động | Di chuyển |
|---|------|-----------|-----------|
| 1 | Nghe Bác Xanh | Hội thoại mở đầu C5 tại Nhà văn hóa | Tại Nhà văn hóa |
| 2 | Thuyết phục Cô Tư | Khu dân cư → Nhà cô Tư | Trip 21: Nhà văn hóa → Khu dân cư → Nhà cô Tư |
| 3 | Thuyết phục Anh Tùng | Công viên | Trip 22: Nhà cô Tư → Công viên (ngắn) |
| 4 | Thuyết phục Ông Sáu | Bờ sông NE | Trip 23: Công viên → Bờ sông NE |
| 5 | Trồng cây | Rải rác ở các khu | Nội bộ các khu |
| 6 | Gặp Bác Xanh | Về Nhà văn hóa | Trip 24: Bờ sông NE → Nhà văn hóa |
| 7 | Ending | UI tổng kết tại Nhà văn hóa | — |

**Số trip:** 4-5 | **Về RC:** 0

> ⚠️ **Khác v3:** NPC circuit gọn hơn: Cô Tư (N) → Anh Tùng (NE) → Ông Sáu (NE) — 2 NPC cuối gần nhau. Trip cuối (Bờ sông NE→Nhà văn hóa) ~180 studs — không còn là trip dài nhất game như v3 (Riverside→SQ ~350 studs). Ending ở Nhà văn hóa thay vì Quảng trường.

---

## Friction Map

| Step | Friction Point | Type | Cause | Intensity | Visibility | Fairness |
|------|---------------|------|-------|-----------|------------|----------|
| C1 T2 | Spawn→Nhà văn hóa lần đầu | Mixed | Người chơi chưa quen bản đồ, nhưng chỉ có 1 đường chính để đi | Low | Partially hidden | Fair |
| C1 T4 | Gặp Bác Xanh sau khi đi bộ | Productive | Cảm giác "tìm thấy nơi cần đến" — reward cho exploration | Low | Obvious | Fair |
| C2A T2 | Nhà văn hóa→Công viên (~160s) | Mixed | Trip dài gấp đôi v3, nhưng đi qua đường trục chính = thấy toàn cảnh map | Medium | Obvious | Fair |
| C2B T3 | Park→RC→Park→RC (backtrack kép) | **Harmful** | Backtrack lặp: đi RC học → về Park nhặt → lại về RC sort | **Medium** | Obvious | Borderline |
| C2C T3 | Đập→Khu dân cư cross-map | Mixed | Trip dài nhất trong C2 (~300s), nhưng là lần đầu khám phá nửa trên | Medium | Obvious | Fair |
| C2C T5 | Về Công viên thấy rác quay lại | **Productive** | Shock có chủ đích — payoff cho toàn bộ C2 | Low | Obvious | Fair |
| C3 Circuit | 6-7 zone liên tiếp trước khi về RC | Mixed | Circuit dài hơn v3 (7 steps), inventory 5 ô có thể đầy giữa chừng | **Medium** | Partially hidden | Borderline |
| C3 T6 | Bờ sông NE→Đập (~200s dọc sông) | Mixed | Trip dài, nhưng đi dọc sông = visual reward (thấy sông sạch dần) | Low | Obvious | Fair |
| C4 T2 | Công viên→RC→Đập (2 trip) | Mixed | 2 trip riêng cho cứu chim + cá, nhưng RC nằm giữa 2 điểm | Medium | Obvious | Fair |
| C4 T6 | Đập→Khu dân cư (~380s) | **Harmful** | Trip dài nhất toàn game — từ SE lên NW | **High** | Obvious | Borderline |
| C4 Gate | Cứu cá bị gate nếu <2 cống thông | **Productive** | Environmental gating — nhưng người chơi đã ở sẵn Đập | Medium | Obvious | Fair |
| C5 NPC | Nhà cô Tư→Công viên→Bờ sông NE | Mixed | 3 NPC theo thứ tự địa lý hợp lý, 2 NPC cuối gần nhau | Low | Obvious | Fair |
| C5 End | Bờ sông NE→Nhà văn hóa (~180s) | Mixed | Trip cuối, nhưng ngắn hơn nhiều so với v3 (350s) | Low | Obvious | Fair |
| **Toàn game** | **Tổng ~24-28 trip, ~5-7 lần về RC** | **Mixed** | Nhiều trip hơn v3 (~23→~26) nhưng ít về RC hơn (~8→~6) | Medium | Obvious | Fair |

---

## Accumulation Analysis

### Vùng tích tụ #1: C2B — Backtrack kép (giảm nhẹ so với v3)
```
Công viên → RC (học sort) → Công viên (nhặt rác) → RC (sort)
```
- **Stack:** 2 vòng Park↔RC trong 4-5 phút
- **Tác động v4:** Khoảng cách Công viên↔RC ~100 studs (ngắn hơn v3 ~140 studs vì RC ở SE gần Công viên NE). Backtrack vẫn tồn tại nhưng thời gian đi bộ giảm ~30%.
- **So với v3:** **Cải thiện.** V3: 4 trip dài. V4: 2 vòng ngắn hơn.

### Vùng tích tụ #2: C3 Circuit — Inventory đầy giữa đường (tệ hơn v3)
```
Nhà văn hóa → Khu dân cư → Nhà cô Tư → Công viên → Bờ sông NE → Đập → RC
```
- **Stack:** 7 zone trong 1 circuit, inventory 5 ô, mỗi zone sinh 3-7 món rác
- **Nguy cơ:** Circuit dài hơn v3 (7 steps vs 6). Inventory đầy ở Công viên hoặc Bờ sông NE → buộc về RC sớm → circuit gãy → phải quay lại
- **So với v3:** **Tệ hơn.** V3 có 6 steps, SCANNER có thể giúp tránh over-pickup. V4 thêm 1 step + Nhà cô Tư là zone phụ có thể ít rác → dễ bị "lố" inventory ở step sau.
- **Mitigation:** Nhà cô Tư (step 3) thường ít rác → inventory pressure thấp ở đầu circuit. Nguy cơ đầy thực sự ở Công viên (step 4) hoặc Bờ sông (step 5).

### Vùng tích tụ #3: C4 — Cross-map cuối game (vừa cải thiện vừa tệ hơn)
```
Công viên(chim) → RC → Đập(cá) → [thông cống nếu gate] → Khu dân cư(sóc) → RC
```
- **Stack:** Mỗi con vật = đến zone → nhặt rác đặc thù → về RC → quay lại → cứu
- **Cải thiện:** Gate cá xảy ra NGAY TẠI Đập — không cần đi đâu để sửa. So với v3 (phải quay lại Drainage từ Riverside).
- **Tệ hơn:** Trip Đập→Khu dân cư (SE→NW) là trip dài nhất toàn game (~380 studs, ~22 giây đi bộ).
- **So với v3:** **Mixed.** Gate handling tốt hơn, nhưng cross-map trip dài hơn.

### Vùng tích tụ #4: Toàn game — Snowball timer
- **Tổng ~24-28 trip** trong ~55-70 phút (tăng nhẹ so với v3: ~23 trip)
- Nhưng **số lần về RC giảm ~40%** (~8-10 → ~5-7)
- Trung bình mỗi 2-2.5 phút có 1 trip
- **Cải thiện:** Đường trục chính Y~50% + nửa trên/nửa dưới rõ ràng — navigation đơn giản hơn, ít bị lạc.
- **Rủi ro:** Vẫn không có natural stopping point cho trẻ 10-12 tuổi.

---

## Breakpoints

| # | Vị trí | Chuyển từ... | Sang... | Tại sao gãy | So với v3 |
|---|--------|-------------|---------|-------------|-----------|
| 1 | **C2B, lần 2 về RC** | Học thú vị | Backtrack mệt | Vừa học sort xong, chưa kịp apply đã phải đi bộ về Park rồi lại về RC | **Cải thiện** — khoảng cách ngắn hơn |
| 2 | **C3, giữa circuit** | Flow mượt | Gãy circuit | Inventory đầy ở Công viên/Bờ sông → phải về RC → mất đà | **Tệ hơn** — circuit dài hơn (7 steps) |
| 3 | **C4, Đập→Khu dân cư** | Hứng thú cứu | Đi bộ dài | Trip dài nhất game (380s), sau khi đã mệt ở phút 40-50 | **Tệ hơn** — trip dài hơn v3 |
| 4 | **C2A, Nhà văn hóa→Công viên** | Tò mò | Đi bộ dài | Trip đầu tiên tự đi đã 160 studs — có thể gây "xa quá" với trẻ 10t | **Tệ hơn** — gấp đôi v3 (80s) |
| 5 | **C5 End, Bờ sông NE→Nhà văn hóa** | Cao trào | Đi bộ về | Trip cuối trước ending, nhưng ngắn hơn v3 (180s vs 350s) | **Cải thiện đáng kể** |

---

## Diagnosis

### Friction nào là cốt lõi, nên giữ?

1. **Inventory limit 5 ô → buộc về RC** — Trụ cột gameplay loop. **GIỮ.**
2. **Environmental gating (cá cần 2/3 cống thông)** — Nhân quả rõ ràng. Hơn nữa người chơi đã ở sẵn Đập. **GIỮ.**
3. **Dynamic spawn → rác quay lại** — Shock giáo dục có chủ đích. **GIỮ.**
4. **C3 circuit đường trục chính** — Flow kim đồng hồ NW→N→NE→SE tự nhiên hơn v3. **GIỮ.**
5. **Spawn tách khỏi Bác Xanh** — Narrative "người lạ vào làng" mạnh hơn. **GIỮ.**

### Friction nào đang gây hại?

1. **C2B backtrack kép (vẫn còn)** — Dù khoảng cách ngắn hơn, vẫn là 4 trip trong 4 phút. Trip thứ 2 (tự đi nhặt rồi về sort) vẫn có thể gộp.
2. **C4: Trip Đập→Khu dân cư (380 studs)** — Dài nhất game, ở phút 40-50, không có gì xảy ra trên đường. Đây là friction point MỚI của v4.
3. **C3 Circuit 7 steps** — Dài hơn v3, inventory 5 ô dễ đầy giữa chừng.
4. **Không có fast-travel late game** — Vẫn là vấn đề từ v3.

### Friction nào đang ở mức chấp nhận được?

1. **C1: Spawn→Nhà văn hóa** — Đi bộ đầu tiên, khám phá, có rác trên đường để nhặt → không purely walking.
2. **C2A: Nhà văn hóa→Công viên** — Dài (160s) nhưng là lần đầu băng qua đường trục chính → reveal toàn map → có giá trị.
3. **Bác Xanh dẫn đường** — Follow NPC giảm cognitive load.
4. **C5 NPC circuit** — Cô Tư→Anh Tùng→Ông Sáu theo thứ tự địa lý NW→N→NE, 2 NPC cuối gần nhau.
5. **C5 End trip** — Ngắn hơn v3 đáng kể, không còn là "trip dài nhất ngay trước ending."

---

## Recommendations

### 1. (P0) Gộp C2B trip 3+4: Spawn rác gần RC sau tutorial

**Issue:** Sau khi học sort 3 món mẫu tại RC, player phải đi Park nhặt rồi về RC sort — 2 trip vẫn lặp dù khoảng cách đã ngắn hơn v3.
**Change:** Spawn 2-3 món rác ngay trong/n-goài RC để người chơi nhặt và sort luôn — không cần về Park.
**Expected effect:** Tiết kiệm 1 trip Park↔RC. Vẫn có trải nghiệm "tự nhặt → tự sort". Park trip vẫn xảy ra ở C2C.
**Priority:** P1 | **Dev cost:** Thấp (spawn rác gần RC)

### 2. (P0) C4: Cho phép gom rác cứu hộ trước khi về RC

**Issue:** Cứu chim→RC→cứu cá→RC→cứu sóc→RC = 3 RC trip riêng biệt, trong đó có trip 380 studs Đập→Khu dân cư.
**Change:** Cho phép người chơi nhặt rác cứu hộ ở Công viên (chim) + Đập (cá) + Khu dân cư (sóc) trước khi về RC. Khi về RC, sort tất cả một lần. Tăng inventory lên 8 ô tạm thời trong C4, hoặc túi phụ "rác cứu hộ".
**Expected effect:** Tiết kiệm 2 trip RC (vẫn phải đi 3 điểm, nhưng chỉ 1 lần sort). Trip dài Đập→Khu dân cư giờ là 1 trong 3 điểm đến, không còn phải về RC giữa chừng.
**Priority:** P1 | **Dev cost:** Trung bình (inventory exception)

### 3. (P1) C3 Circuit: Cảnh báo sớm inventory + cho phép bỏ qua Nhà cô Tư

**Issue:** Circuit 7 steps dài hơn v3, inventory dễ đầy ở step 4-5.
**Change A:** Khi bắt đầu circuit, hiện tooltip "Inventory còn 5 ô. Có thể bỏ qua Nhà cô Tư nếu muốn — quay lại sau."
**Change B:** Nhà cô Tư (step 3) là optional — nếu bỏ qua, vẫn đi thẳng Khu dân cư→Công viên.
**Expected effect:** Circuit linh hoạt hơn. Người chơi có thể skip Nhà cô Tư để giữ inventory, quay lại sau khi sort.
**Priority:** P2 | **Dev cost:** Thấp (UI text + optional flag)

### 4. (P1) C4: Thêm "cầu gỗ bắc sông" làm shortcut giữa Công viên và Đập

**Issue:** Trip cross-map dài nhất (Đập→Khu dân cư 380 studs) không có shortcut.
**Change:** Sau khi thông Cống 2 (C3/C4), mở cầu gỗ bắc qua sông nối Công viên (NE) ↔ bờ bên kia gần Đập (SE). Đi tắt này giảm trip Đập→Khu dân cư bằng cách: Đập → cầu gỗ → Công viên → Nhà cô Tư → Khu dân cư (thay vì đi vòng đường trục chính).
**Expected effect:** Giảm ~100 studs cho trip dài nhất game. Tuyến đường mới: Đập→cầu→Công viên (đẹp, đi qua cầu gỗ trên sông).
**Priority:** P2 | **Dev cost:** Trung bình (1 cầu gỗ + collision)

### 5. (P1) C1: Thêm 1-2 món rác "đặc biệt" trên đường Spawn→Nhà văn hóa

**Issue:** Trip đầu tiên dài ~80 studs, chưa có hành động gì ngoài đi bộ.
**Change:** Đặt 1-2 món rác "to" trên đường (ví dụ: tấm biển quảng cáo cũ, bao tải rác lớn) — nhặt được, auto-disappear, tạo cảm giác "mình đang làm việc có ích ngay từ đầu."
**Expected effect:** Giảm cảm giác "đi bộ không" — có hành động xen kẽ.
**Priority:** P3 | **Dev cost:** Thấp (đặt 2 rác to trên đường)

### 6. (P2) Toàn game: Thêm checkpoint/pause point rõ ràng giữa các Chapter

**Issue:** 55-70 phút không có natural stopping point cho trẻ 10-12 tuổi (vấn đề từ v3).
**Change:** Cuối C2 và C4, Bác Xanh nói câu như "Ngày mai cháu quay lại nhé" — màn hình tối 2 giây — sáng lại. Nhà văn hóa trở thành "điểm về" tự nhiên.
**Expected effect:** Người chơi có thể tự ngừng. Giảm drop rate.
**Priority:** P3 | **Dev cost:** Thấp (1-2 câu thoại)

---

## So sánh v3 → v4

| Chỉ số | v3 | v4 | Thay đổi |
|--------|----|----|----------|
| Tổng trip | ~23 | ~24-28 | 🔺 +1-5 |
| Số lần về RC | ~8-10 | ~5-7 | 🔽 -30-40% |
| Trip dài nhất | 350 studs (Riverside→Res) | 380 studs (Đập→Res) | 🔺 +30 studs |
| Trip ngắn nhất | 60 studs (SQ→RC) | 70 studs (NVH→RC) | ≈ tương đương |
| C5 End trip | 350 studs (Riverside→SQ) | 180 studs (NE→NVH) | 🔽 -48% |
| C2A first solo trip | 80 studs | 160 studs | 🔺 gấp đôi |
| Breakpoint #4 (C5 end) | Critical | Không còn | ✅ Đã giải quyết |
| Navigation model | Grid phức tạp | Trên/Dưới rõ ràng | ✅ Cải thiện |
| Gate cá (C4) | Phải đi lại Drainage | Đã ở sẵn Đập | ✅ Cải thiện |
| Backtrack C2B | 4 trip dài | 4 trip ngắn hơn | ✅ Cải thiện một phần |
| Circuit C3 | 6 steps | 7 steps | 🔺 Phức tạp hơn |

---

## Minimal Fix

**Chỉ 1 thay đổi có leverage cao nhất:**

> **C4: Cho phép gom rác cứu hộ (3 con) vào inventory mở rộng tạm thời, sort 1 lần duy nhất.**

*Lý do:* Đây là nơi trip dài nhất game (380 studs) + pattern lặp 3 lần mệt nhất. Gom rác cứu hộ vào 1 trip RC duy nhất tiết kiệm 2 trip, giảm cross-map fatigue ở phút 40-50, và không phá vỡ core loop (vẫn cần sort — chỉ gom lại).

---

*GREEN AGAIN v4 — Friction Journey Audit — Tháng 6/2026*
