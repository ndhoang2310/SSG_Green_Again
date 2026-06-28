# GREEN AGAIN v3 — BẢN ĐỒ THỊ TRẤN VEN SÔNG

> **Tạo:** Tháng 6/2026 — Dựa trên GDD v2.0 + v3 changes  
> **File SVG:** `map_ven_song_topdown.svg`  
> **Friction Journey Audit:** Xem `friction_journey_audit.md`  
> **Flow Audit:** Xem `flow_audit.md`

---

## 1. BẢN ĐỒ ASCII (TOP-DOWN)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                          🌲 RỪNG CÂY (Visual Background)                  │
│                      Không vào được — chỉ để ngắm                         │
│     [🌱 Đất trồng cây]                                [🌱 Đất trồng cây]  │
├─────────────────────┬────────────────────────────────────────────────────┤
│                     │                                                    │
│   🏘️ KHU DÂN CƯ    │              🌳 CÔNG VIÊN / KHU PICNIC              │
│   PL ban đầu: 60    │              PL ban đầu: 55                        │
│                     │                                                    │
│   ┌──────────────┐  │   ┌──────────────┐           ┌─────┐               │
│   │ Tiệm tạp hóa  │  │   │ Thảm picnic  │           │Cối  │ ← Landmark   │
│   │ 👩 Cô Tư     │  │   │ 🧑 Anh Tùng  │           │xay  │   toàn map   │
│   │ (Unaware)    │  │   │ (Unaware)    │           │gió  │               │
│   └──────────────┘  │   └──────────────┘           │cũ   │               │
│                     │                              └─────┘               │
│   [🏠] [🏠] [🏠]    │   [🌳 Cây]  [🌳 Cây]   👧 Bé Na (gần cây)          │
│                     │                                                    │
│   🟠 HOTSPOT:       │   🟠 HOTSPOT: Picnic Area                          │
│   Residential St.   │   🐦 Chim (C4) — mắc túi nhựa                      │
│   . . . rác . . .   │   . . . rác sinh hoạt . . .                        │
│   🐿️ Sóc (C4)      │                                                    │
│                     │            │                                       │
├──────────┬──────────┴────────────┼───────────────────────────────────────┤
│          │                       │                                       │
│  🏛️ QUẢNG TRƯỜNG  │  ♻️ TRUNG TÂM TÁI CHẾ │     🌊 BỜ SÔNG              │
│  PL ban đầu: 40    │  Hub phân loại        │     PL ban đầu: 50          │
│  ⚡ SPAWN POINT    │  (Vị trí TRUNG TÂM)   │                              │
│                    │                       │                              │
│      [⛲]          │  ┌──┬──┬──┬──┐       │  ┌──────────────┐            │
│    Đài phun        │  │HC│TC│VC│ĐH│       │  │ 👴 Ông Sáu   │            │
│   (khô/có nước)    │  └──┴──┴──┴──┘       │  │ (Unaware)    │            │
│                    │  4 thùng phân loại    │  │ Ngồi câu cá  │            │
│  ┌──────────────┐  │                      │  └──────────────┘            │
│  │ 🧓 BÁC XANH │  │  👩‍🔧 Chị Lan        │                               │
│  │ Mentor chính │  │  (quản lý RC)        │  🟠 HOTSPOT: Riverside       │
│  │ Ghế đá       │  │                      │  🐟 Cá (C4) — bơi yếu       │
│  └──────────────┘  │  Sorting UI mở khi   │                              │
│                    │  bước vào RC         │  ≈ ≈ ≈ ≈ SÔNG ≈ ≈ ≈ ≈        │
│         │          │         │            │  ≈ ≈ ≈ ≈ ≈ ≈ ≈ ≈ ≈ ≈ ≈       │
├─────────┴──────────┴─────────┴────────────────────────────────────────────┤
│                                                                           │
│                         🚰 CỐNG THOÁT NƯỚC                                │
│                         PL ban đầu: 80 (CAO NHẤT)                         │
│                                                                           │
│              ┌──────────────────────────────────────┐                     │
│              │         CỐNG CHÍNH (bị tắc rác)       │                     │
│              │    . rác . rác . . rác . rác . .     │                     │
│              │    Nhặt sạch → Giữ E 3s thông cống   │                     │
│              └──────────────────────────────────────┘                     │
│                                                                           │
│              🔴 HOTSPOT: Drainage (ĐỎ) — Pollution Spread Event           │
│                                                                           │
│    ┌─────────────────────────────────────────────────────────┐           │
│    │  ⚠ Cảnh báo lần 1 (PL>75%): "Cống sắp tràn ra sông!"    │           │
│    │  🚨 Cảnh báo lần 2 (sau 2'): Rác tràn → Riverside +15 PL │           │
│    └─────────────────────────────────────────────────────────┘           │
│                                                                           │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 2. BẢN ĐỒ CHI TIẾT (DÀNH CHO DEV)

### 2.1 Kích thước & tỉ lệ Roblox

| Thông số | Giá trị |
|----------|---------|
| Tổng diện tích map | ~800 × 600 studs |
| Khu vực chơi được | 6 zone (Rừng cây chỉ visual) |
| Khoảng cách trung bình giữa 2 zone | ~100-150 studs |
| Trip dài nhất (Riverside ↔ Residential) | ~350 studs |
| Trip ngắn nhất (SQ ↔ RC) | ~60 studs |

### 2.2 Tọa độ từng khu vực (tham khảo)

| Khu vực | X | Y | Rộng | Cao |
|---------|---|---|------|-----|
| Rừng cây | 0 | 0 | 800 | 80 |
| Khu dân cư | 0 | 80 | 300 | 250 |
| Công viên / Picnic | 300 | 80 | 500 | 250 |
| Quảng trường | 0 | 330 | 220 | 180 |
| Trung tâm Tái chế | 220 | 330 | 240 | 180 |
| Bờ sông | 460 | 330 | 340 | 180 |
| Cống thoát nước | 0 | 510 | 800 | 200 |

### 2.3 Vị trí cụ thể

| Đối tượng | Khu vực | Tọa độ (X, Y) | Ghi chú |
|-----------|---------|---------------|---------|
| Spawn point | Quảng trường | (60, 355) | Hướng mặt về phía RC |
| Bác Xanh | Quảng trường | (120, 460) | Ghế đá cạnh đài phun nước |
| Đài phun nước | Quảng trường | (130, 420) | Khô → có nước theo tiến trình |
| Cô Tư | Khu dân cư | (150, 150) | Trước tiệm tạp hóa |
| Anh Tùng | Công viên | (400, 160) | Trên thảm picnic |
| Ông Sáu | Bờ sông | (540, 400) | Ghế gỗ cạnh sông, cần câu |
| Chị Lan | Trung tâm Tái chế | (340, 440) | Cạnh 4 thùng phân loại |
| Bé Na | Công viên | (520, 240) | Gần cây có chim |
| Cối xay gió | Công viên | (720, 160) | Landmark toàn map |
| Cây 1 | Công viên | (470, 220) | Cây có chim |
| Cây 2 | Công viên | (550, 200) | |
| Cây 3 (C5) | Rừng cây | (80, 25) | Đất trồng cây #1 |
| Cây 4 (C5) | Rừng cây | (680, 25) | Đất trồng cây #2 |
| Cây 5 (C5) | Bờ sông | (550, 370) | Gần Ông Sáu |
| Cây 6 (C5) | Công viên | (380, 130) | Gần thảm picnic |
| Cây 7 (C5) | Khu dân cư | (200, 250) | Gần tiệm Cô Tư |

---

## 3. ĐƯỜNG ĐI & GIAO THÔNG

### 3.1 Hệ thống đường mòn

```
Quảng trường ──▶ Trung tâm Tái chế ──▶ Công viên
     │                 │                    │
     │                 │                    │
     ▼                 ▼                    ▼
  Khu dân cư ◀──── Cống thoát nước ◀─── Bờ sông
```

### 3.2 Chi tiết từng tuyến đường

| Tuyến | Khoảng cách | Thời gian đi bộ | Màu đất | Ghi chú |
|-------|------------|----------------|---------|---------|
| SQ → RC | ~60 studs | ~4 giây | Gạch xám | Ngắn nhất |
| RC → Park | ~80 studs | ~5 giây | Đất nâu → Cỏ | Qua biển chỉ dẫn |
| RC → Residential | ~90 studs | ~6 giây | Đất nâu → Đất nâu | |
| Residential → Drainage | ~150 studs | ~9 giây | Đất nâu → Xám | Xuống dốc nhẹ |
| Park → Drainage | ~120 studs | ~7 giây | Cỏ → Xám | |
| RC → Riverside | ~100 studs | ~6 giây | Đất nâu → Cỏ | |
| Riverside → Drainage | ~80 studs | ~5 giây | Cỏ → Xám | Gần rãnh nước |
| SQ → Drainage | ~140 studs | ~8 giây | Gạch xám → Xám | |
| Riverside → Residential | ~350 studs | ~20 giây | Cross-map | Trip dài nhất |

### 3.3 Đường tắt (mở sau C3)

| Đường tắt | Mở khi | Kết nối | Tiết kiệm |
|-----------|--------|---------|-----------|
| Cầu gỗ bắc rãnh | Sau khi thông cống (C3) | Residential ↔ Riverside | ~100 studs |
| Đường mòn sau RC | Sau C3 | RC ↔ Park (không qua SQ) | ~30 studs |

### 3.4 Biển chỉ dẫn (Wayfinding v3)

| Vị trí | Nội dung biển |
|--------|---------------|
| Ngã ba SQ → RC / Park | "↑ Trung Tâm Tái Chế | → Công Viên | ← Khu Dân Cư" |
| Ranh giới SQ → Residential | "← Khu Dân Cư" |
| Ranh giới RC → Park | "→ Công Viên" |
| Ranh giới RC → Riverside | "→ Bờ Sông" |
| Gần cống | "⚠ Cống thoát nước — Nguy hiểm" |

---

## 4. HOTSPOT & MARKER MÀU

### 4.1 Danh sách hotspot

| Hotspot | Khu vực | Màu ban đầu | PL ban đầu | Mở khóa |
|---------|---------|------------|------------|---------|
| Picnic Area | Công viên | 🟠 Cam | 55 | C2A |
| Residential Street | Khu dân cư | 🟠 Cam | 60 | C2C |
| Drainage | Cống thoát nước | 🔴 Đỏ | 80 | C2C |
| Riverside | Bờ sông | 🟠 Cam | 50 | C2C (nếu cống tắc → 🔴) |

### 4.2 Hệ thống màu marker

| Màu | PL khu vực | Ý nghĩa | Hành động gợi ý |
|------|-----------|---------|-----------------|
| 🟡 Vàng | < 40 | Ô nhiễm nhẹ | Theo dõi |
| 🟠 Cam | 40–70 | Ô nhiễm trung bình | Nhặt rác + phân loại |
| 🔴 Đỏ | > 70 | Ô nhiễm nghiêm trọng | Ưu tiên xử lý ngay |
| ✅ Xanh | < 20 | Đã xử lý | Không cần can thiệp |

### 4.3 Phạm vi phát hiện (v3)

| Hành động | Phạm vi |
|-----------|---------|
| Scanner phát hiện hotspot | **50 studs** (tăng từ 15 — Friction Audit) |
| Nhặt rác | 5 studs |
| Đặt thùng rác (bán kính ảnh hưởng) | 25 studs |
| Đặt biển báo (bán kính ảnh hưởng) | 30 studs |
| Trồng cây (bán kính visual) | 15 studs |
| Cứu chim (bán kính dọn rác nhựa) | 15 studs |
| Cứu sóc (bán kính dọn rác độc hại) | 20 studs |

---

## 5. NPC VỊ TRÍ & PHẠM VI

| NPC | Vị trí cố định | Xuất hiện từ | Phạm vi di chuyển | Trạng thái |
|-----|---------------|-------------|-------------------|------------|
| Bác Xanh | Ghế đá cạnh đài phun, Quảng trường | C1 | Không di chuyển (trừ lúc dẫn đường C2B, C2C) | Luôn ở SQ |
| Cô Tư | Trước tiệm tạp hóa, Khu dân cư | C2 | Quanh tiệm (~15 studs) | Unaware → Aware → Considerate |
| Anh Tùng | Thảm picnic, Công viên | C2 | Quanh thảm (~20 studs) | Unaware → Aware → Considerate |
| Ông Sáu | Ghế câu cá, Bờ sông | C3 | Dọc bờ sông (~30 studs) | Unaware → Aware → Considerate |
| Chị Lan | Trong Trung tâm Tái chế | C2B | Trong RC (~20 studs) | Không đổi |
| Bé Na | Gần cây, Công viên | C2 | Quanh cây (~10 studs) | Không đổi |

---

## 6. LUỒNG DI CHUYỂN THEO CHAPTER

### Chapter 1
```
[SPAWN] → Nhặt 8 rác quanh SQ → Gặp Bác Xanh → Nhận Scanner
```
**Số trip:** 0 | **Phạm vi:** Nội bộ Quảng trường

### Chapter 2A
```
SQ → Park (tìm hotspot, nhặt rác, auto-disappear)
```
**Số trip:** 1 (SQ→Park) | **Về RC:** 0

### Chapter 2B
```
[Bác Xanh dẫn] RC (học sort 3 món mẫu) → Park (tự nhặt) → RC (tự sort)
```
**Số trip:** 2 (có follow) | **Về RC:** 1

### Chapter 2C
```
[Bác Xanh dẫn] Drainage → Residential → RC (sort) → Park (thấy rác quay lại)
```
**Số trip:** 3-4 | **Về RC:** 1-2

### Chapter 3 (Spatial Circuit)
```
SQ (nhận vật phẩm) → Residential (đặt thùng) → Drainage (nhặt + thông cống)
→ Riverside (đặt biển) → Park (đặt thùng) → RC (sort tất cả)
```
**Số trip:** 6 | **Về RC:** 1 (cuối circuit)

### Chapter 4
```
SQ → Park (cứu chim) → RC (sort rác nhựa) → Riverside (cứu cá)
→ [Drainage nếu bị gate] → Residential (cứu sóc) → RC (sort rác độc hại)
```
**Số trip:** 5-7 | **Về RC:** 2-3

### Chapter 5
```
SQ (nghe Bác Xanh) → Residential (Cô Tư) → Park (Anh Tùng)
→ Riverside (Ông Sáu) → Trồng cây rải rác → SQ (Ending)
```
**Số trip:** 4-5 | **Về RC:** 0

### Tổng kết toàn game

| Chapter | Số trip | Về RC | Thời gian (phút) |
|---------|---------|-------|-------------------|
| C1 | 0 | 0 | 5-8 |
| C2A | 1 | 0 | 3-4 |
| C2B | 2 | 1 | 4-5 |
| C2C | 3-4 | 1-2 | 4-5 |
| C3 | 6 | 1 | 10-15 |
| C4 | 5-7 | 2-3 | 10-15 |
| C5 | 4-5 | 0 | 10-15 |
| **Tổng** | **~23** | **~8-10** | **~55-70** |

---

## 7. CÁC LỚP VISUAL MAP

### 7.1 Layer 1: Nền (Ground)
- Màu nền khác nhau cho từng khu vực (gạch xám, đất nâu, cỏ xanh, nước)
- Giúp người chơi nhận biết zone transition không cần UI

### 7.2 Layer 2: Cấu trúc (Structures)
- Nhà dân (Residential): 3-5 căn đơn giản
- Tiệm tạp hóa (Cô Tư): 1 building + quầy hàng
- Đài phun nước (Square): centerpiece
- Trung tâm Tái chế: building có 4 thùng + băng chuyền
- Cối xay gió (Park): tall landmark
- Cống (Drainage): cấu trúc bê tông thấp
- Cây cối: rải rác, tăng theo ES

### 7.3 Layer 3: NPC & Interactive
- NPC với animation idle
- Rác (fixed + dynamic)
- Hotspot marker (khi bật Scanner)
- Prompt [E] cho tương tác

### 7.4 Layer 4: UI Overlay
- Minimap (góc trên trái, phím M toggle)
- HUD 3 chỉ số (ES / PL / CA)
- Quest tracker (góc trên phải)
- Inventory bar (dưới cùng)

---

## 8. MINIMAP (v3 — MỚI)

```
┌──────────────────────┐
│     RỪNG CÂY         │
│  [🌱]         [🌱]   │
│                      │
│  KDCư    │   CôngViên│  ← ● = Vị trí người chơi
│  🟠      │    🟠     │  ← Màu marker = hotspot
│          │           │
│  QuảngTrường│BờSông  │  ← 🟢 = Bác Xanh
│  🟢  │ RC │  🟠     │  ← ♻ = Trung tâm Tái chế
│      │  ♻  │         │
│  ───── Cống ─────    │  ← ~~~ = Sông
│       🔴             │
└──────────────────────┘
```

**Hiển thị:**
- Chấm trắng: vị trí người chơi
- Chấm xanh lá: Bác Xanh
- Icon thùng rác: Trung tâm Tái chế
- Mũi tên nhỏ: hướng người chơi đang nhìn
- Marker màu: hotspot (vàng/cam/đỏ/xanh)

---

## 9. THAY ĐỔI MAP TỪ v2 → v3

| # | Thay đổi | Audit nguồn | Impact |
|---|----------|------------|--------|
| 1 | **RC dời vào trung tâm** (hàng 3, giữa SQ và Riverside) | Friction Journey | Giảm ~25-30% tổng trip về RC |
| 2 | **Bờ sông kéo dài full hàng ngang** | Friction Journey | Nhân quả cống→sông trực quan hơn |
| 3 | **Cống full hàng dưới cùng** | Friction Journey | Kết nối visual với sông |
| 4 | **Biển chỉ dẫn tại ranh giới zones** | Friction Journey | Wayfinding cho trẻ 10-12t |
| 5 | **Cối xay gió làm landmark** | Friction Journey | Spatial anchor toàn map |
| 6 | **Scanner breadcrumb trail** | Friction Journey | Dẫn hướng mờ đến hotspot gần nhất |
| 7 | **Minimap** | Friction Journey | Xây dựng mental model bản đồ |
| 8 | **Màu đất khác biệt mỗi zone** | Friction Journey | Zone transition không cần UI |
| 9 | **Đường tắt sau C3** (cầu gỗ + đường mòn) | Friction Journey | Giảm ~20% thời gian đi bộ late game |
| 10 | **Scanner phạm vi 15→50 studs** | Friction Journey | Thực sự dẫn đường |

---

## 10. HƯỚNG DẪN BUILD MAP TRONG ROBLOX STUDIO

### 10.1 Quy trình

1. **Tạo Baseplate:** 800×600 studs, flat terrain
2. **Vẽ layout bằng Parts:** Dùng colored bricks để đánh dấu ranh giới 6 zone
3. **Terrain painting:** Sơn màu đất theo zone (gạch xám, đất nâu, cỏ, cát)
4. **Dựng structures:** Buildings → Fountain → RC → Windmill → Drainage
5. **Đặt props:** Ghế đá, thảm picnic, cây cối, thùng rác
6. **Path system:** Đường đất nối các zone
7. **NPC placement:** Spawn locations cho 6 NPC
8. **Rác spawner:** Fixed trash (tutorial) + Dynamic spawners
9. **Water:** Sông bằng transparent parts + flow animation
10. **Lighting:** Ánh sáng thay đổi theo ES (FutureTint màu)

### 10.2 Gợi ý asset Roblox Marketplace

| Cần | Từ khóa tìm |
|-----|------------|
| Nhà dân đơn giản | "house" "suburban" (free) |
| Cây | "tree" "oak" (free) |
| Đài phun nước | "fountain" "stone" |
| Thùng rác | "trash bin" "recycle bin" |
| Ghế đá | "bench" "park" |
| Cối xay gió | "windmill" "old" |
| Cống | "pipe" "drain" "sewer" |
| Biển báo | "sign" "wooden" |
| Cầu gỗ | "bridge" "wooden" |

---

*GREEN AGAIN v3 — Thị trấn Ven Sông — Map Documentation*
