# Green Again v5 - Current Map Draft

> Mục tiêu của tài liệu này: ghi lại bản đồ theo cách project nên hiểu ở thời điểm hiện tại, dựa trên map thật và audit chỉnh sửa của người thiết kế. Đây vẫn là bản nháp để tiếp tục sửa, nhưng đã bỏ cách hiểu cũ theo "tầng tọa độ" và chuyển sang cách đọc map theo cụm địa điểm.

## 1. Cách đọc map hiện tại

Map chính không nên được hiểu như một sơ đồ dọc từ trên xuống theo tọa độ. Map nên được hiểu như các cụm không gian nối với nhau:

```text
Spawner + Nhà văn hóa
        |
        v
Thị trấn / làng Ven Sông + Tạp hóa Cô Tư
        |
        v
Sân bóng thôn
        |
        v
Ông Sáu + bờ sông
        |
        v
Dòng sông liên tục + khúc cong
        |
        v
Cống thoát nước cuối xóm
```

Cụm phụ quan trọng:

```text
Nhà văn hóa ---- Điểm tập kết rác ---- đường nối lên khu sinh hoạt
```

## 2. Sơ đồ không gian corrected

Sơ đồ này ưu tiên quan hệ không gian nhìn từ map thật, không ưu tiên chính xác tọa độ tuyệt đối.

```text
                         THỊ TRẤN / LÀNG VEN SÔNG
                  nhà dân, đường làng, khu sinh hoạt thường ngày
                                      |
                                      |
                               TẠP HÓA CÔ TƯ
                         điểm chuyển từ làng sang sân bóng
                                      |
                                      |
  SPAWNER ---- NHÀ VĂN HÓA ---- ĐIỂM TẬP KẾT RÁC -------- SÂN BÓNG
  bắt đầu      hub kể chuyện     tutorial phân loại        Anh Tùng, Bé Na
               Bác Xanh          / rác cộng đồng           rác sau vui chơi
                                                                  |
                                                                  |
                                                              ÔNG SÁU
                                                        bờ sông / ký ức cũ
                                                                  |
                                                                  |
                                                          DÒNG SÔNG LIÊN TỤC
                                                        rác trôi theo dòng
                                                                  |
                                                                  |
                                                       CỐNG THOÁT NƯỚC CUỐI XÓM
                                                       rác tụ, nghẹt, hậu quả
```

## 3. Những sửa đổi lớn so với bản nháp cũ

| Bản nháp cũ | Cách hiểu corrected |
|---|---|
| Map được vẽ theo "đường trên -> giữa -> dưới" | Map được đọc theo cụm: hub, làng, tạp hóa, sân bóng, sông, cống |
| `Portal1Destination` được xem như cổng vào làng bên phải | Người chơi thực tế bắt đầu từ `Spawner` gần Nhà văn hóa |
| `Nhà văn hóa` nằm như một điểm giữa map | `Nhà văn hóa` là hub khởi đầu ở cụm dưới/trái |
| `Điểm tập kết rác` nằm tách bên trái Nhà văn hóa | Điểm tập kết rác nằm bên phải/hơi trên Nhà văn hóa, là điểm trung gian rất tốt |
| `PicnicArea` / công viên / bãi picnic | `Sân bóng thôn Ven Sông` |
| `ResidentialSt` / xóm ven đường nhỏ | `Thị trấn / làng Ven Sông`, một cụm dân cư lớn hơn |
| `Dam_C1/C2/C3` / đập | `Cống thoát nước cuối xóm` |
| Sông là nhiều hotspot rời | Sông là một dòng liên tục từ bờ sông Ông Sáu xuống khúc cong và cống |

## 4. Địa điểm chính của map

| Địa điểm v5 | Tên kỹ thuật hiện có | Vai trò không gian | Vai trò story |
|---|---|---|---|
| Spawner map chính | `Spawner` / điểm spawn thực tế sau teleport | Bên trái Nhà văn hóa | Nơi người chơi bắt đầu cảm giác "mình vừa đến Ven Sông". |
| Nhà văn hóa thôn Ven Sông | `NhaVanHoa_ThonNoiChuan` | Hub khởi đầu, gần Spawner | Nơi gặp Bác Xanh, mở chương, kết chương, ending cộng đồng. |
| Bác Xanh | `Bác Xanh` | Ở khu Nhà văn hóa | Mentor kể chuyện Ven Sông và dẫn người chơi qua từng cụm. |
| Điểm tập kết rác thôn | `DiemTapKetRacThai_ThonVenSong` | Bên phải/hơi trên Nhà văn hóa | Tutorial phân loại, nơi Chị Lan/tổ môi trường giải thích rác cộng đồng. |
| Chị Lan | `Chị Lan` | Gần điểm tập kết rác | NPC phụ trách rác/phân loại hoặc người trong tổ môi trường. |
| Thị trấn / làng Ven Sông | `ResidentialSt` + cụm building dân cư | Cụm làng bên trái/trên hub | Chứng minh rác đến từ sinh hoạt thường ngày, không phải một sự kiện riêng lẻ. |
| Tạp hóa Cô Tư | `TapHoaCoTu_HouseOnly_Rural`, `Cô Tư` | Nối cụm làng với sân bóng | Nơi kể chuyện nhu cầu tăng: túi nilon, chai nước, bao snack, hộp xốp. |
| Sân bóng thôn Ven Sông | `PicnicArea` hiện tại nên đổi nghĩa | Khu sinh hoạt lớn bên phải/trung tâm | Rác sau trận bóng/tụ tập: chai nước, ly nhựa, túi snack. |
| Anh Tùng | `Anh Tùng` | Ở sân bóng | Người chơi bóng/người trẻ vô tư, ban đầu nghĩ "chỉ một chút thôi". |
| Bé Na | `Bé Na` | Gần sân bóng | Em nhỏ chứng kiến hậu quả, tạo cảm xúc và góc nhìn trong sáng. |
| Ông Sáu | `Ông Sáu` | Ngay bên phải sân bóng, sát sông | Người sống lâu năm nhớ Ven Sông từng xanh, dẫn người chơi nhìn ra dòng sông. |
| Bờ sông chỗ Ông Sáu | `RiverNE` nếu dùng marker | Sát Ông Sáu | Điểm chuyển từ "rác trên đất" sang "rác trôi theo nước". |
| Khúc sông sau làng | `RiverBend` | Một đoạn trong dòng sông liên tục | Nơi rác tụ theo dòng chảy. |
| Cống thoát nước cuối xóm | `Dam_C1/C2/C3` hiện tại nên đổi nghĩa | Cuối dòng, phía dưới map | Cao trào môi trường: rác mắc lại, nghẹt nước, mùi, hậu quả thấy rõ. |

## 5. Địa điểm không nên dùng theo tên cũ

Các tên này dễ làm lệch hướng thiết kế:

- Không gọi `PicnicArea` là `Công viên`, `Bãi picnic`, hoặc `Bãi cỏ ven sông` nữa. Trong story v5, đây là `Sân bóng thôn Ven Sông`.
- Không gọi `Dam_C1/C2/C3` là `Đập` nữa. Trong story v5, đây là `Cống thoát nước cuối xóm`.
- Không gọi toàn bộ `ResidentialSt` là `Xóm ven đường` nếu đang nói về cụm lớn. Nên gọi là `Thị trấn / làng Ven Sông`. Nếu cần "xóm ven đường", chỉ dùng cho một đoạn nhỏ trong cụm làng.
- Không xem `Portal1Destination` là cổng vào làng trong fiction nếu người chơi thực tế spawn gần Nhà văn hóa. Với người chơi, điểm bắt đầu nên được gọi là `Spawner` hoặc `lối vào Nhà văn hóa`.
- Không chia `RiverNE`, `RiverBend`, `Dam_C1/C2/C3` thành các vấn đề rời rạc. Chúng là các đoạn của một hệ thống nước.

## 6. Route story v5 corrected

### Chapter 1 - Người lạ đến Ven Sông

Route:

```text
Spawner -> Nhà văn hóa -> Bác Xanh -> Điểm tập kết rác
```

Vai trò:

- Người chơi xuất hiện gần hub cộng đồng, không phải từ một cổng xa ngoài làng.
- Bác Xanh đón người chơi ở Nhà văn hóa.
- Điểm tập kết rác nằm đủ gần để làm tutorial đầu: nhặt rác, phân loại, hiểu "rác không tự biến mất".

### Chapter 2 - Chỉ một chút thôi mà

Route:

```text
Nhà văn hóa -> Thị trấn/làng -> Tạp hóa Cô Tư
```

Vai trò:

- Cô Tư kể về nhu cầu sinh hoạt tăng: hàng hóa tiện hơn, bao bì nhiều hơn.
- Rác không đến từ "người xấu"; nó đến từ thói quen nhỏ lặp lại mỗi ngày.
- Người chơi thấy túi nilon, chai nước, bao snack, hộp xốp quanh đường làng/tạp hóa.

### Chapter 3 - Sau trận bóng

Route:

```text
Tạp hóa Cô Tư -> Sân bóng -> Anh Tùng / Bé Na
```

Vai trò:

- Sân bóng là nơi vui chơi/sinh hoạt, không phải công viên picnic.
- Sau trận bóng hoặc buổi tụ tập, rác nằm quanh sân: chai nước, ly nhựa, túi snack.
- Anh Tùng ban đầu có thể nghĩ "để đó lát có người dọn".
- Bé Na giúp chuyển cảm xúc: trẻ con cũng thấy sân chơi của mình đang bẩn đi.

### Chapter 4 - Rác không đứng yên

Route:

```text
Sân bóng -> Ông Sáu -> bờ sông -> dòng sông
```

Vai trò:

- Ông Sáu nằm gần sân bóng và sông, nên là cầu nối tự nhiên.
- Ông Sáu chỉ ra rác không chỉ nằm ở nơi bị vứt; nó bị gió/nước cuốn xuống sông.
- Người chơi bắt đầu hiểu hệ quả lan truyền: sân bóng bẩn là chuyện nhìn thấy, sông bẩn là chuyện chảy âm thầm.

### Chapter 5 - Cống cuối xóm và lời hứa Ven Sông

Route:

```text
Dòng sông
-> khúc cong
-> cống thoát nước cuối xóm
-> điểm tập kết rác / các điểm phòng ngừa
-> Nhà văn hóa
```

Vai trò:

- Cống thoát nước là cao trào môi trường: rác tụ lại, nghẹt dòng, gây mùi và tác động thấy rõ.
- Chapter 5 không chỉ là dọn cống. Nó gồm 5 phase: thấy hậu quả, dọn cống, gọi cộng đồng, đặt phòng ngừa, quay về Nhà văn hóa.
- Điểm tập kết rác trở lại như nơi biến "dọn rác" thành "rác đi đúng chỗ".
- Tạp hóa, Sân bóng, bờ sông nên có ít nhất 2-3 hành động phòng ngừa đại diện: thùng rác, biển nhắc, cây xanh hoặc cam kết NPC.
- Ending quay về Nhà văn hóa: cả cộng đồng không "cứu môi trường trong một ngày", nhưng biết bắt đầu từ hành động nhỏ đúng chỗ.

NPC nên tham gia:

- Bác Xanh: kết nối ý nghĩa, mở ending.
- Chị Lan: hướng dẫn rác đi về điểm tập kết/phân loại.
- Anh Hòa thợ sửa cống nếu thêm: giải thích nghẹt cống.
- Cô Tư: cam kết giảm/nhắc rác ở tạp hóa.
- Anh Tùng: cam kết dọn sân sau trận bóng.
- Ông Sáu: cam kết nhắc người ở bờ sông.
- Bé Na: đại diện thế hệ sau được hưởng một Ven Sông sạch hơn.

## 7. Logic sông trong story

Sông phải được kể như một dòng liên tục:

```text
Rác từ làng / tạp hóa / sân bóng
        |
        v
rơi hoặc bị cuốn về bờ sông chỗ Ông Sáu
        |
        v
trôi theo dòng
        |
        v
tụ ở khúc cong
        |
        v
mắc tại cống thoát nước cuối xóm
```

Điều này giúp Chapter 3 và Chapter 4 rõ hơn: người chơi không chỉ dọn rác từng điểm, mà hiểu đường đi của rác.

## 8. Placement zone nên hiểu lại

| Loại zone | Cách dùng v5 đề xuất |
|---|---|
| Thùng rác | Nên có gần Tạp hóa Cô Tư, gần Sân bóng, và điểm phân loại lớn ở Điểm tập kết rác. |
| Biển báo | Nên đặt ở lối vào Nhà văn hóa, đường Tạp hóa -> Sân bóng, gần bờ sông Ông Sáu, và gần Cống thoát nước. |
| Cây xanh | Nên dùng để phục hồi cảm giác làng xanh lại: quanh Nhà văn hóa, sân bóng, bờ sông. |

Ghi chú: các `SignZone_1..3` và `BinZone_1..2` hiện có trong Studio vẫn dùng được, nhưng story/marker không nên mô tả chúng như "khu đường trên" nếu không khớp route thực tế.

## 9. Mật độ NPC theo map

Map hiện tại chỉ có vài NPC chính nên cảm giác câu chuyện còn mỏng. V5 nên thêm NPC phụ theo cụm, ưu tiên thoại ngắn và vai trò rõ, không biến tất cả thành quest giver.

| Cụm map | NPC hiện có | NPC phụ nên thêm | Tác dụng |
|---|---|---|---|
| Nhà văn hóa | Bác Xanh | Bác Bảy bảo vệ Nhà văn hóa | Tạo cảm giác hub cộng đồng có người trông nom/ký ức. |
| Điểm tập kết rác | Chị Lan | Chú Minh xe rác | Giải thích vì sao phân loại rác quan trọng trong đời thường. |
| Thị trấn / làng | Chưa có rõ ngoài Cô Tư gần đó | Cô Hạnh tổ dân phố, Em Phúc học sinh | Cho thấy rác sinh hoạt ảnh hưởng cả người lớn và trẻ nhỏ. |
| Tạp hóa Cô Tư | Cô Tư | Có thể thêm khách mua hàng | Làm rõ nhu cầu tăng, bao bì tăng, thói quen tiện tay. |
| Sân bóng | Anh Tùng, Bé Na | Dì Năm bán nước, Nam thủ môn, Cô Mai phụ huynh | Sân bóng thành nơi sinh hoạt đông người, không phải chỉ 2 NPC đứng nói chuyện. |
| Bờ sông Ông Sáu | Ông Sáu | Chú Lộc câu cá, Bà Tám ven sông | Tăng góc nhìn ký ức và hậu quả ở sông. |
| Cống thoát nước | Chưa có NPC riêng | Anh Hòa thợ sửa cống | Giải thích hậu quả cụ thể của rác mắc cống. |

Quy tắc đặt NPC:

- NPC chính đứng ở vị trí dễ thấy, gần marker nhiệm vụ.
- NPC phụ đứng gần bối cảnh liên quan, không chắn đường chính.
- Ambient NPC chỉ cần câu thoại ngắn, không hiện marker lớn.
- Ending ở Nhà văn hóa có thể gọi một số NPC phụ đã gặp về đứng trong đám đông.

## 10. Gợi ý đổi tên kỹ thuật sau này

Nếu có thời gian refactor tên instance/quest, nên đổi để giảm nhầm lẫn:

| Tên hiện tại | Tên nên dùng |
|---|---|
| `PicnicArea` | `SanBong_ThonVenSong` |
| `ResidentialSt` | `LangVenSong` hoặc `ThiTranVenSong` |
| `RiverNE` | `BoSong_OngSau` |
| `RiverBend` | `KhucSongSauLang` |
| `Dam_C1` / `Dam_C2` / `Dam_C3` | `CongThoatNuoc_CuoiXom` hoặc các segment quanh cống |
| `Portal1Destination` trong fiction | `Spawner_MainMap` hoặc `LoiVaoNhaVanHoa` |

## 11. Những điều cần xác nhận tiếp trong Studio/map

1. Điểm spawn thật sau teleport hiện đang là instance nào? Có cần đổi tên `Portal1Destination` cho khớp vai trò không?
2. Sân bóng có tên kỹ thuật riêng trong Workspace chưa, hay hiện vẫn chỉ được đại diện bằng hotspot `PicnicArea`?
3. Cống thoát nước có model/mesh rõ chưa, hay mới chỉ có hotspot `Dam_C1/C2/C3`?
4. Bờ sông chỗ Ông Sáu có bến/cầu gỗ không? Nếu không, chỉ gọi là `Bờ sông chỗ Ông Sáu`, không gọi là `Bến câu`.
5. Đường chính người chơi nên đi có cần thêm path marker/biển chỉ dẫn vật lý không?
6. Điểm tập kết rác có đủ gần Nhà văn hóa để làm tutorial phân loại ngay Chapter 1 không?

## 12. North Star map v5

Map v5 phải giúp người chơi hiểu nguyên nhân và hậu quả theo không gian:

```text
Sinh hoạt hằng ngày tạo rác
        |
        v
Vui chơi/tụ tập làm rác nhiều hơn
        |
        v
Rác bị bỏ lại không đứng yên
        |
        v
Rác trôi xuống sông và mắc ở cống
        |
        v
Cộng đồng cùng thay đổi thói quen
```

Mỗi địa điểm nên trả lời một câu hỏi:

- `Nhà văn hóa`: Ai kể cho mình câu chuyện Ven Sông?
- `Điểm tập kết rác`: Rác nên đi đâu sau khi được nhặt?
- `Thị trấn/làng`: Rác bắt đầu từ thói quen sinh hoạt nào?
- `Tạp hóa Cô Tư`: Vì sao nhu cầu tăng làm bao bì tăng?
- `Sân bóng`: Vì sao "chỉ một chút thôi" thành nhiều?
- `Ông Sáu + bờ sông`: Người sống lâu ở đây thấy môi trường đổi thay ra sao?
- `Cống thoát nước`: Rác cuối cùng gây hậu quả cụ thể thế nào?
- `Nhà văn hóa cuối game`: Cộng đồng sẽ làm gì để Ven Sông xanh lại?
