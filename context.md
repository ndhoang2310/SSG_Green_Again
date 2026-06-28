# CONTEXT — Green Again (Thị trấn Ven Sông)

> **Lưu:** Tháng 6/2026
> **Phiên:** 5 audit + GDD v4 hoàn chỉnh
> **Trạng thái:** GDD v4 đã viết. Còn Flow Audit v4 doc + NPC Dialogue v4.

---

## 1. PROJECT LÀ GÌ

**Green Again** — Game Roblox giáo dục môi trường.
- **Target:** 10-16 tuổi, ~55-70 phút (3 buổi ~20 phút)
- **Core message:** Dọn rác chỉ là bước đầu. Cần hạ tầng + nguyên nhân + cộng đồng.
- **3 Pillars:** Nhân quả rõ ràng / Giáo dục tự nhiên / Không dead end
- **5 Chapter:** Khởi đầu → Tìm nguồn → Ngăn rác → Cứu sinh vật → Cộng đồng
- **Emotional core:** Earned Belonging — Sự gắn bó được vun đắp

---

## 2. 6 AUDIT ĐÃ CHẠY

| # | Audit | Kết quả chính |
|---|-------|---------------|
| 1 | **Emotional Canvas** | Chốt vibe "Earned Belonging", palette làng quê VN |
| 2 | **Flow Audit v4** | 3 breakpoint: C2B sorting, C3 circuit gãy, C4 flat zone. C5 end trip cải thiện 48% |
| 3 | **Peak-End Audit** | Chốt payoff: Nhà văn hóa sáng đèn + NPC tụ họp + cối xay gió quay |
| 4 | **FTUE Hero's Journey** | Spawn xa Bác Xanh = narrative tốt hơn. Cần opening hook 3s đầu |
| 5 | **Goal Density** | Session Mismatch critical. Cần chapter breaks C2/C4 |
| 6 | **Design Pillars** | Trích xuất pillar thứ 4: "Gắn bó được vun đắp". KHÔNG thêm fast travel, achievement, daily reward |

---

## 3. TÀI LIỆU HIỆN CÓ

| File | Nội dung | Trạng thái |
|------|----------|------------|
| `GDD_GreenAgain_v4.md` | GDD chính v4 — tích hợp toàn bộ map v4 + 3 thay đổi chính + 5 audit | ✅ Done |
| `GDD_GreenAgain_Map_v4.md` | Map kiểu VN: sông uốn lượn, đập 3 cống, Nhà văn hóa | ✅ Done |
| `GDD_GreenAgain_Friction_Audit_v4.md` | Friction audit cho map v4 | ✅ Done |
| `GDD_GreenAgain_Flow_Audit_v4.md` | Flow audit cho map v4 | ✅ Done |
| `GDD_GreenAgain_NPC_Dialogue_v4.md` | ~101 dòng thoại, cập nhật vị trí + chapter breaks + ending mới | ✅ Done |
| `GDD_GreenAgain_v2.md` | GDD v2 (có v3 changes inline) | 📦 Archive |
| `GDD_GreenAgain_v3_changes.md` | 3 thay đổi P0/P1 (C2 3-phase, Bác Xanh, Spill) | 📦 Đã tích hợp vào v4 |
| `GDD_GreenAgain_Flow_Audit_v3.md` | Flow audit v3 | 📦 Đã thay bởi v4 |
| `GDD_GreenAgain_Friction_Audit_v3.md` | Friction audit v3 | 📦 Đã thay bởi v4 |
| `GDD_GreenAgain_Map_v3.md` | Map cũ | 📦 Đã thay bởi v4 |
| `GDD_GreenAgain_NPC_Dialogue_v3.md` | ~91 dòng thoại cho 6 NPC | 📦 Đã thay bởi v4 |

### CHƯA CÓ:
- (Đã hoàn thành tất cả tài liệu core)

---

## 4. 3 THAY ĐỔI CHÍNH ĐÃ IMPLEMENT TRONG GDD v4

| # | Thay đổi | Audit nguồn | Dev cost |
|---|----------|------------|----------|
| 1 | **Chapter breaks cuối C2 và C4** | Flow + Goal Density + Friction | Thấp (2 câu thoại + fade) |
| 2 | **Nhà văn hóa sáng đèn** thay đài phun nước | Peak-End | Trung bình (lighting + NPC spawn) |
| 3 | **C4: gom rác cứu hộ, sort 1 lần** (inventory 8 ô tạm) | Flow + Friction | Trung bình (inventory exception) |

---

## 5. DECISIONS ĐÃ CHỐT

- [x] Map kiểu Việt Nam: sông uốn lượn + đập nước + nhà văn hóa
- [x] Bác Xanh → Nhà văn hóa (mái ngói đỏ)
- [x] Ông Sáu → bờ sông NE (gần mỏm đá)
- [x] Đập 3 cống thay cống đơn — Pollution Spread 3 giai đoạn
- [x] Spawn tách khỏi Bác Xanh (góc dưới trái)
- [x] Payoff ending: Nhà văn hóa sáng đèn + NPC tụ họp + cối xay gió quay (ES > 85)
- [x] C4: cá ở dưới chân đập
- [x] Chapter breaks cuối C2 và C4
- [x] C2B: thêm 2 món bán hướng dẫn (highlight 2s) trước khi thả tự do
- [x] C3: Nhà cô Tư có skip flag
- [x] C1: opening hook (text mờ + feedback món rác đầu)

---

## 6. CẦN LÀM TIẾP

1. **GDD_GreenAgain_Flow_Audit_v4.md** — Lưu kết quả Flow Audit thành file riêng
2. **GDD_GreenAgain_NPC_Dialogue_v4.md** — Cập nhật ~91 dòng thoại:
   - Sửa references "quảng trường", "bờ sông", "cống" → vị trí mới
   - Thêm thoại Bác Xanh cho chapter breaks (cuối C2, cuối C4)
   - Thêm thoại Bác Xanh cho ending mới (Nhà văn hóa sáng đèn)
   - Cập nhật vị trí NPC: Bác Xanh → Nhà văn hóa, Ông Sáu → NE, Chị Lan → NVH/RC
3. Cân nhắc chạy `game-design-fairness-frustration-audit` nếu cần

---

*Context saved — Tháng 6/2026*
