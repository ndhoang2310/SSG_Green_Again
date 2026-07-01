# GREEN AGAIN: ONE LIVING TOWN
## Game Design Document — Revised v2.0 + v3 (Audit Changes)

> **Nền tảng:** Roblox  
> **Thể loại:** Educational Simulation / Adventure  
> **Đối tượng:** 10–16 tuổi  
> **Thông điệp cốt lõi:** Dọn rác chỉ là bước đầu. Thị trấn xanh bền vững cần hạ tầng đúng, nguyên nhân được xử lý và cộng đồng thay đổi cùng nhau.

---

## ✂️ NHỮNG GÌ ĐÃ BỎ VÀ LÝ DO

Trước khi vào chi tiết, đây là các phần trong v1 đã được loại hoặc điều chỉnh:

| Phần bị loại/sửa | Lý do |
|---|---|
| **"Khu cứu động vật" là khu riêng biệt** | Không cần thiết. Động vật nằm rải rác trong các khu vực có sẵn là đủ tự nhiên hơn. |
| **Inventory limit bật ngay từ Chapter 2** | Nên bật từ đầu game nhưng với limit cao hơn (8 món), giảm dần sau khi tutorial xong (5 món). Bật đột ngột ở Chapter 2 làm gián đoạn flow. |
| **NPC "Active Helper" quét rác** | Animation quá phức tạp cho MVP Roblox. Thay bằng NPC đổi thoại và ngừng sinh rác — đơn giản hơn nhưng vẫn đủ ý nghĩa. |
| **Cây trồng yêu cầu Pollution < 30%** | Ngưỡng quá khắt khe, dễ gây frustration. Đổi thành < 50% và chỉ yêu cầu khu vực sạch rác, không cần toàn bộ thị trấn. |
| **Ending C có rác quay lại ngay trong cutscene** | Khó implement trong Roblox, dễ gây bug visual. Thay bằng UI thống kê + thoại kết thúc có sắc thái khác nhau. |
| **Phân loại sai gây +1 Pollution Level** | Quá phạt nặng trong game giáo dục. Phân loại sai chỉ không được điểm, không bị phạt ngược — khuyến khích thử sai. |
| **Mốc visual dựa 100% vào Environment Score** | Đổi thành dựa vào từng khu vực riêng lẻ. Quảng trường có thể xanh dù bờ sông vẫn đục — thực tế và hợp lý hơn. |

---

## PHẦN 1: TỔNG QUAN DỰ ÁN

### 1.1 Concept một câu

> Người chơi là tình nguyện viên môi trường đến một thị trấn đang ô nhiễm, phải phục hồi nó bằng cách dọn rác, xử lý nguyên nhân, cứu động vật và thuyết phục người dân thay đổi thói quen.

### 1.2 Vòng lặp gameplay tổng quát

```
PHÁT HIỆN ──► DỌN DẸP ──► XỬ LÝ NGUYÊN NHÂN ──► PHỤC HỒI
    ▲                                                    │
    └────────────── (kiểm tra lại bằng Scanner) ─────────┘
```

**Vòng ngắn (~2–5 phút):**  
Quét Scanner → thấy Hotspot → nhặt rác → phân loại → kiểm tra chỉ số

**Vòng dài (~30–60 phút toàn game):**  
Dọn rác → tìm nguyên nhân → đặt hạ tầng → cứu sinh vật → thuyết phục NPC → nhận ending

### 1.3 Ba cột trụ thiết kế

| Cột trụ | Ý nghĩa trong gameplay |
|---|---|
| **Nhân quả rõ ràng** | Mỗi hành động có phản hồi hữu hình. Bỏ mặc cống → sông bẩn hơn. Đặt thùng rác → rác sinh chậm hơn. |
| **Giáo dục tự nhiên** | Kiến thức về môi trường được nhúng vào feedback, không phải bài giảng. |
| **Không có dead end** | Người chơi không thể fail hoàn toàn — chỉ nhận ending khác nhau tùy chất lượng chơi. |

---

## PHẦN 2: BẢN ĐỒ THỊ TRẤN

> Game chỉ dùng **một thị trấn duy nhất**. Không có loading screen giữa các chapter. Chapter là trạng thái tiến trình, không phải map riêng.

### 2.1 Sơ đồ bố cục thị trấn

> ⚠️ **Thay đổi v3:** Trung tâm Tái chế được dời từ góc dưới phải vào trung tâm thật sự (giao điểm L-R, R2-R3) để giảm ~30% số lần chạy qua chạy lại. Xem Friction Journey Audit.

```
┌─────────────────────────────────────────────┐
│                  RỪNG CÂY                    │  ← Visual background, không vào được
│  [Khu đất trồng cây]   [Khu đất trồng cây]  │
├──────────────┬──────────────────────────────┤
│              │                              │
│  KHU DÂN CƯ │    CÔNG VIÊN / KHU PICNIC   │
│  (NPC sinh   │    (rác sinh hoạt, chim)    │
│   rác)       │                              │
├──────────────┼────────┬─────────────────────┤
│              │ TRUNG  │                     │
│  QUẢNG TRƯỜNG│  TÂM   │    BỜ SÔNG          │
│  TRUNG TÂM  │ TÁI CHẾ│    (cá, rác nổi,    │
│  (spawn,     │ (sort  │     nước đục)        │
│   Bác Xanh)  │  hub)  │                     │
├──────────────┴────────┴─────────────────────┤
│                                              │
│              CỐNG THOÁT NƯỚC                 │
│  (liên kết với sông — PL cao lan xuống sông)  │
│                                              │
└──────────────────────────────────────────────┘
```

**Cải thiện so với v2:**
- RC nằm giữa Quảng trường và Công viên/Khu dân cư — mọi trip từ bất kỳ khu vực nào đến RC đều ngắn hơn
- Bờ sông được kéo dài full hàng ngang phía dưới — tạo cảm giác "sông bao quanh", nhân quả cống→sông rõ hơn
- Cống thoát nước nằm full hàng dưới cùng, kết nối trực quan với bờ sông
- Đường đi từ Residential → RC và từ Park → RC gần như bằng nhau

### 2.2 Chi tiết từng khu vực

---

#### 🏛️ Quảng trường trung tâm
**Trạng thái ban đầu:** Xám, rác rải rác, cây héo, đường bị chặn  
**Trạng thái phục hồi:** Màu sắc tươi, cây xanh, NPC đi lại tự nhiên  

**Vai trò gameplay:**
- Spawn point của người chơi
- Tutorial nhặt rác, gặp NPC hướng dẫn
- Bị chặn bởi rác → mở ra sau khi dọn

**NPC ở đây:** Bác Xanh (mentor chính)

**Rác cố định:** 8 món chặn đường (không tái sinh, chỉ cho tutorial)

---

#### 🏘️ Khu dân cư
**Trạng thái ban đầu:** Vài NPC đi lại, có 2–3 NPC xả rác định kỳ  
**Trạng thái phục hồi:** NPC ngừng xả rác, có thể có animation bỏ rác vào thùng  

**Vai trò gameplay:**
- Nguồn rác tái sinh do hành vi NPC
- Vị trí thuyết phục NPC (Chapter 5)
- Đặt thùng rác và biển báo giảm spawn rate

**Hotspot:** Residential Street  
**Rác xuất hiện:** Vỏ bánh kẹo, hộp đồ ăn, chai nhựa nhỏ  
**Spawn Rate:** Cứ 3 phút sinh 2–3 món nếu NPC chưa thuyết phục, có thùng rác gần đó → giảm còn 1 món mỗi 5 phút

---

#### 🌳 Công viên / Khu picnic
**Trạng thái ban đầu:** Nhiều rác sinh hoạt, cỏ vàng, chim bị mắc túi nhựa  
**Trạng thái phục hồi:** Cỏ xanh, chim bay quanh, NPC picnic tự dọn  

**Vai trò gameplay:**
- Hotspot chính cho Chapter 2 (dạy phân loại)
- Vị trí cứu chim (Chapter 4)
- Đặt thùng rác giảm rác tái sinh
- Thuyết phục NPC picnic ngừng bỏ rác bừa

**Hotspot:** Picnic Area (mức cam)  
**Rác xuất hiện:** Chai nhựa, túi nilon, hộp xốp, vỏ chuối, giấy gói đồ  
**Spawn Rate:** Cứ 4 phút sinh 3–4 món nếu chưa có thùng rác

---

#### 🚰 Cống thoát nước
**Trạng thái ban đầu:** Rác bít miệng cống, có marker đỏ trên Scanner  
**Trạng thái phục hồi:** Nước chảy thông, không có rác tích tụ  

**Vai trò gameplay:**
- Hotspot có mức độ ô nhiễm cao nhất (đỏ)
- Nếu không xử lý → kích hoạt Pollution Spread Event đến bờ sông
- Điều kiện tiên quyết để cứu cá
- Người chơi phải nhặt sạch rác xung quanh VÀ giữ E để "thông cống" (3 giây)
  - **v3:** Hành động thông cống kích hoạt NGAY sau khi rác cuối cùng trong bán kính được nhặt — không cần quay lại Trung tâm Tái chế trước. Rác đã biến mất = cống đã sẵn sàng thông. Hành lý vẫn cần về RC để sort, nhưng việc thông cống không bị trì hoãn.

**Hotspot:** Drainage (mức đỏ)  
**Trigger Event:** Nếu Drainage Pollution > 75% trong hơn 5 phút game-time → hiện cảnh báo → rác xuất hiện thêm ở bờ sông

> ⚠️ **Lưu ý thiết kế:** Thông cống là hành động một lần duy nhất, không tái sinh. Sau khi thông xong, Drainage Pollution giảm về 0 và chỉ tăng nhẹ nếu có rác đổ vào từ khu dân cư.

---

#### 🌊 Bờ sông
**Trạng thái ban đầu:** Nước đục nhẹ, rác nổi, cá yếu  
**Trạng thái phục hồi:** Nước trong hơn, cá bơi lại, chim nước xuất hiện  

**Vai trò gameplay:**
- Thể hiện hậu quả của cống ô nhiễm (nhân quả rõ nhất trong game)
- Vị trí cứu cá (Chapter 4)
- Đặt biển báo gần đây giúp NPC hiểu liên kết rác → sông

**Hotspot:** Riverside (mức cam, có thể lên đỏ nếu cống tắc)  
**Rác xuất hiện:** Rác nổi tự động từ cống nếu không xử lý, không tự sinh ở bờ sông

---

#### ♻️ Trung tâm tái chế
**Vị trí:** Trung tâm bản đồ — giữa Quảng trường, Công viên và Khu dân cư  
**Trạng thái:** Không thay đổi visual theo tiến trình, luôn sẵn sàng  

**Vai trò gameplay:**
- Hub phân loại rác (mở UI Sorting khi vào)
- Người chơi phải đến đây để xử lý inventory
- Không có quá nhiều ý nghĩa gameplay sau Chapter 3 → người chơi sẽ biết rõ loại rác, việc phân loại trở nên nhanh hơn

> ⚠️ **Thay đổi v3:** RC được dời vào trung tâm bản đồ (giao điểm các khu vực chính). Khoảng cách từ Residential, Park, Square đến RC gần như bằng nhau. Giảm ~25-30% tổng số lần chạy qua chạy lại trong toàn bộ game.

---

#### 🌱 Khu đất trồng cây
**Vị trí:** 4–5 ô đất rải rác quanh thị trấn (công viên, khu dân cư, gần bờ sông)  
**Trạng thái ban đầu:** Đất nâu, không có cây, có thể có rác  
**Điều kiện mở:** Khu vực xung quanh không còn rác, Pollution Level khu đó < 50%  

**Vai trò gameplay:**
- Hành động phục hồi cuối cùng (Chapter 5)
- Tăng Environment Score mạnh (+5 mỗi cây)
- Thay đổi visual rõ nhất trong game

---

## PHẦN 3: BA CHỈ SỐ CHÍNH

### 3.1 Tổng quan chỉ số

```
ENVIRONMENT SCORE    ████████░░  45/100  ↑ (càng cao càng tốt)
POLLUTION LEVEL      ██████░░░░  62/100  ↓ (càng thấp càng tốt)  
COMMUNITY AWARENESS  ███░░░░░░░  30/100  ↑ (càng cao càng tốt)
```

> **Lưu ý quan trọng:** Ba chỉ số này **không phải là gương phản chiếu nhau**. Có thể Environment Score cao nhưng Community Awareness thấp (người chơi dọn nhiều nhưng không thuyết phục NPC), dẫn đến Ending B thay vì Ending A.

---

### 3.2 Environment Score (ES)

**Thang:** 0–100 | **Mục tiêu:** Tối đa hóa

#### Cách tăng ES:

| Hành động | Điểm tăng |
|---|---|
| Nhặt rác thông thường | +1 |
| Phân loại đúng | +2 |
| Phân loại đúng rác độc hại | +4 |
| Đặt thùng rác đúng vị trí (Good Location) | +5 |
| Đặt biển báo đúng vị trí | +3 |
| Làm sạch cống | +10 |
| Cứu động vật | +8 |
| Trồng cây | +5 |
| Thuyết phục NPC thành công | +5 |

#### Cách giảm ES:
- Để Pollution Spread Event xảy ra: -5
- Không xử lý Hotspot đỏ sau 10 phút game-time: -2 mỗi phút

#### Mốc visual theo ES (theo từng KHU VỰC, không phải toàn map):

| ES của khu vực | Visual khu vực đó |
|---|---|
| 0–30 | Xám, cây héo, nhiều rác |
| 31–55 | Bớt rác, cỏ vàng nhạt |
| 56–75 | Cỏ xanh nhạt, cây đứng thẳng |
| 76–89 | Cỏ xanh đậm, hoa nhỏ xuất hiện |
| 90–100 | Cây ra lá mới, ánh sáng ấm hơn, động vật xuất hiện |

---

### 3.3 Pollution Level (PL)

**Thang:** 0–100 | **Mục tiêu:** Giảm về thấp nhất có thể  
**Pollution Level được theo dõi riêng cho từng khu vực**, không chỉ một chỉ số chung.

#### Pollution Level của từng khu vực:

| Khu vực | PL ban đầu | PL mục tiêu |
|---|---|---|
| Quảng trường | 40 | < 10 |
| Khu dân cư | 60 | < 20 |
| Công viên | 55 | < 15 |
| Cống | 80 | < 10 |
| Bờ sông | 50 | < 20 |

#### Ngưỡng kích hoạt sự kiện:

| PL khu vực | Hậu quả |
|---|---|
| < 25 | Ổn định, không sinh thêm rác |
| 25–50 | Rác sinh bình thường |
| 51–75 | Rác sinh nhanh hơn 50% |
| > 75 | Cảnh báo, nếu là cống thì kích hoạt Pollution Spread Event |

---

### 3.4 Community Awareness (CA)

**Thang:** 0–100 | **Mục tiêu:** Tối đa hóa  
**CA ảnh hưởng trực tiếp đến Ending và tốc độ rác sinh lại.**

#### Cách tăng CA:

| Hành động | Điểm tăng |
|---|---|
| Thuyết phục NPC chọn đúng lựa chọn | +10 |
| Đặt biển báo trong bán kính 30 studs của NPC | +3 |
| Đặt thùng rác gần khu sinh hoạt (Good Location) | +2 |
| Hoàn thành quest giáo dục (nếu có) | +5 |

#### Ảnh hưởng của CA:

| CA | Hệ quả |
|---|---|
| 0–30 | NPC xả rác bình thường, rác tái sinh nhanh |
| 31–60 | NPC trung lập, rác tái sinh bình thường |
| 61–80 | NPC ngừng xả rác, rác tái sinh chậm |
| 81–100 | NPC bỏ rác vào thùng, rác hầu như không tái sinh |

---

## PHẦN 4: CÁC HỆ THỐNG GAMEPLAY

### 4.1 Hệ thống Nhặt rác

**Trigger:** Đến gần rác → hiện prompt `[E] Nhặt rác`  
**Thời gian:** Nhặt tức thì (không có animation dài)  
**Phạm vi:** 5 studs

#### Phân loại rác:

| Loại | Ví dụ | Thùng xử lý | Điểm ô nhiễm |
|---|---|---|---|
| Hữu cơ | Vỏ chuối, lá mục, hộp cơm còn thức ăn | Thùng xanh lá | 1 |
| Tái chế | Chai nhựa, lon, giấy, hộp carton sạch | Thùng xanh dương | 1 |
| Vô cơ | Hộp xốp, túi nilon bẩn, tã | Thùng vàng | 1 |
| Độc hại | Pin cũ, bóng đèn vỡ, chai hóa chất | Thùng đỏ | 3 |

#### Rác cố định vs. rác động:

- **Rác cố định:** Chỉ xuất hiện một lần, không tái sinh. Dùng trong tutorial và cutscene điều kiện (rác quanh chim, rác ở cống).
- **Rác động:** Tái sinh theo Spawn Rate, giảm khi đặt thùng rác hoặc thuyết phục NPC.

---

### 4.2 Hệ thống Inventory

**Ngay từ đầu game:** Túi có 5 ô  
**Tutorial:** 3 món rác đầu tiên không cần quản lý inventory (rác tự biến sau khi nhặt, để người chơi học flow)  
**Từ bước 4 trở đi:** Inventory bật đầy đủ

```
┌─────────────────────────────────┐
│  🗑️ Túi rác: ■ ■ ■ □ □  (3/5)  │
│  [Chai nhựa] [Vỏ chuối] [Pin]   │
└─────────────────────────────────┘
```

**Khi túi đầy:**
> 💬 "Túi rác đã đầy! Đến khu tái chế để phân loại trước nhé."

**Vì sao giữ limit ở 5?**  
Buộc người chơi phải quay lại Trung tâm Tái chế thường xuyên → nhịp gameplay rõ ràng, sorting system có ý nghĩa thật.

---

### 4.3 Eco Scanner

**Mở khóa:** Cuối Chapter 1  
**Phím:** `Q` để toggle bật/tắt  
**Trạng thái bật:** Màn hình có filter xanh nhẹ, marker nổi trên các Hotspot

#### Màu marker:

| Màu | PL khu vực | Ý nghĩa |
|---|---|---|
| 🟡 Vàng | < 40 | Ô nhiễm nhẹ |
| 🟠 Cam | 40–70 | Ô nhiễm trung bình |
| 🔴 Đỏ | > 70 | Ô nhiễm nghiêm trọng |
| ✅ Xanh | < 20 | Đã xử lý |

**Thông tin hiện khi đến gần Hotspot (trong bán kính 50 studs):**

> ⚠️ **Thay đổi v3:** Tăng phạm vi phát hiện hotspot từ 15 → 50 studs (theo Friction Journey Audit). Ở 15 studs người chơi phải vào đúng zone mới thấy marker — vô dụng cho navigation. Ở 50 studs, marker xuất hiện khi đang di chuyển giữa các zone, thực sự dẫn đường.

```
┌─────────────────────────────┐
│  📍 Cống thoát nước         │
│  Ô nhiễm: Cao  🔴           │
│  Nguyên nhân: Rác bít cống  │
│  ⚠️ Cảnh báo: Có thể lan    │
│     xuống sông nếu để lâu  │
└─────────────────────────────┘
```

---

### 4.4 Sorting System (Phân loại rác)

**Trigger:** Bước vào Trung tâm Tái chế với inventory có rác  
**Giao diện:**

```
┌──────────────────────────────────────────┐
│  🗂️ PHÂN LOẠI RÁC                       │
│                                          │
│  [1] Chai nhựa Aqua        →  ❓         │
│  [2] Vỏ chuối               →  ❓         │
│  [3] Pin cũ                 →  ❓         │
│                                          │
│  🟢 Hữu cơ  🔵 Tái chế  🟡 Vô cơ  🔴 Độc hại │
└──────────────────────────────────────────┘
```

**Feedback khi đúng:**
> ✅ "Đúng rồi! Chai nhựa có thể tái chế, giúp giảm rác thải."

**Feedback khi sai:**

> ❌ "Chưa đúng. Pin cũ chứa hóa chất độc hại, phải xử lý đặc biệt — không bỏ chung với rác thông thường."

**Hiệu ứng Spill khi sai (v3 — mới):**

```
Khi chọn sai thùng, ngoài text feedback, hệ thống kích hoạt hiệu ứng "spill":

1. Rác trong UI "rơi ra" khỏi thùng sai
2. Vệt bẩn xuất hiện trên sàn Trung tâm Tái chế:
   - Decal tròn, bán kính ~2 studs
   - Màu theo loại rác: nâu (hữu cơ) / xám (tái chế) / vàng (vô cơ) / đỏ (độc hại)
   - Particle nhỏ (3-5 hạt) rơi xuống
   - Âm thanh "tách" nhẹ
   - Thời gian animation: 0.5 giây
3. Prompt hiện trên vệt bẩn: [E] Dọn sạch — giữ E 1 giây để xóa
   - Có thể dọn ngay hoặc để lại
   - Dọn spill không được điểm
4. Sorting UI mở lại → người chơi chọn lại thùng đúng
   - Khi sort ĐÚNG: tất cả vệt bẩn tồn đọng tự động biến mất

Quy tắc tích tụ:
- 1-2 vệt: không ảnh hưởng
- 3-4 vệt: Bác Xanh nhắc nhẹ 💬 "Cẩn thận cháu nhé, phân loại sai làm bẩn khu tái chế."
- 5+ vệt: Visual Trung tâm Tái chế hơi xám đi nhẹ (thuần visual, không ảnh hưởng gameplay)

Reset tự động: Tất cả vệt bẩn biến mất khi rời Trung tâm > 30 giây HOẶC sort đúng liên tiếp 3 lần.
```

**Điểm tính:**
- Đúng: +2 ES, -2 PL khu vực tương ứng
- Đúng rác độc hại: +4 ES, -4 PL
- Sai: Không được điểm, không bị phạt → hiệu ứng spill (visual, dọn 1 giây) → thử lại ngay

> ⚠️ **Thay đổi so với v1:** Không phạt ngược (-PL) khi sai. Game giáo dục nên khuyến khích thử, không sợ sai.
> ⚠️ **Thay đổi v3:** Thêm hiệu ứng spill khi sai — tạo nhân quả visual (sai = bẩn, đúng = sạch) mà không phạt điểm. Dọn spill mất 1 giây, không chặn tiến trình. Khôi phục Pillar 1 (Nhân quả rõ ràng) trong sorting loop.

---

### 4.5 Placement System (Đặt hạ tầng)

**Vật phẩm có thể đặt:**

| Vật phẩm | Ảnh hưởng | Bán kính |
|---|---|---|
| Thùng rác | Giảm Spawn Rate 50% trong vùng | 25 studs |
| Biển cấm xả rác | Tăng CA +3, NPC trong vùng có thoại mới | 30 studs |
| Cây xanh (Chapter 5) | Tăng ES +5, cải thiện visual | 15 studs |

**Cách đặt:**
1. Mở item trong inventory
2. Model preview xuất hiện dưới chân nhân vật
3. Vòng tròn ảnh hưởng hiện trên mặt đất
4. Vòng đổi màu theo vị trí
5. Click để đặt

**Hệ thống feedback vị trí:**

| Trạng thái vòng | Màu | Ý nghĩa | Điểm |
|---|---|---|---|
| Good Location | 🟢 Xanh | Đặt tốt, ảnh hưởng mạnh | +5 ES |
| Low Impact | 🟡 Vàng | Đặt được, hiệu quả thấp | +1 ES |
| Invalid | 🔴 Đỏ | Không thể đặt (dưới nước, trên đường...) | Không đặt được |

**Ví dụ feedback Good Location:**
> 💬 "Vị trí tốt! Thùng rác ở đây sẽ giúp giảm rác khu picnic đáng kể."

**Ví dụ feedback Low Impact:**
> 💬 "Hơi xa khu người hay tụ tập. Thùng rác sẽ ít được dùng hơn."

> ⚠️ **Thiết kế quan trọng:** Không yêu cầu đặt đúng một điểm duy nhất. Hệ thống chấm dựa trên vùng ảnh hưởng. Như vậy gameplay linh hoạt, không cảm giác bị railroaded.

---

### 4.6 NPC Behaviour System

> 📖 **Hội thoại đầy đủ của tất cả NPC:** xem file `GDD_GreenAgain_NPC_Dialogue_v3.md` (~91 dòng thoại cho 6 NPC + hệ thống).

**Danh sách NPC:**

| NPC | Tên | Vị trí | Tính cách | Vai trò |
|-----|-----|--------|-----------|---------|
| Bác Xanh | Nguyễn Xanh, ~60t | Quảng trường | Ấm áp, kiên nhẫn, hoài niệm | Mentor chính xuyên suốt 5 chapter |
| Cô Tư | Tư, ~45t | Khu dân cư | Vội vàng, thực dụng, "việc nhỏ không đáng bận tâm" | NPC thuyết phục #1 — xả rác theo thói quen |
| Anh Tùng | Tùng, ~22t | Khu picnic | Vô tư, ỷ lại, "sẽ có người dọn" | NPC thuyết phục #2 — để rác sau picnic |
| Ông Sáu | Sáu, ~65t | Bờ sông | Chân chất, bảo thủ, không hiểu hệ sinh thái | NPC thuyết phục #3 — không hiểu rác trên bờ → sông |
| Chị Lan | Lan, ~28t | Trung tâm Tái chế | Chuyên nghiệp, thân thiện | NPC phụ — hướng dẫn sorting, phản ứng streak |
| Bé Na | Na, ~8t | Công viên | Tò mò, hồn nhiên, yêu động vật | NPC phụ — tạo đồng cảm với chim & sóc |

**Các trạng thái NPC:**

```
UNAWARE ──(thuyết phục đúng)──► AWARE ──(đặt thùng gần)──► CONSIDERATE
   │                                                              │
   └── (thuyết phục sai / không làm gì) ──────────────────────────┘
         (tiếp tục xả rác, rác tái sinh bình thường)
```

| Trạng thái | Hành vi | Spawn rác |
|---|---|---|
| Unaware | Xả rác, nói thờ ơ | Bình thường |
| Aware | Ngừng xả rác, nói tích cực hơn | Giảm 70% |
| Considerate | Ngừng xả rác, bỏ rác vào thùng (animation đơn giản) | 0% |

**Hội thoại dạng lựa chọn:**  
Mỗi NPC có 3 lựa chọn thoại. Chỉ 1 lựa chọn tốt nhất. Các lựa chọn còn lại không phạt nặng mà chỉ CA tăng ít hơn — người chơi được thử lại.

---

### 4.7 Animal Rescue System

**Nguyên tắc cốt lõi:** Không cứu được ngay lập tức. Phải dọn môi trường trước.

| Động vật | Vị trí | Vấn đề | Điều kiện cứu | Sau khi cứu |
|---|---|---|---|---|
| 🐦 Chim | Công viên, gần cây | Mắc túi nhựa | Nhặt sạch rác nhựa trong bán kính 15 studs | Chim bay lên, xuất hiện trên cây khi ES công viên > 70 |
| 🐟 Cá | Bờ sông | Nước bẩn, cá yếu | Drainage PL < 30 VÀ Riverside PL < 45 | Cá bơi lại, thêm cá nhỏ xuất hiện ở bờ sông |
| 🐿️ Sóc | Gần khu dân cư, cạnh bụi rác | Rác độc hại xung quanh | Nhặt toàn bộ rác độc hại trong bán kính 20 studs, phân loại đúng | Sóc chạy lên cây, xuất hiện thêm sóc ở công viên |

**Feedback khi chưa đủ điều kiện:**
> 💬 (cá) "Nước sông vẫn còn quá bẩn. Hãy xử lý cống trước để nước sạch hơn."

**Reward khi cứu:**
- +8 ES
- Unlock visual: động vật xuất hiện thêm trong khu vực liên quan

---

### 4.8 Pollution Spread Event System

**Trigger:** Drainage PL > 75% trong hơn 5 phút game-time mà chưa được xử lý

**Diễn biến:**

```
Cảnh báo lần 1 (PL cống 75%):
💬 "Cảnh báo: Cống đang bị tắc nghiêm trọng. Rác có thể tràn ra sông!"

  ↓ (2 phút không xử lý)

Cảnh báo lần 2:
💬 "Cống đã tràn. Rác đang chảy ra bờ sông..."
→ Rác mới xuất hiện ở Riverside (+3–5 món)
→ Riverside PL tăng +15
→ Cá trở nên khó cứu hơn (yêu cầu Riverside PL phải thấp hơn)

  ↓ (Xử lý cống bất kỳ lúc nào)

Cống sạch → Riverside không nhận thêm rác từ cống
```

**Mục đích của Event này:**
- Không phải để phạt người chơi nặng nề
- Để cho người chơi *trải nghiệm hậu quả* của việc bỏ mặc vấn đề
- Tạo cảm giác thị trấn là "living world", không tĩnh

---

## PHẦN 5: THIẾT KẾ TỪNG CHAPTER

---

### 📘 CHAPTER 1: KHỞI ĐẦU

**Thời gian dự kiến:** 5–8 phút  
**Mục tiêu học:** Nhặt rác, di chuyển, tương tác NPC, nhận Scanner  
**Chỉ số lúc bắt đầu:** ES 10, PL 70, CA 0

#### Flow nhiệm vụ:

```
SPAWN ──► Thấy rác chặn đường ──► Nhặt 8 món rác (không cần phân loại)
  ──► Đường mở, gặp Bác Xanh ──► Nghe giải thích 3–4 câu ngắn
  ──► Nhận Eco Scanner ──► Thử Scanner, thấy marker đầu tiên ở công viên
  ──► Chapter 1 hoàn thành
```

**Hội thoại Bác Xanh (v3 — thêm kết nối cảm xúc, mentor có hồn):**

> *[Bác Xanh quay lại, mỉm cười]*
>
> "Chà! Cháu là tình nguyện viên mới mà hội đồng thị trấn gửi đến phải không? Bác là Bác Xanh — bác đã sống ở thị trấn Ven Sông này từ hồi nó còn xanh mướt, chim hót đầy công viên, cá bơi đầy sông..."
>
> *[Nhìn quanh quảng trường]*
>
> "Giờ thì nhìn quanh đi — xám xịt, rác ngập đường. Mà cháu vừa dọn sạch cả quảng trường một mình đấy! Nhanh thật! Cảm ơn cháu."
>
> *[Giọng trầm xuống]*
>
> "Nhưng bác phải nói thật với cháu: rác sạch hôm nay, ngày mai lại đầy. Không phải tại cháu đâu — mà tại mấy cái cống bị tắc đằng kia, tại mấy người dân chưa hiểu rác của họ đi đâu về đâu. Dọn rác là bước đầu — nhưng chỉ là bước đầu thôi."
>
> *[Rút Eco Scanner ra, đưa về phía người chơi]*
>
> "Bác có cái này — Máy Quét Sinh Thái. Nó sẽ cho cháu thấy những thứ mắt thường không thấy: chỗ nào ô nhiễm nặng nhất, nguyên nhân từ đâu. Hồi xưa bác dùng nó để giữ cho thị trấn luôn xanh. Giờ đến lượt cháu. Cháu muốn thử không?"
>
> *[Người chơi nhận Scanner — hiệu ứng UI: màn hình flash xanh nhẹ, Scanner xuất hiện trong tay nhân vật, icon Q hiện ở góc]*
>
> "Bấm Q để bật máy quét. Đi về phía công viên đằng kia đi — máy sẽ đổi màu khi cháu đến gần điểm ô nhiễm. Có gì không hiểu thì quay lại đây, bác luôn ở quảng trường này."

> ⚠️ **Thay đổi v3:** Hội thoại được viết lại hoàn toàn — Bác Xanh có tên tuổi, lịch sử, công nhận hành động người chơi, Scanner là quà tặng không phải giao dịch. Tạo kết nối cảm xúc trước khi vào gameplay.

**Unlock sau Chapter 1:**
- Eco Scanner (phím Q)
- UI hiện 3 chỉ số
- Công viên và khu dân cư có thể đến thăm dò

**Lưu ý thiết kế:**
- Inventory limit chưa kích hoạt đầy đủ trong Chapter 1 (không cần quay lại tái chế)
- Rác Chapter 1 biến mất sau khi nhặt, không cần phân loại — đây là onboarding, không phải gameplay

---

### 📗 CHAPTER 2: TÌM NGUỒN Ô NHIỄM

**Thời gian dự kiến:** 11–14 phút  
**Mục tiêu học:** Dùng Scanner, quản lý inventory, phân loại rác  
**Chỉ số lúc bắt đầu:** ES 25, PL 65, CA 5

> ⚠️ **Thay đổi v3:** Chapter 2 được chia thành 3 mini-phase (A/B/C) để tránh vách đá độ phức tạp. Mỗi phase mở khóa 1-2 hệ thống mới thay vì 4 hệ thống cùng lúc.

---

#### Phase 2A: Làm quen Scanner (3–4 phút)

**Hệ thống mở khóa:** Eco Scanner chủ động  
**Chưa mở:** Inventory limit, Sorting system, Dynamic spawn (rác vẫn auto-disappear)

**Flow:**
```
Bác Xanh:
💬 "Máy quét sẽ cho cháu thấy những điểm ô nhiễm mà mắt thường không thấy.
    Đi về phía công viên đi — máy sẽ tự đổi màu khi cháu đến gần."

Objective 2A: Dùng Scanner tìm Hotspot đầu tiên
  → Đi bộ đến Picnic Area (công viên)
  → Bật Scanner (Q) — thấy marker cam đầu tiên
  → Đến gần marker → UI hotspot info hiện lên:
    ┌─────────────────────────────┐
    │  📍 Khu Picnic              │
    │  Ô nhiễm: Trung bình  🟠    │
    │  Nguyên nhân: Rác sinh hoạt │
    └─────────────────────────────┘
  → Scanner tutorial popup ngắn: "🟡 Vàng = nhẹ | 🟠 Cam = trung bình | 🔴 Đỏ = nghiêm trọng"
  → Nhặt 3-4 món rác trong bán kính hotspot (rác auto-disappear, chưa vào inventory)

Hoàn thành → Bác Xanh khen:
💬 "Tốt lắm! Cháu thấy chưa — có những chỗ bẩn hơn mắt thường thấy."
```

---

#### Phase 2B: Học phân loại (4–5 phút)

**Hệ thống mở khóa:** Inventory 5 ô + Sorting system  
**Chưa mở:** Dynamic spawn  
**Giữ lại:** Scanner

**Flow:**
```
Bác Xanh:
💬 "Giờ cháu đã biết tìm rác ở đâu. Nhưng nhặt lên rồi — vứt đi đâu?
    Mỗi loại rác cần được xử lý khác nhau. Bác sẽ chỉ cho cháu."

→ Bác Xanh dẫn người chơi đến Trung tâm Tái chế (đi trước, người chơi follow)

Tại Trung tâm Tái chế:
  → Inventory limit kích hoạt (5 ô) — tutorial popup nhỏ: "Túi của cháu chứa được 5 món"
  → Bác Xanh đưa 3 món rác mẫu (1 hữu cơ, 1 tái chế, 1 vô cơ)
  → Mở Sorting UI — highlight đúng thùng cho từng món (1 giây delay)
  → Mỗi lần đúng: feedback ngắn + giải thích phân loại

Sau khi sort xong 3 món mẫu:
💬 "Giờ cháu thử tự làm nhé. Ra công viên nhặt thêm ít rác rồi quay lại đây."

Objective 2B: Tự nhặt rác → inventory đầy → quay lại Trung tâm → tự sort
  → Lần đầu mỗi loại rác MỚI: vẫn auto-highlight 1 giây
  → Từ lần 2 trở đi: tự chọn không gợi ý
```

---

#### Phase 2C: Đối mặt thực tế (4–5 phút)

**Hệ thống mở khóa:** Full 3 hotspot + Dynamic Trash Spawn  
**Giữ lại:** Tất cả hệ thống phase trước

**Flow:**
```
Scanner cập nhật: hiện 2 marker mới
  → Residential Street (🟡 vàng/cam)
  → Drainage (🔴 đỏ)

Bác Xanh:
💬 "Còn 2 điểm ô nhiễm nữa. Và cháu nên biết — rác sẽ không đứng yên mãi.
    Ở những nơi người dân chưa ý thức, rác sẽ xuất hiện trở lại."

→ Bác Xanh dẫn người chơi đến Drainage trước (đi trước, người chơi follow — giống C2B):
💬 "Cái cống này là chỗ ô nhiễm nặng nhất. Nó đỏ trên máy quét là có lý do —
    nếu bỏ mặc, rác sẽ theo nước tràn ra sông. Nhớ chỗ này, cháu sẽ phải quay lại."

→ Sau đó người chơi tự do tìm Residential Street và các hotspot còn lại

Objective 2C: Tìm và dọn sạch cả 3 hotspot
  → Residential Street (vàng/cam) — nhặt rác, inventory loop
  → Drainage (đỏ) — nhặt rác xung quanh, không cần thông cống ngay
  → Picnic Area (đã dọn trước đó — nhưng giờ rác ĐÃ quay lại một ít!)

  → Khi thấy rác quay lại ở công viên:
  💬 "Cháu thấy không? Rác đã quay lại. Dọn mà không ngăn nguyên nhân thì sẽ phải dọn mãi."

→ Dynamic spawn chính thức active trên toàn bản đồ
→ Inventory loop đầy đủ: nhặt → đầy → về tái chế → sort → quay lại

Chapter 2 hoàn thành: mở Chapter 3
```

**Unlock sau Chapter 2:**
- Sorting system đầy đủ
- Hotspot system active (3/3 đã xác định)
- Rác động bắt đầu tái sinh ở tất cả Hotspot chưa xử lý triệt để

#### So sánh C2 cũ vs mới:

| Tiêu chí | C2 cũ (v2) | C2 mới (v3) |
|---|---|---|
| Số hệ thống kích hoạt cùng lúc | 4 | 1-2 mỗi phase |
| Có tutorial sorting có người hướng dẫn? | Chỉ highlight tự động | Có 3 món mẫu + Bác Xanh hướng dẫn |
| Khi nào dynamic spawn bắt đầu? | Ngay đầu C2 | Cuối C2, sau khi đã hiểu sorting |
| Cảm giác "bị úp" hệ thống | Có | Không — mỗi phase là một bước nhỏ |

---

### 📙 CHAPTER 3: NGĂN RÁC QUAY LẠI

**Thời gian dự kiến:** 10–15 phút  
**Mục tiêu học:** Placement system, xử lý cống, hiểu nhân quả dài hạn  
**Chỉ số lúc bắt đầu:** ES 40, PL 55, CA 10

#### Flow nhiệm vụ (v3 — sắp xếp theo spatial circuit):

> ⚠️ **Thay đổi v3:** Objectives được sắp xếp thành một vòng tròn khép kín (Square → Residential → Drainage → Riverside → Park → RC) thay vì danh sách ngẫu nhiên. Giảm zig-zag không cần thiết.

```
Nhận 3 thùng rác + 2 biển báo từ Bác Xanh tại Quảng trường

  ↓

[1] KHU DÂN CƯ: Đặt thùng rác + nhặt rác
  → Đặt 1 thùng rác gần khu dân cư (gợi ý Good Location)
  → Quan sát Spawn Rate giảm

  ↓

[2] CỐNG THOÁT NƯỚC : Nhặt rác + thông cống
  → Nhặt 5–7 món rác quanh cống
  → Khi sạch → giữ E 3 giây thông cống (không cần về RC)
  → Drainage PL giảm mạnh
  → Cảnh báo Pollution Spread Event biến mất

  ↓

[3] BỜ SÔNG: Đặt biển báo
  → Đặt 2 biển báo gần bờ sông (gần NPC Ông Sáu hoặc điểm quan trọng)
  → CA tăng, NPC có thoại phản ứng

  ↓

[4] CÔNG VIÊN: Đặt thùng rác + nhặt rác
  → Đặt 1 thùng rác gần khu picnic
  → Nhặt rác còn tồn đọng → inventory loop

  ↓

[5] TRUNG TÂM TÁI CHẾ: Sort toàn bộ inventory
  → Về RC sort tất cả rác thu được trong circuit

  ↓

Eco Scanner cập nhật: Picnic Area → Low, Drainage → xanh
Bác Xanh:
💬 "Đó mới là xử lý đúng cách. Thùng rác để rác có chỗ về. Biển báo để người ta nhớ.
    Thông cống để nước không ứ đọng. Giờ thị trấn có thể tự duy trì tốt hơn rồi —
    ít nhất là một thời gian."

Chapter 3 hoàn thành
```

**Bác Xanh — Phản ứng khi Pollution Spread Event kích hoạt trong C3:**

```
Cảnh báo lần 1 (PL cống đạt 75%):
💬 "Cháu ơi! Cái cống đằng kia — bác vừa thấy nước bắt đầu tràn.
    Nếu không thông sớm, rác sẽ theo nước chảy hết ra sông.
    Con cá dưới đó không chịu nổi đâu."

Cảnh báo lần 2 (rác đã tràn ra sông):
💬 "Muộn mất rồi... Rác đã ra đến bờ sông.
    Giờ cháu phải dọn thêm ở bờ sông nữa.
    Lần sau nhớ xử lý cống sớm hơn nhé."
```

**Thứ tự Objective:**  
Không bắt buộc theo thứ tự cố định. Người chơi có thể thông cống trước, đặt thùng sau — miễn đủ 3 objective là xong Chapter 3.

**Unlock sau Chapter 3:**
- Thông cống → Riverside PL không tăng thêm
- Bờ sông trở nên có thể tiếp cận để cứu cá (nếu PL đủ thấp)
- Placement system unlocked đầy đủ

---

### 📕 CHAPTER 4: CỨU SINH VẬT

**Thời gian dự kiến:** 10–15 phút  
**Mục tiêu học:** Environmental gating, hậu quả ô nhiễm lên sinh vật  
**Chỉ số lúc bắt đầu:** ES 55, PL 40, CA 20

#### Flow nhiệm vụ:

```
Eco Scanner hiện tín hiệu mới:
Bác Xanh:
💬 "Cháu có thấy tín hiệu mới trên máy quét không? Đó là động vật — chim, cá, sóc —
    chúng vẫn còn sống trong thị trấn này! Nhưng tín hiệu yếu lắm, nghĩa là chúng đang
    gặp nguy hiểm. Cứu được con nào hay con ấy, cháu nhé."
→ 3 marker mới: chim (công viên), cá (bờ sông), sóc (khu dân cư)

  ↓

Nhiệm vụ song song — người chơi tự chọn thứ tự:

[A] Cứu chim:
  → Đến công viên → thấy chim mắc túi nhựa
  → Nhặt rác nhựa trong bán kính 15 studs (6–8 món)
  → Phân loại → quay lại → E để cứu
  → Chim bay lên ✓

[B] Cứu cá:
  → Đến bờ sông → thấy cá bơi yếu
  → Kiểm tra: Drainage PL và Riverside PL
  → Nếu cống chưa thông → nhắc quay lại thông cống
  → Nếu đủ điều kiện → E để cứu
  → Cá bơi lại ✓

[C] Cứu sóc:
  → Đến khu dân cư → thấy sóc gần đống rác độc hại
  → Nhặt 4–5 món rác độc hại, phân loại vào thùng đỏ
  → Quay lại → E để cứu
  → Sóc chạy lên cây ✓

  ↓

Sau khi cứu đủ 3 con:
→ ES tăng mạnh (+24)
→ Động vật bắt đầu xuất hiện tự nhiên trong khu vực liên quan
→ Visual map rõ ràng hơn

Bác Xanh (sau khi cứu con đầu tiên):
💬 "Cháu cứu được nó rồi! Hồi xưa công viên này đầy chim, sông đầy cá...
    Bác cứ tưởng chúng đi hết rồi. Cảm ơn cháu."

Bác Xanh (sau khi cứu con thứ hai):
💬 "Một con nữa! Cháu có tin được không — ngày hôm qua bác còn nghĩ
    thị trấn này hết cứu được rồi."

Bác Xanh (sau khi cứu cả ba):
💬 "Ba con... Cháu cứu được cả ba con. Ngày cháu đến, bác chỉ mong cháu
    dọn được cái quảng trường thôi. Mà giờ thì... chim bay lại rồi, cá bơi
    lại rồi, sóc chạy trên cây. Cảm ơn cháu. Thật lòng đấy."

Chapter 4 hoàn thành
```

**Nếu Pollution Spread Event đã xảy ra trước Chapter 4:**  
Cá sẽ khó cứu hơn (Riverside PL cần < 35 thay vì < 45). Đây là hậu quả tự nhiên, không phải fail state — người chơi vẫn có thể cứu, chỉ cần dọn thêm bờ sông.

---

### 📒 CHAPTER 5: CỘNG ĐỒNG VÀ KẾT THÚC

**Thời gian dự kiến:** 10–15 phút  
**Mục tiêu học:** Dialogue system, cộng đồng là yếu tố bền vững, trồng cây  
**Chỉ số lúc bắt đầu:** ES 70–75, PL 30, CA 20–30

#### Flow nhiệm vụ:

```
Bác Xanh:
💬 "Thị trấn đã sạch hơn nhiều. Bác đi dạo quanh hồi sáng — công viên xanh, sông cũng trong hơn trước. Nhưng cháu thấy không..."

*[Chỉ tay về phía khu dân cư]*

💬 "Mấy người dân đằng kia — họ vẫn chưa thay đổi thói quen. Cô Tư thì vẫn tiện tay vứt rác. Anh Tùng thì ăn xong cứ để đó. Ông Sáu thì không hiểu rác trên đường với rác dưới sông liên quan gì đến nhau."

*[Quay lại nhìn người chơi]*

💬 "Nếu cháu rời đi mà họ vẫn vậy, thì một tháng nữa thôi — thị trấn sẽ lại như lúc cháu mới đến. Dọn rác là việc của tay. Nhưng thay đổi con người mới là việc... của một người thực sự quan tâm. Cháu hiểu ý bác chứ?"

Objective 1: Thuyết phục 3 NPC

  ┌─────────────────────────────────────────────────────────────┐
  │  NPC 1 — CÔ TƯ (Khu dân cư, trước tiệm tạp hóa)            │
  │  Context clue: Trên quầy có ảnh con gái cô chơi ở công viên │
  │  Thoại mở đầu: "Chỉ một ít rác thôi mà, có sao đâu.        │
  │    Một cái vỏ bánh, một cái túi nilon — có đáng gì..."      │
  │                                                             │
  │  A. "Ừ, một ít thì không sao."                    → CA +0   │
  │  B. "Nếu ai cũng nghĩ một ít không sao, thì 50 hộ            │
  │      trong khu này, mỗi ngày một ít — cô thử tính            │
  │      một tháng có bao nhiêu rác trước cửa tiệm?"  → CA +10 ✓│
  │  C. "Cô mà còn vứt, con báo hội đồng thị trấn."   → CA +3   │
  │                                                             │
  │  Feedback B: "50 hộ... Ừ ha. Cô chưa nghĩ tới vụ đó.        │
  │    Từ mai cô sẽ bỏ rác vô thùng." [Cô quét vỏ bánh bỏ thùng]│
  │  Feedback C: "Trời, có nhiêu đó mà cũng đi báo..."           │
  │    [Dừng xả rác vì sợ phạt, không phải vì hiểu]             │
  └─────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────┐
  │  NPC 2 — ANH TÙNG (Khu picnic, trên thảm picnic)           │
  │  Context clue: Chim đang bay quanh, không dám đậu vì rác     │
  │  Thoại mở đầu: "Ăn xong tụi mình sẽ có người dọn thôi.      │
  │    Công viên này có đội vệ sinh mà — tuần dọn hai lần."      │
  │                                                             │
  │  A. "Không sao, cứ để đó đi."                      → CA +0  │
  │  B. "Nếu ai cũng tự dọn và phân loại rác sau khi ăn,        │
  │      công viên sẽ sạch cho chính mình lần sau —              │
  │      với lại chim cũng không bị mắc rác nhựa."    → CA +10 ✓│
  │  C. "Anh phải tự dọn ngay — để rác là thiếu ý thức."→ CA +3 │
  │                                                             │
  │  Feedback B: "Con chim đó... nó bị mắc nhựa hả?              │
  │    Tụi anh có để ý vụ đó đâu. Thôi được rồi —                │
  │    từ bữa sau tụi anh tự dọn." [Cả nhóm cùng dọn]           │
  │  Feedback C: "Mà nói chuyện nhẹ nhàng thôi em..."            │
  │    [Dọn nhưng không vui]                                    │
  └─────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────┐
  │  NPC 3 — ÔNG SÁU (Bờ sông, ngồi câu cá)                     │
  │  Context clue: Rãnh nước nhỏ chảy từ đường xuống sông        │
  │  Thoại mở đầu: "Tôi có vứt xuống sông đâu — tôi chỉ để       │
  │    trên đường. Rác trên đường thì hại gì đến cá?"            │
  │                                                             │
  │  A. "Thì cũng không hại gì."                       → CA +0  │
  │  B. "Khi mưa, nước cuốn rác theo rãnh này xuống sông.       │
  │      Mỗi lần mưa là rác của mình xuống sông —                │
  │      cá phải sống trong nước đó, ông ạ."          → CA +10 ✓│
  │  C. "Ông nên cẩn thận hơn — rác trên bờ cũng                │
  │      ảnh hưởng đến sông."                          → CA +3  │
  │                                                             │
  │  Feedback B: "Cái rãnh này... Ừ ha, nó chảy thẳng xuống      │
  │    sông thiệt. Mấy chục năm ông ngồi đây chưa nghĩ tới.      │
  │    Hóa ra cá bỏ đi là tại mình..." [Ông nhặt vỏ hộp bỏ thùng]│
  │  Feedback C: "Nghe giống mấy cái bảng tuyên truyền quá..."   │
  │    [Dừng vứt rác nhưng chưa thực sự hiểu]                   │
  └─────────────────────────────────────────────────────────────┘

  ↓

Objective 2: Trồng 3 cây ở các khu đất sạch
  → Kiểm tra PL khu đó < 50%, không còn rác nhìn thấy
  → Nếu chưa đủ: nhắc dọn thêm
  → Trồng cây → ES +5 mỗi cây, visual đổi ngay lập tức

  ↓

Bác Xanh (sau khi thuyết phục thành công NPC đầu tiên):
💬 "Hay lắm! Cháu thấy không — họ không xấu, họ chỉ chưa hiểu thôi.
    Một lời nói đúng lúc có sức mạnh hơn cả cái máy quét của bác đấy."

Bác Xanh (sau khi thuyết phục cả ba NPC):
💬 "Cả ba người... Cháu đã nói chuyện được với cả ba.
    Cô Tư chịu bỏ rác vào thùng. Anh Tùng chịu dọn sau khi ăn.
    Ông Sáu đã hiểu rác trên bờ và rác dưới sông là một.
    Cháu biết không — cái này còn khó hơn thông cống gấp mười lần."

Bác Xanh (sau khi trồng cây đầu tiên):
💬 "Cây non... Hồi xưa bác với mấy ông bạn trồng nguyên hàng cây
    dọc bờ sông. Giờ cháu trồng tiếp — như là nối lại cái hàng cây đó.
    Ý nghĩa lắm."

  ↓

Objective 3: Gặp Bác Xanh ở quảng trường

Bác Xanh (đứng cạnh đài phun nước — đã có nước nếu visual đạt mức cao):
💬 "Lại đây cháu. Đài phun nước này — nó khô từ 3 năm trước, từ hồi
    cái cống bắt đầu tắc. Sáng nay bác ra đây, thấy nước chảy lại...
    Bác đứng cả buổi không nói nên lời."

💬 "Cháu đến thị trấn này là một người lạ. Mà giờ nhìn quanh đi —
    không còn lạ nữa. Mỗi cái cây, mỗi con chim, mỗi người dân...
    đều có một phần của cháu trong đó."

💬 "Giờ thì... để bác cho cháu biết thị trấn Ven Sông đã thay đổi
    đến mức nào nhé."

  → EndingManager tổng kết
  → Cutscene hoặc UI kết quả
  → Nhận Ending A, B hoặc C
```

---

## PHẦN 6: HỆ THỐNG ENDING

### Điều kiện Ending

| Chỉ số | Ending A | Ending B | Ending C |
|---|---|---|---|
| Environment Score | ≥ 90 | 65–89 | < 65 |
| Pollution Level (TB) | < 20 | 20–45 | > 45 |
| Community Awareness | ≥ 70 | 40–69 | < 40 |
| Số động vật đã cứu | 3/3 | 2–3/3 | 0–1/3 |
| Số cây đã trồng | ≥ 3 | 1–2 | 0 |

> **Lưu ý:** Nếu điều kiện lẫn lộn giữa hai ending (ví dụ ES cao nhưng CA thấp), game ưu tiên ending thấp hơn.

---

### 🏆 Ending A: Green Again

**Thông điệp Bác Xanh:**  
> "Môi trường bền vững không đến từ một mình ai. Nó cần hành động cá nhân, hạ tầng đúng chỗ và cả một cộng đồng cùng nhìn về một hướng. Cháu đã làm được cả ba. Thị trấn Ven Sông — xanh trở lại rồi. Nhờ cháu."

**Phản hồi NPC (lần lượt hiện trong UI tổng kết):**
- **Cô Tư:** 💬 "Hồi trước cô cứ nghĩ một mình cô thì có gì đâu. Mà giờ cả xóm cùng làm — đường sá sạch sẽ, đi chợ cũng vui hơn. Cảm ơn cháu nghen."
- **Anh Tùng:** 💬 "Từ bữa em nói, tụi anh dọn sau khi ăn luôn. Công viên giờ như của mình thiệt. Cuối tuần tụi anh làm picnic 'xanh', em ghé chơi nha!"
- **Ông Sáu:** 💬 "Cháu coi nè! Cá cắn câu lại rồi! 3 năm rồi ông mới câu được con cá to vầy... Cảm ơn cháu. Không có cháu chắc ông vẫn ngồi đây mà không hiểu tại sao cá bỏ đi."

**Visual:** Thị trấn xanh rõ, ánh sáng ấm, động vật quanh quất, NPC đi bộ tự nhiên, cây ra lá mới, đài phun nước có nước.  
**Reward:** Badge "Green Guardian"

---

### 🥈 Ending B: Đang trên đường phục hồi

**Thông điệp Bác Xanh:**  
> "Thị trấn đã sạch hơn nhiều so với lúc đầu. Nhưng để giữ vững điều này, cần nhiều người hơn — và cần tiếp tục. Cháu đã làm được nhiều rồi. Phần còn lại... biết đâu có ngày cháu quay lại?"

**Phản hồi NPC (những người chưa được thuyết phục sẽ có thoại khác):**
- NPC đã thuyết phục → thoại như Ending A nhưng thêm: "...mà giá như mọi người cùng làm như mình."
- NPC chưa thuyết phục → thoại trung lập, chưa nhận ra vấn đề.

**Visual:** Công viên xanh, bờ sông còn hơi đục, một vài khu chưa hoàn toàn phục hồi.  
**Gợi ý:** "Thuyết phục thêm người dân, trồng thêm cây để đạt Green Again."

---

### 📉 Ending C: Sạch nhưng chưa bền

**Thông điệp Bác Xanh:**  
> "Thị trấn sạch hơn hôm cháu đến. Nhưng nếu không có gì thay đổi sâu hơn, chỉ cần vài tuần là rác sẽ quay lại. Dọn rác là bước đầu — nhưng chỉ là bước đầu thôi. Cháu làm tốt phần của mình rồi. Chỉ tiếc là... chưa đủ."

**Phản hồi NPC:** Hầu hết NPC chưa được thuyết phục → vẫn thờ ơ hoặc không hiểu vấn đề. Có thể thấy NPC tiếp tục xả rác trong background của UI tổng kết.

**Visual:** Một số khu sạch, nhưng khu dân cư và bờ sông vẫn xám.  
**Gợi ý:** "Hãy xử lý các Hotspot còn lại và nói chuyện với người dân."

> ⚠️ **Thay đổi so với v1:** Ending C không có rác quay lại theo thời gian thực trong cutscene — chỉ dùng UI thống kê và thoại. Dễ implement hơn, tránh bug visual.

---

## PHẦN 7: UI VÀ FEEDBACK

### 7.0 Minimap (v3 — mới)

**Vị trí:** Góc trên trái màn hình  
**Kích thước:** Nhỏ (~15% màn hình), có thể toggle ẩn/hiện bằng phím M

```
┌──────────────┐
│  RỪNG CÂY    │
│  [Cây][Cây]  │
│ DCư [RC] Cviên│  ← ● = vị trí người chơi
│  QuảngTrường  │  ← marker màu: 🟠🟠🔴 = hotspot
│   ~~~Sông~~~  │  ← ~~~ = bờ sông
│   [Cống]      │
└──────────────┘
```

**Hiển thị:**
- Vị trí người chơi (chấm trắng)
- Tên khu vực (chữ nhỏ)
- Hotspot marker (màu theo PL: vàng/cam/đỏ/xanh)
- Vị trí Bác Xanh (chấm xanh lá)
- Vị trí Trung tâm Tái chế (icon thùng rác)
- Hướng người chơi đang nhìn (mũi tên nhỏ)

> ⚠️ **Lý do thêm (Friction Journey Audit):** Trẻ 10-12 tuổi cần công cụ xây dựng mental model bản đồ. Không có minimap, navigation thuần túy dựa vào trí nhớ dẫn đến lạc đường và snowball timer.

### 7.05 Wayfinding trong thế giới (v3 — mới)

**Biển chỉ dẫn tại ranh giới các khu vực:**
- Mỗi lối ra vào zone có biển gỗ nhỏ: "← Khu Dân Cư | Công Viên →"
- Biển ở ngã ba Quảng trường: "↑ Trung Tâm Tái Chế | → Công Viên | ← Khu Dân Cư"

**Điểm mốc (Landmark):**
- **Cối xay gió cũ** ở rìa Công viên — có thể nhìn thấy từ mọi khu vực trong thị trấn
- Đây là điểm neo không gian (spatial anchor) — người chơi luôn biết hướng Công viên
- Cối xay gió thay đổi visual theo ES toàn map (gãy cánh → lành → quay)

**Đường mòn:**
- Đường đất nối Quảng trường → RC → Công viên → Khu dân cư
- Màu đất khác biệt giữa các zone (gạch xám ở Quảng trường, đất nâu ở Khu dân cư, cỏ ở Công viên)
- Giúp người chơi nhận biết zone transition mà không cần nhìn UI

**Scanner breadcrumb (v3 — mới):**
- Khi Scanner bật, ngoài marker hotspot, còn hiện đường mòn mờ (faint blue trail) nối từ vị trí người chơi đến hotspot gần nhất
- Trail mờ dần khi đến gần — chỉ dẫn hướng, không railroad

---

### 7.1 HUD chính (luôn hiển thị)

```
┌──────────────────────────────────────────────────────────┐
│  🌿 ES: 55   ☠️ PL: 38   👥 CA: 45   🗑️ Túi: ■■■□□ (3/5)│
└──────────────────────────────────────────────────────────┘
```

Chỉ hiển thị số và icon — không cần thanh dài phức tạp. Tooltip khi hover giải thích ý nghĩa.

### 7.2 Quest Tracker (góc trên phải)

```
┌──────────────────────────┐
│  📋 NHIỆM VỤ HIỆN TẠI   │
│  Tìm Hotspot: 2/3       │
│  [Sử dụng Eco Scanner]  │
└──────────────────────────┘
```

### 7.3 Feedback tức thì

| Sự kiện | Feedback |
|---|---|
| Nhặt rác | Sound nhỏ + icon +1 nhỏ ở góc túi |
| Phân loại đúng | "✅ Đúng!" + +2 ES nhỏ nổi lên |
| Phân loại sai | "❌ Chưa đúng — [giải thích ngắn]" |
| Đặt hạ tầng Good | "✅ Vị trí tốt!" + +5 ES |
| Cứu động vật | Animation nhỏ + âm thanh vui + +8 ES nổi lên lớn |
| Pollution Spread Event | Màn hình nhấp nháy cam nhẹ + thông báo nổi bật |

---

## PHẦN 8: THỨ TỰ PHÁT TRIỂN MVP

### Ưu tiên 1 — Core không thể thiếu:
- [ ] Nhặt rác (pickup mechanic)
- [ ] Inventory 5 món
- [ ] Sorting system (4 loại rác)
- [ ] 3 chỉ số ES / PL / CA
- [ ] NPC Bác Xanh + hội thoại cơ bản
- [ ] QuestManager theo Chapter

### Ưu tiên 2 — Chiều sâu gameplay:
- [ ] Eco Scanner + Hotspot marker
- [ ] Dynamic Trash Spawner (tái sinh theo điều kiện)
- [ ] Placement system (thùng rác, biển báo)
- [ ] Pollution Spread Event (cống → sông)
- [ ] NPC behaviour 3 trạng thái

### Ưu tiên 3 — Game sống hơn:
- [ ] Animal Rescue (chim, cá, sóc)
- [ ] Trồng cây
- [ ] Visual map thay đổi theo ES khu vực
- [ ] Ending A/B/C với UI tổng kết
- [ ] Dialogue system chọn câu trả lời

### Ưu tiên 4 — Polish:
- [ ] Âm thanh môi trường thay đổi theo ES
- [ ] Hiệu ứng Scanner (filter xanh)
- [ ] Animation NPC bỏ rác vào thùng
- [ ] Particle effect khi trồng cây hoặc cứu động vật
- [ ] Cutscene ngắn khi nhận Ending

---

## PHẦN 9: BẢNG TÓM TẮT CHAPTER

| Chapter | Thời gian | Hệ thống mới | Bài học cốt lõi |
|---|---|---|---|
| 1 | 5–8 phút | Nhặt rác, NPC, Scanner | Ô nhiễm phức tạp hơn mắt thấy |
| 2 | 11–14 phút | Scanner, Inventory, Sorting, Hotspot (3 phase) | Phân loại đúng là xử lý đúng |
| 3 | 10–15 phút | Placement, Cống, Event, Bác Xanh cảnh báo | Hạ tầng ngăn rác tái sinh |
| 4 | 10–15 phút | Animal Rescue, Gating, Bác Xanh phản hồi | Ô nhiễm ảnh hưởng sinh vật |
| 5 | 10–15 phút | Dialogue (3 NPC × 3 lựa chọn), Trồng cây, Ending | Cộng đồng mới tạo thay đổi bền vững |
| **Tổng** | **~55–70 phút** | | |

---

*GDD v2.0 → v3 — Green Again: One Living Town*  
*Điều chỉnh bởi design review & 4 audit (Failure Loop, FTUE Hero's Journey, Flow, Player Motivation), tháng 6/2026*

---

## PHẦN 10: CHANGELOG v3

| # | Thay đổi | Audit nguồn | Mục tiêu |
|---|---|---|---|
| 1 | **Chapter 2 chia 3 mini-phase (A/B/C)** | Flow | Tránh vách đá độ phức tạp C1→C2. Mỗi phase mở khóa 1-2 hệ thống thay vì 4 cùng lúc |
| 2 | **Viết lại toàn bộ hội thoại Bác Xanh (C1)** | FTUE Hero's Journey | Thêm kết nối cảm xúc: mentor có tên, lịch sử, công nhận người chơi, Scanner là quà tặng |
| 3 | **Hiệu ứng Spill khi phân loại sai** | Failure Loop | Thêm nhân quả visual khi sort sai (vệt bẩn, dọn 1 giây) — không phạt điểm, khôi phục Pillar 1 |
| 4 | **Toàn bộ hội thoại NPC chi tiết (~91 dòng)** | FTUE + Motivation + Flow | 6 NPC có tên + tính cách + context clue + multi-state dialogue (Unaware/Aware/Considerate) + Ending; Bác Xanh xuyên suốt 5 chapter; Chị Lan + Bé Na NPC phụ; system dialogue đầy đủ |
| 5 | **Bác Xanh phản ứng Pollution Spread Event (C3)** | Failure Loop | Mentor cảnh báo khẩn trương ở cả 2 giai đoạn — tăng emotional stake của event |
| 6 | **Bác Xanh phản ứng cứu động vật (C4)** | Motivation | 3 mốc phản hồi (cứu 1/2/3 con) — tăng dần xúc động, tạo payoff cho identified regulation |
| 7 | **Bác Xanh dẫn vào Ending + NPC ending lines** | Motivation | Đài phun nước có nước = biểu tượng; mỗi NPC có thoại riêng theo ending đạt được |

> 📖 **File hội thoại đầy đủ:** `GDD_GreenAgain_NPC_Dialogue_v3.md`

