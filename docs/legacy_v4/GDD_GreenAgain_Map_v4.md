# GREEN AGAIN v4 — BẢN ĐỒ THỊ TRẤN VEN SÔNG (KIỂU VIỆT NAM)

> **Tạo:** Tháng 6/2026 — Thiết kế lại toàn bộ theo phong cách làng quê Việt Nam
> **Dựa trên:** GDD v3 + JSON bản đồ mới
> **Thay đổi chính:** Sông uốn lượn Bắc→Đông Nam, Nhà văn hóa thay Quảng trường, Đập 3 cống thay cống đơn, Rừng bao quanh

---

## 1. TỔNG QUAN MÔI TRƯỜNG

**Địa hình:** Thị trấn Ven Sông nằm trong một thung lũng nhỏ, bao bọc bởi đồi núi và rừng cây rậm rạp ở các phía (Bắc, Nam, Tây, Đông Bắc).

**Sông:** Một con sông chạy dọc từ phía Bắc (gần công viên) uốn lượn xuống phía Đông Nam, đi qua một con đập có 3 cống xả nước ở phía Nam.

**Đường trục chính:** Một con đường chính nằm ngang (trục Y ~50%), chia cắt nửa trên (Khu dân cư, Nhà cô Tư, Công viên) và nửa dưới (Điểm spawn, Nhà văn hóa, Trung tâm tái chế).

---

## 2. BẢN ĐỒ ASCII (TOP-DOWN)

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                        🌲 RỪNG CÂY — ĐỒI NÚI BAO QUANH                       │
│                                                                              │
│  ┌──────────────────────────┬──────────┬─────────────────────────────────┐  │
│  │                          │          │                                 │  │
│  │   🏘️ KHU DÂN CƯ         │ 🏚️ NHÀ   │     🌳 CÔNG VIÊN                │  │
│  │   PL ban đầu: 60         │ CÔ TƯ    │     PL ban đầu: 55              │  │
│  │                          │          │                                 │  │
│  │   [🏠] [🏠] [🏠]        │ ┌──────┐ │  ┌──────────────────┐   🪨      │  │
│  │                          │ │Tiệm  │ │  │  Cây lớn         │   Mỏm đá  │  │
│  │   🟠 HOTSPOT:            │ │tạp   │ │  │                  │        ╱  │  │
│  │   Residential St.        │ │hóa   │ │  │  ┌─────┐        │   ≈≈≈╱   │  │
│  │                          │ │👩CôTư│ │  │  │Cối  │        │   Sông    │  │
│  │   🐿️ Sóc (C4)           │ └──────┘ │  │  │xay  │🧑Anh   │  ╱       │  │
│  │                          │          │  │  │gió  │Tùng    │ ╱        │  │
│  │                          │          │  │  └─────┘        │╱    👴    │  │
│  └──────────────────────────┴──────────┘  │  👧 Bé Na      │ Ông Sáu  │  │
│                                           │  🟠 Picnic      │ (NE)     │  │
│                                           │  🐦 Chim (C4)   │          │  │
│                                           └──────────────────┘          │  │
│                                                                         │  │
│ ════════════════════════ ĐƯỜNG TRỤC CHÍNH (~Y=50%) ══════════════════════ │
│                                                                         │  │
│  ┌────────────────────────────┬──────────────────────────────┐          │  │
│  │                            │                              │          │  │
│  │  ⚡ SPAWN (góc dưới trái) │  🏛️ NHÀ VĂN HÓA              │  ♻️ TRUNG│  │
│  │                            │  Mái ngói đỏ                 │  TÂM TÁI │  │
│  │                            │                              │  CHẾ     │  │
│  │                            │  ┌──────────┐               │          │  │
│  │                            │  │ 🧓 BÁC   │               │  ┌──┬──┐ │  │
│  │                            │  │  XANH    │               │  │HC│TC│ │  │
│  │                            │  │  Mentor  │               │  ├──┼──┤ │  │
│  │                            │  └──────────┘               │  │VC│ĐH│ │  │
│  │                            │                              │  └──┴──┘ │  │
│  │                            │  👩‍🔧 Chị Lan tại đây       │          │  │
│  │                            │  (chuyển từ RC cũ)          │          │  │
│  └────────────────────────────┴──────────────────────────────┘          │  │
│                                                                         │  │
│                         ≈ ≈ ≈ ≈ ≈ SÔNG ≈ ≈ ≈ ≈ ≈                        │  │
│                         ≈ ≈ ≈ uốn lượn → Đông Nam ≈ ≈ ≈                  │  │
│                                                                         │  │
│  ┌──────────────────────────────────────────────────────────────────┐   │  │
│  │                    🏗️ ĐẬP NƯỚC (3 cống xả)                       │   │
│  │                    PL ban đầu: 80 (CAO NHẤT)                      │   │
│  │                                                                   │   │
│  │    ┌─────────┐    ┌─────────┐    ┌─────────┐                      │   │
│  │    │ Cống 1  │    │ Cống 2  │    │ Cống 3  │                      │   │
│  │    │  🔴 80   │    │  🔴 80   │    │  🔴 80   │                     │   │
│  │    └─────────┘    └─────────┘    └─────────┘                      │   │
│  │                                                                   │   │
│  │    🔴 HOTSPOT: Dam (3 cống) — Pollution Spread Event              │   │
│  │    🐟 Cá (C4) — tập trung dưới chân đập                          │   │
│  └──────────────────────────────────────────────────────────────────┘   │  │
│                                                                          │  │
│                        🌲 RỪNG CÂY — ĐỒI NÚI                               │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## 3. BẢN ĐỒ CHI TIẾT (DÀNH CHO DEV)

### 3.1 Kích thước & tỉ lệ Roblox

| Thông số | Giá trị |
|----------|---------|
| Tổng diện tích map | ~800 × 700 studs |
| Khu vực chơi được | 5 zone chính + Nhà cô Tư (zone phụ) + Đập (zone đặc biệt) |
| Rừng bao quanh | Tứ phía (Bắc, Nam, Tây, Đông Bắc) — visual only |
| Khoảng cách trung bình giữa 2 zone | ~120-180 studs |
| Trip dài nhất (Khu dân cư → Đập) | ~380 studs |
| Trip ngắn nhất (Nhà văn hóa → Trung tâm Tái chế) | ~70 studs |

### 3.2 Tọa độ từng khu vực (tham khảo — theo % của map)

| Khu vực | x_start% | x_end% | y_start% | y_end% | Ghi chú |
|---------|----------|--------|----------|--------|---------|
| Khu dân cư | 0 | 35 | 20 | 50 | NW, trên đường trục chính, giáp rừng trái |
| Nhà cô Tư | 35 | 45 | 20 | 50 | N-center, giữa Khu dân cư và Công viên, có đường kẻ đen phân ranh |
| Công viên | 45 | 70 | 15 | 50 | NE, giáp sông bên phải, hình vuông khoanh viền đen |
| Nhà văn hóa | 20 | 45 | 50 | 75 | SW, dưới đường trục chính, mái ngói đỏ |
| Trung tâm Tái chế | 45 | 65 | 50 | 75 | SE, sát khúc quanh sông, kề Nhà văn hóa |
| Đập nước | 45 | 75 | 75 | 95 | Cuối dòng sông, mép Nam, 3 cống xả |
| Sông | — | — | — | — | Chảy Bắc→Đông Nam, từ cạnh Công viên xuống Đập |

### 3.3 Vị trí cụ thể (tọa độ tương đối %, x, y)

| Đối tượng | Khu vực | x% | y% | Ghi chú |
|-----------|---------|----|----|---------|
| **Spawn point** | Góc dưới trái | 10 | 60 | Giáp rừng trái + đường ranh Nhà văn hóa |
| **Bác Xanh** | Nhà văn hóa | 32 | 62 | Trước cửa Nhà văn hóa, ghế đá |
| **Cô Tư** | Nhà cô Tư | 40 | 35 | Trước tiệm tạp hóa nhỏ |
| **Anh Tùng** | Công viên | 58 | 30 | Trên thảm picnic |
| **Ông Sáu** | Bờ sông NE | 75 | 25 | Sát mép sông, gần mỏm đá tảng |
| **Chị Lan** | Nhà văn hóa / Trung tâm Tái chế | 55 | 65 | Quản lý khu vực phân loại |
| **Bé Na** | Công viên | 60 | 40 | Gần cây lớn |
| **Cây lớn** | Công viên | 55 | 18 | Mép trên Công viên, nơi chim đậu |
| **Cối xay gió** | Công viên | 62 | 22 | Landmark toàn map |
| **Đập — Cống 1** | Đập nước | 50 | 82 | Cống trái |
| **Đập — Cống 2** | Đập nước | 58 | 82 | Cống giữa |
| **Đập — Cống 3** | Đập nước | 66 | 82 | Cống phải |
| **Mỏm đá tảng** | Bờ sông NE | 78 | 22 | Gần Ông Sáu |

### 3.4 Vị trí trồng cây (C5)

| Cây | Khu vực | x% | y% | Ghi chú |
|-----|---------|----|----|---------|
| Cây 1 | Rừng Bắc — gần Khu dân cư | 10 | 10 | Đất trồng ven rừng |
| Cây 2 | Rừng Bắc — gần Công viên | 65 | 8 | Đất trồng ven rừng |
| Cây 3 | Ven sông — cạnh Công viên | 70 | 40 | Gần bờ sông, phía Park |
| Cây 4 | Ven sông — khúc quanh | 68 | 55 | Giữa dòng sông uốn lượn |
| Cây 5 | Dưới chân đập | 60 | 88 | Cạnh đập nước, biểu tượng phục hồi |
| Cây 6 | Nhà văn hóa | 28 | 72 | Trước sân Nhà văn hóa |
| Cây 7 | Khu dân cư | 18 | 40 | Gần nhà dân |

---

## 4. HỆ THỐNG ĐƯỜNG ĐI & GIAO THÔNG

### 4.1 Sơ đồ đường đi

```
                        ┌──────────────┐
                        │  KHU DÂN CƯ  │
                        │     (NW)     │
                        └──────┬───────┘
                               │
                    ┌──────────┴──────────┐
                    │    NHÀ CÔ TƯ (N)    │
                    └──────────┬──────────┘
                               │
                    ┌──────────┴──────────┐
                    │   CÔNG VIÊN (NE)   │──── Sông (Bắc)
                    └──────────┬──────────┘
                               │
═══════════════════ ĐƯỜNG TRỤC CHÍNH ═══════════════════
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
   ┌──────┴──────┐    ┌────────┴────────┐   ┌───────┴──────┐
   │   SPAWN     │    │  NHÀ VĂN HÓA   │   │ TRUNG TÂM    │
   │  (SW góc)   │────│     (SW)       │───│ TÁI CHẾ (SE) │
   └─────────────┘    └────────┬───────┘   └───────┬──────┘
                               │                    │
                               │    SÔNG UỐN LƯỢN   │
                               │    Bắc → Đông Nam  │
                               └──────────┬─────────┘
                                          │
                                 ┌────────┴────────┐
                                 │  ĐẬP NƯỚC (S)  │
                                 │   3 cống xả     │
                                 └─────────────────┘
```

### 4.2 Chi tiết từng tuyến đường

| Tuyến | Mô tả | Khoảng cách (studs) | Thời gian đi bộ |
|-------|-------|---------------------|------------------|
| Spawn → Nhà văn hóa | Dọc đường dưới, men rừng trái | ~80 | ~5 giây |
| Nhà văn hóa → Trung tâm Tái chế | Đường dưới, ngang qua | ~70 | ~4 giây |
| Nhà văn hóa → Khu dân cư | Cắt ngang đường trục chính lên NW | ~130 | ~8 giây |
| Nhà văn hóa → Công viên | Cắt đường trục chính lên NE | ~160 | ~10 giây |
| Khu dân cư → Nhà cô Tư | Đi ngang phía trên đường trục | ~40 | ~2 giây |
| Nhà cô Tư → Công viên | Tiếp tục ngang phía trên | ~60 | ~4 giây |
| Công viên → Ông Sáu (NE) | Dọc bờ sông lên Bắc | ~100 | ~6 giây |
| Công viên → Trung tâm Tái chế | Xuống đường trục chính → SE | ~100 | ~6 giây |
| Trung tâm Tái chế → Đập nước | Đi xuống phía Nam, men sông | ~120 | ~7 giây |
| Khu dân cư → Đập nước | Cross-map NW→S | ~380 | ~22 giây |
| Khu dân cư → Trung tâm Tái chế | NW→SE, cắt đường trục | ~200 | ~12 giây |

### 4.3 Đường tắt (mở sau C3)

| Đường tắt | Mở khi | Kết nối | Tiết kiệm |
|-----------|--------|---------|-----------|
| Cầu gỗ bắc sông | Sau khi thông Cống 2 (C3) | Công viên → Trung tâm Tái chế (qua sông) | ~40 studs |
| Đường mòn ven đồi | Sau khi thông toàn bộ đập (C4) | Khu dân cư → Nhà văn hóa (men rừng) | ~60 studs |
| Bậc đá xuống đập | Sau C3 | Trung tâm Tái chế → Đập (đường thẳng) | ~30 studs |

### 4.4 Biển chỉ dẫn (Wayfinding v4)

| Vị trí | Nội dung biển |
|--------|---------------|
| Spawn → Nhà văn hóa | "→ Nhà Văn Hóa — Gặp Bác Xanh" |
| Ngã ba: Nhà văn hóa → RC / lên đường trục | "↑ Khu Dân Cư — Công Viên | → Trung Tâm Tái Chế" |
| Đường trục chính: dưới chân dốc lên Bắc | "↑ Nhà Cô Tư — Công Viên" |
| Đường trục chính: rẽ vào Công viên | "→ Công Viên — Bờ Sông" |
| Gần đập nước | "⚠ Đập Nước — 3 Cống Xả. Nguy hiểm!" |
| Bờ sông NE (gần Ông Sáu) | "🐟 Khu vực câu cá — Giữ sạch bờ sông" |

---

## 5. HOTSPOT & MARKER MÀU

### 5.1 Danh sách hotspot

| Hotspot | Khu vực | Màu ban đầu | PL ban đầu | Mở khóa |
|---------|---------|------------|------------|---------|
| Residential Street | Khu dân cư | 🟠 Cam | 60 | C2C |
| Picnic Area | Công viên | 🟠 Cam | 55 | C2A |
| Dam — Cống 1 | Đập nước | 🔴 Đỏ | 80 | C2C |
| Dam — Cống 2 | Đập nước | 🔴 Đỏ | 80 | C3 |
| Dam — Cống 3 | Đập nước | 🔴 Đỏ | 80 | C3 |
| Riverside — Khúc quanh | Ven sông (giữa) | 🟡 Vàng | 40 | C3 |
| Riverside — NE (Ông Sáu) | Ven sông (NE) | 🟡 Vàng | 45 | C2C |

### 5.2 Hệ thống màu marker (giữ nguyên)

| Màu | PL khu vực | Ý nghĩa | Hành động gợi ý |
|------|-----------|---------|-----------------|
| 🟡 Vàng | < 40 | Ô nhiễm nhẹ | Theo dõi |
| 🟠 Cam | 40–70 | Ô nhiễm trung bình | Nhặt rác + phân loại |
| 🔴 Đỏ | > 70 | Ô nhiễm nghiêm trọng | Ưu tiên xử lý ngay |
| ✅ Xanh | < 20 | Đã xử lý | Không cần can thiệp |

### 5.3 Phạm vi phát hiện (giữ nguyên v3)

| Hành động | Phạm vi |
|-----------|---------|
| Scanner phát hiện hotspot | 50 studs |
| Nhặt rác | 5 studs |
| Đặt thùng rác (bán kính ảnh hưởng) | 25 studs |
| Đặt biển báo (bán kính ảnh hưởng) | 30 studs |
| Trồng cây (bán kính visual) | 15 studs |
| Cứu chim (bán kính dọn rác nhựa) | 15 studs |
| Cứu sóc (bán kính dọn rác độc hại) | 20 studs |

---

## 6. HỆ THỐNG ĐẬP NƯỚC & 3 CỐNG XẢ (MỚI — thay thế Cống đơn)

### 6.1 Cấu trúc

Đập nước nằm ở cuối dòng sông (mép Nam bản đồ). Gồm 3 cống xả độc lập:

| Cống | Vị trí | PL ban đầu | Mở khóa |
|------|--------|------------|---------|
| Cống 1 (trái) | 50%, 82% | 80 | C2C (phát hiện), C3 (thông) |
| Cống 2 (giữa) | 58%, 82% | 80 | C3 |
| Cống 3 (phải) | 66%, 82% | 80 | C3 |

### 6.2 Cơ chế thông cống

Mỗi cống là một thực thể riêng:
1. Nhặt sạch rác trong bán kính 15 studs quanh cống đó
2. Giữ E 3 giây để thông cống
3. Không cần về RC trước khi thông — nhưng rác nhặt được vẫn cần sort
4. Mỗi cống thông → PL khu vực Đập giảm 25 điểm
5. Thông cả 3 cống → Đập hoạt động bình thường, nước chảy sạch qua

### 6.3 Pollution Spread Event (thiết kế lại cho 3 cống)

**Giai đoạn 1 — 1 cống tắc (PL > 75%):**
> 💬 "⚠ Cảnh báo: Một cống xả đang tắc. Nước bắt đầu ứ đọng."

**Giai đoạn 2 — 2 cống tắc (sau 3 phút không xử lý):**
> 💬 "🚨 Cảnh báo: 2 cống xả đã tắc! Rác bắt đầu tràn ra khúc quanh sông. Mức ô nhiễm sông tăng +10."

**Giai đoạn 3 — 3 cống tắc (sau 5 phút):**
> 💬 "🔴 NGUY CẤP: Toàn bộ đập bị tắc! Rác tràn xuống hạ lưu. Cá dưới chân đập đang bị ảnh hưởng nghiêm trọng."

**Sau khi thông mỗi cống:**
> 💬 "✅ Cống [1/2/3] đã được thông! Nước chảy qua bình thường."

### 6.4 Cá (C4) — vị trí mới

Cá tập trung dưới chân đập (khu vực nước sâu). Điều kiện cứu:
- Ít nhất 2/3 cống đã được thông
- PL trung bình khu vực Đập < 40

---

## 7. NPC VỊ TRÍ & PHẠM VI

| NPC | Vị trí cố định | Xuất hiện từ | Phạm vi di chuyển | Trạng thái |
|-----|---------------|-------------|-------------------|------------|
| **Bác Xanh** | Ghế đá trước Nhà văn hóa (mái ngói đỏ) | C1 | Trong/trước Nhà văn hóa (trừ lúc dẫn đường C2B, C2C) | Luôn ở Nhà văn hóa |
| **Cô Tư** | Trước tiệm tạp hóa, Nhà cô Tư | C2 | Quanh tiệm (~15 studs) | Unaware → Aware → Considerate |
| **Anh Tùng** | Thảm picnic, Công viên | C2 | Quanh thảm (~20 studs) | Unaware → Aware → Considerate |
| **Ông Sáu** | Bờ sông NE, cạnh mỏm đá tảng | C3 | Dọc bờ sông gần mỏm đá (~25 studs) | Unaware → Aware → Considerate |
| **Chị Lan** | Nhà văn hóa (gần khu Trung tâm Tái chế) | C2B | Quanh Nhà văn hóa + RC (~25 studs) | Không đổi |
| **Bé Na** | Gần cây lớn, Công viên | C2 | Quanh cây (~10 studs) | Không đổi |

---

## 8. LUỒNG DI CHUYỂN THEO CHAPTER (v4)

### Chapter 1: Khởi đầu
```
[Spawn góc dưới trái] → Đi dọc đường dưới → Nhặt rác rải rác trên đường
→ Đến Nhà văn hóa → Gặp Bác Xanh → Nhận Scanner
```
**Số trip:** 1 (Spawn → Nhà văn hóa) | **Về RC:** 0 | **Phạm vi:** Nửa dưới map

### Chapter 2A: Làm quen Scanner
```
[Nhà văn hóa] → Lên đường trục chính → Rẽ vào Công viên
→ Bật Scanner, tìm hotspot Picnic Area → Nhặt rác (auto-disappear)
```
**Số trip:** 1 (Nhà văn hóa → Công viên) | **Về RC:** 0

### Chapter 2B: Học phân loại
```
[Bác Xanh dẫn] Nhà văn hóa → Trung tâm Tái chế (học sort 3 món mẫu)
→ Công viên (tự nhặt rác) → Trung tâm Tái chế (tự sort)
```
**Số trip:** 2 (+ follow) | **Về RC:** 1

### Chapter 2C: Đối mặt thực tế
```
[Bác Xanh dẫn] Trung tâm Tái chế → Đập nước (thấy Cống 1, chưa thông)
→ Khu dân cư (nhặt rác Residential St.)
→ Trung tâm Tái chế (sort) → Công viên (thấy rác quay lại)
```
**Số trip:** 3-4 | **Về RC:** 1-2

### Chapter 3: Ngăn rác quay lại (Spatial Circuit mới)
```
Nhà văn hóa (nhận 3 thùng rác + 2 biển báo từ Bác Xanh)
  ↓
[1] KHU DÂN CƯ: Đặt thùng rác + nhặt rác
  ↓
[2] NHÀ CÔ TƯ: Đi ngang qua, đặt biển báo gần tiệm
  ↓
[3] CÔNG VIÊN: Đặt thùng rác + nhặt rác
  ↓
[4] VEN SÔNG NE (Ông Sáu): Đặt biển báo
  ↓
[5] ĐẬP NƯỚC: Nhặt rác quanh Cống 1 + thông cống 1
  ↓
[6] TRUNG TÂM TÁI CHẾ: Sort toàn bộ inventory
```
**Số trip:** 7 | **Về RC:** 1 (cuối circuit)

### Chapter 4: Cứu sinh vật
```
Nhà văn hóa → Công viên (cứu chim: nhặt rác nhựa → sort → cứu)
→ Trung tâm Tái chế (sort rác nhựa)
→ Đập nước (cứu cá: kiểm tra 2/3 cống đã thông? → cứu)
→ [Nếu bị gate: thông thêm cống 2,3]
→ Khu dân cư (cứu sóc: nhặt rác độc hại → sort → cứu)
→ Trung tâm Tái chế (sort rác độc hại)
```
**Số trip:** 5-7 | **Về RC:** 2-3

### Chapter 5: Cộng đồng và kết thúc
```
Nhà văn hóa (Bác Xanh mở đầu C5)
  ↓
[1] KHU DÂN CƯ → NHÀ CÔ TƯ: Thuyết phục Cô Tư
  ↓
[2] CÔNG VIÊN: Thuyết phục Anh Tùng
  ↓
[3] VEN SÔNG NE: Thuyết phục Ông Sáu
  ↓
[4] Trồng cây rải rác (3-5 cây ở các khu)
  ↓
[5] NHÀ VĂN HÓA: Gặp Bác Xanh → Ending
```
**Số trip:** 5-6 | **Về RC:** 0

### Tổng kết toàn game

| Chapter | Số trip | Về RC | Thời gian (phút) |
|---------|---------|-------|-------------------|
| C1 | 1-2 | 0 | 5-8 |
| C2A | 1 | 0 | 3-4 |
| C2B | 2 | 1 | 4-5 |
| C2C | 3-4 | 1-2 | 4-5 |
| C3 | 7 | 1 | 10-15 |
| C4 | 5-7 | 2-3 | 10-15 |
| C5 | 5-6 | 0 | 10-15 |
| **Tổng** | **~24-28** | **~5-7** | **~55-70** |

> ⚠️ **So với v3:** Tổng trip tăng nhẹ (~23 → ~24-28) do Spawn tách khỏi Bác Xanh, nhưng số lần về RC giảm (~8-10 → ~5-7) do Trung tâm Tái chế gần Nhà văn hóa và Đập hơn.

---

## 9. CÁC LỚP VISUAL MAP

### 9.1 Layer 1: Nền (Ground)
- **Nửa trên (Bắc):** Đất nâu + cỏ xanh (khu dân cư, công viên)
- **Nửa dưới (Nam):** Đất gạch xám (Nhà văn hóa, đường, Trung tâm Tái chế)
- **Sông:** Nước xanh đậm (bẩn) → xanh trong (sạch) theo tiến trình
- **Rừng bao quanh:** Màu xanh rừng rậm, không vào được (collision wall)

### 9.2 Layer 2: Cấu trúc (Structures)
- Nhà dân (Khu dân cư): 3-5 căn đơn giản, mái ngói
- Tiệm tạp hóa (Nhà cô Tư): 1 building nhỏ, có sạp hàng phía trước
- Nhà văn hóa: Tòa nhà mái ngói đỏ, cửa gỗ, có sân trước
- Trung tâm Tái chế: Nhà khung thép, 4 thùng phân loại, băng chuyền nhỏ
- Cối xay gió (Công viên): Landmark cao, thấy từ mọi khu vực
- Đập nước: Cấu trúc bê tông lớn, 3 cửa cống, nước chảy qua
- Đường trục chính: Đường đất rộng, chia đôi map

### 9.3 Layer 3: NPC & Interactive
- NPC với animation idle + di chuyển trong phạm vi
- Rác (cố định + động)
- Hotspot marker (khi bật Scanner Q)
- Prompt [E] cho tương tác
- Thùng rác / biển báo đã đặt

### 9.4 Layer 4: UI Overlay
- Minimap (góc trên trái, phím M toggle)
- HUD 3 chỉ số (ES / PL / CA)
- Quest tracker (góc trên phải)
- Inventory bar (dưới cùng)

---

## 10. MINIMAP (v4)

```
┌──────────────────────────────────┐
│        🌲 RỪNG CÂY (Bắc)        │
│                                  │
│  KDCư   │CôTư│   CôngViên      │
│  🟠     │    │    🟠   🪨👴    │
│         │    │         ≈≈≈     │
│───────── Đường Trục ─────────  │
│         │    │         ≈≈≈     │
│  ●Spawn│ NVH │   ♻RC   ≈≈≈    │
│         │ 🟢 │         ≈≈≈     │
│         │    │         ≈≈≈     │
│  ───────── Đập 🔴 ──────────  │
│        🌲 RỪNG CÂY (Nam)       │
└──────────────────────────────────┘
```

**Hiển thị:**
- ● = Vị trí người chơi (màu trắng)
- 🟢 = Bác Xanh (Nhà văn hóa)
- ♻ = Trung tâm Tái chế
- 👴 = Ông Sáu (bờ sông NE)
- 🟠/🔴 = Hotspot marker màu
- ≈ = Sông
- 🪨 = Mỏm đá tảng
- ─── = Đường trục chính

---

## 11. THAY ĐỔI MAP TỪ v3 → v4

| # | Thay đổi | Lý do | Impact |
|---|----------|-------|--------|
| 1 | **Quảng trường → Nhà văn hóa** | Phù hợp làng quê VN, có building mái ngói đỏ làm neo không gian | Bác Xanh chuyển về đây, C1+C5 thiết kế lại |
| 2 | **Sông uốn lượn Bắc→Đông Nam** | Tự nhiên hơn, sông chảy xuyên map = thanh tiến trình trực quan | Ông Sáu chuyển lên NE, thêm hotspot dọc sông |
| 3 | **Cống đơn → Đập 3 cống** | Đập nước là công trình quen thuộc VN, 3 cống = 3 cấp độ xử lý | Pollution Spread Event 3 giai đoạn, "boss fight" cuối game |
| 4 | **Rừng bao quanh tứ phía** | Thung lũng biệt lập — thẩm mỹ làng quê | Nhiều vị trí trồng cây hơn |
| 5 | **Đường trục chính Y~50%** | Phân chia "trên/dưới" rõ ràng cho trẻ 10-12t | Navigation đơn giản hơn, wayfinding tốt hơn |
| 6 | **Nhà cô Tư tách zone riêng** | Ranh giới rõ — tăng cảm giác "không gian riêng" | C5 thuyết phục có chiều sâu hơn |
| 7 | **Spawn góc dưới trái** | "Người lạ từ ngoài vào" — narrative mạnh hơn | C1 cần đi bộ đến Nhà văn hóa (thêm 1-2 trip) |
| 8 | **RC cạnh Nhà văn hóa (cùng nửa dưới)** | Gom cụm "khu xử lý" phía Nam | Giảm ~40% số lần về RC so với v3 (~8-10 → ~5-7) |
| 9 | **Công viên giáp sông** | Bờ sông trong công viên = visual đẹp | Cứu chim có thêm context sông, Anh Tùng thấy rác→sông trực quan |
| 10 | **Bỏ "Bờ sông" thành zone riêng** | Sông giờ là dải chảy xuyên map, không phải 1 zone | Thay bằng các điểm tương tác dọc sông |

---

## 12. HƯỚNG DẪN BUILD MAP TRONG ROBLOX STUDIO

### 12.1 Quy trình

1. **Tạo Baseplate:** 800×700 studs, flat terrain
2. **Tạo đồi núi bao quanh:** Dùng Terrain Editor nâng cao rìa Bắc, Nam, Tây, Đông Bắc
3. **Vẽ sông:** Dùng Terrain Editor hạ thấp lòng sông từ Bắc (cạnh Công viên) → uốn lượn → Đông Nam → kết thúc ở Đập
4. **Vẽ đường trục chính:** Đường đất rộng ngang ở Y~50%
5. **Phân vùng màu đất:** Nửa trên = cỏ/nâu, nửa dưới = gạch xám
6. **Dựng structures theo thứ tự:**
   - Nhà văn hóa (mái ngói đỏ) — SW
   - Trung tâm Tái chế (khung thép) — SE
   - Nhà dân (3-5 căn) — NW
   - Tiệm tạp hóa Cô Tư — N-center
   - Cối xay gió + thảm picnic — Công viên NE
   - Đập nước + 3 cống — cực Nam
7. **Đặt props:** Ghế đá (trước Nhà văn hóa), thảm picnic, cây cối, thùng rác, mỏm đá tảng (NE)
8. **Path system:** Đường đất nối Spawn→Nhà văn hóa→RC, và các nhánh lên nửa trên
9. **NPC placement:** Spawn locations cho 6 NPC
10. **Rác spawner:** Fixed trash (tutorial) + Dynamic spawners
11. **Water:** Sông bằng transparent parts + flow animation
12. **Lighting:** Ánh sáng thay đổi theo ES (FutureTint màu)

### 12.2 Gợi ý asset Roblox Marketplace

| Cần | Từ khóa tìm |
|-----|------------|
| Nhà văn hóa mái ngói đỏ | "temple" "pagoda" "red roof" (free) |
| Nhà dân đơn giản | "house" "suburban" "vietnam" (free) |
| Đập nước | "dam" "concrete" "water gate" |
| Cống xả | "pipe" "drain" "sewer" |
| Cối xay gió | "windmill" "old" |
| Cây | "tree" "oak" "banyan" (free) |
| Thùng rác | "trash bin" "recycle bin" |
| Ghế đá | "bench" "park" "stone" |
| Biển báo gỗ | "sign" "wooden" |
| Cầu gỗ | "bridge" "wooden" |
| Mỏm đá | "rock" "boulder" "cliff" |
| Thảm picnic | "picnic" "blanket" "mat" |

---

*GREEN AGAIN v4 — Thị trấn Ven Sông — Map Documentation (Kiểu Việt Nam)*
*Tháng 6/2026*
