# Green Again v6 - Cutscene Script

> Cutscene trong v6 là xương sống cảm xúc. Mỗi cutscene phải có: mục tiêu cảm xúc, staging, thoại chính, trigger, và objective sau đó.

## 1. Cutscene Style

- Thời lượng lý tưởng: 20-60 giây.
- Chỉ dùng cinematic camera cho moment quan trọng.
- Các đoạn nhỏ có thể dùng dialogue lock + camera focus nhẹ.
- Không dùng cutscene để giảng bài dài.
- Mỗi cutscene kết thúc bằng objective rõ ràng.

## 2. Required Cutscenes

| ID | Chapter | Tên | Trigger | Mục tiêu |
|---|---|---|---|---|
| CS0 | Lobby/Main | Bước Qua Cổng | Player teleport sang map chính | Tạo cảm giác bước vào Ven Sông |
| CS1 | Ch1 | Bác Xanh Và Ảnh Cũ | Player tới Nhà văn hóa | Ven Sông từng xanh |
| CS1B | Ch1 | Điểm Tập Kết Rác | Sau gặp Bác Xanh | Rác cần đi đúng chỗ |
| CS2 | Ch2 | Cái Túi Nhỏ | Player gặp Cô Tư | Nhu cầu tăng, bao bì tăng |
| CS3 | Ch3 | Sau Trận Bóng | Player tới sân bóng | Vui chơi cũng để lại dấu vết |
| CS4 | Ch4 | Rác Trôi Theo Nước | Player gặp Ông Sáu | Rác không đứng yên |
| CS5A | Ch5 | Cống Nghẹt | Player tới cống | Hậu quả cuối dòng |
| CS5B | Ch5 | Dọn Cống Không Đủ | Sau clear cống | Cần cộng đồng thay đổi |
| CS5C | Ch5 | Ngõ Sau Cơn Mưa | Player quay lại khu dân cư | Hậu quả quay lại đời sống hằng ngày |
| CS5D | Ch5 | Chỗ Sống Nhỏ | Player dọn góc cây và trồng cây | Cho thấy môi trường là nơi sống, không chỉ nơi sạch |
| CS5E | Ch5 | Lời Hứa Nhà Văn Hóa | Player nói chuyện Bác Xanh cuối game | Ending truyền cảm hứng |

## 3. CS0 - Bước Qua Cổng

Trigger: player teleport từ lobby sang map chính.

Staging:

- Fade in từ đen.
- Camera nhìn từ sau player về hướng Nhà văn hóa.
- Một bảng/ảnh cũ hoặc biển bạc màu nằm trong tầm nhìn.
- Rác không quá dày, chỉ đủ để thấy nơi này bị bỏ quên.

Text on screen:

```text
Thôn Ven Sông
Một nơi từng xanh hơn những gì bạn đang thấy.
```

Objective after:

```text
Đi tới Nhà văn hóa
```

## 4. CS1 - Bác Xanh Và Ảnh Cũ

Trigger: player tới vùng Nhà văn hóa lần đầu.

Staging:

- Bác Xanh đứng gần ảnh/bảng "Ven Sông Xanh".
- Camera focus ảnh cũ, rồi chuyển sang Bác Xanh.

Dialogue draft:

```text
Bác Xanh:
Cháu mới tới hả? Đừng nhìn mỗi mấy túi rác kia mà nghĩ Ven Sông lúc nào cũng vậy.

Bác Xanh:
Hồi trước, sân này chiều nào cũng có trẻ con chạy chơi. Người lớn họp xong là tự nhặt ghế, nhặt rác.

Bác Xanh:
Không phải bây giờ ai xấu hơn. Chỉ là mọi thứ tiện hơn, nhanh hơn... còn thói quen giữ chung thì chậm lại.
```

Objective after:

```text
Nhặt rác quanh lối vào Nhà văn hóa
```

## 5. CS1B - Điểm Tập Kết Rác

Trigger: player nhặt xong cụm rác đầu hoặc Bác Xanh dẫn tới Chị Lan.

Staging:

- Camera nhìn Điểm tập kết rác.
- Chị Lan đứng gần thùng/giỏ phân loại.

Dialogue draft:

```text
Chị Lan:
Nhặt được rác mới là một nửa thôi em. Nửa còn lại là cho nó về đúng chỗ.

Bác Xanh:
Ven Sông không thiếu người tốt. Chỉ thiếu một cách làm mà ai cũng nhớ để làm theo.
```

Objective after:

```text
Phân loại rác đầu tiên
```

## 6. CS2 - Cái Túi Nhỏ

Trigger: player gặp Cô Tư ở tạp hóa.

Staging:

- Một vài rác nhỏ quanh tạp hóa: túi nilon, vỏ bánh, chai nước.
- Cô Tư đang bận hoặc đứng trước quầy.

Dialogue draft:

```text
Cô Tư:
Rác trước tiệm hả? Ừ thì có, mà ngày nào cô cũng tính lát dọn.

Cô Tư:
Khách giờ mua đồ mang đi nhiều. Chai nước, bánh gói, túi nilon... tiện thật, mà cũng nhiều thứ bỏ lại hơn.

Player choice:
- "Một cái túi nhỏ cũng có thể thành nhiều."
- "Cô có muốn thử đặt thùng gần đây không?"

Cô Tư:
Một cái thì nhỏ thiệt. Nhưng nếu cả ngày ai cũng một cái... chắc cô phải nhìn lại.
```

Objective after:

```text
Dọn rác quanh tạp hóa
```

## 7. CS3 - Sau Trận Bóng

Trigger: player tới sân bóng.

Staging:

- Sân bóng có rác sau một buổi chơi: chai nước, túi snack.
- Anh Tùng đứng gần sân.
- Bé Na đứng ở rìa sân, hơi ngại bước vào.

Dialogue draft:

```text
Anh Tùng:
Tụi anh đá xong mệt quá, tính lát quay lại dọn. Mấy cái chai thôi mà.

Bé Na:
Nhưng hôm nào cũng "lát". Em nhặt bóng mà cứ sợ dẫm trúng rác.

Anh Tùng:
Ờ... sân này tụi anh chơi nhiều nhất. Mà để người khác dọn hoài cũng kỳ.
```

Objective after:

```text
Dọn rác quanh sân bóng
```

## 8. CS4 - Rác Trôi Theo Nước

Trigger: player gặp Ông Sáu ở bờ sông.

Staging:

- Camera nhìn từ sân bóng qua Ông Sáu rồi xuống bờ sông.
- Một vài rác nằm ở mép nước hoặc mắc vào bụi/cỏ.

Dialogue draft:

```text
Ông Sáu:
Hồi xưa đứng đây nhìn xuống thấy cá quẫy. Giờ nước đục hơn, cá cũng thưa.

Ông Sáu:
Tui đâu có vứt xuống sông. Rác trên bờ thì liên quan gì cá dưới nước?

Bác Xanh:
Cháu nhìn mép nước kia. Gió không hỏi rác của ai. Mưa cũng không hỏi.

Ông Sáu:
Vậy là thứ mình bỏ trên bờ... cũng có ngày xuống sông.
```

Objective after:

```text
Theo dấu rác dọc bờ sông
```

## 9. CS5A - Cống Nghẹt

Trigger: player tới Cống thoát nước cuối xóm.

Staging:

- Camera thấp nhìn rác mắc ở miệng cống.
- Nước chảy chậm hoặc có màu tối hơn nếu có thể.
- Anh Hòa có thể đứng gần cống.

Dialogue draft:

```text
Anh Hòa:
Mỗi lần mưa lớn là nước dềnh lên chỗ này. Người ta tưởng tại mưa, nhưng nhìn đây.

Bác Xanh:
Chai ở sân bóng, túi ở tạp hóa, rác ở bờ sông... cuối cùng lại gặp nhau ở đây.
```

Objective after:

```text
Dọn rác mắc ở cống
```

## 10. CS5B - Dọn Cống Không Đủ

Trigger: player clear cống.

Staging:

- Nước chảy tốt hơn.
- Camera không ăn mừng quá lớn, giữ tone suy nghĩ.

Dialogue draft:

```text
Chị Lan:
Cống thông rồi. Nhưng nếu ngày mai mọi người vẫn bỏ rác như cũ, mình lại quay về đây thôi.

Bác Xanh:
Việc cuối không phải dọn thêm một đống rác. Việc cuối là giúp mỗi người thấy phần nhỏ của mình.
```

Objective after:

```text
Rủ mọi người cùng thay đổi
```

## 11. CS5C - Ngõ Sau Cơn Mưa

Trigger: sau khi player rủ Cô Tư, Anh Tùng và Ông Sáu cùng thay đổi.

Staging:

- Camera hoặc dialogue focus nhìn dọc một đoạn ngõ dân cư.
- 2-3 cụm rác nhỏ nằm ở chỗ thấp: mép mương, cạnh gốc cây, đường đi học.
- Cô Hạnh đứng gần đầu ngõ; Em Phúc đứng gần lối đi học.
- Không cần cinematic dài. Dialogue lock + marker tới 2 inspect spots là đủ.

Dialogue draft:

```text
Cô Hạnh:
Con vừa ở cống về hả? Vậy con nhìn thử ngõ này sau mưa đi.

Em Phúc:
Con đi học ngang đây mỗi ngày. Có bữa mưa xong, rác dồn ngay chỗ con bước qua.

Bác Xanh:
Rác đi xa, rồi có lúc nó quay lại rất gần.
```

Objective after:

```text
Quan sát ngõ sau mưa
```

## 12. CS5D - Chỗ Sống Nhỏ

Trigger: player hoàn thành inspect/cleanup ngõ dân cư.

Staging:

- Camera focus một gốc cây/bụi cỏ nhỏ.
- Có dây nilon/mảnh nhựa ở cạnh gốc cây.
- Nếu có model động vật: cho chim/mèo/cún xuất hiện sau khi dọn. Nếu không có, dùng sound cue, vệt chân, hoặc Bé Na/Em Phúc phản ứng.
- Trồng cây non dùng runtime tree visual hiện có; không cần mechanic mới ngoài placement.

Dialogue draft:

```text
Em Phúc:
Hồi trước chỗ gốc cây này hay có chim xuống uống nước.

Bác Xanh:
Không phải lúc nào mình cũng cần làm chuyện lớn như cứu một con vật.

Bác Xanh:
Nhiều khi chỉ cần chừa lại một chỗ sạch để sự sống tự quay về.

Chị Lan:
Trồng cây không thay thế chuyện bỏ rác đúng chỗ. Nhưng nó nhắc mọi người chăm tiếp mỗi ngày.
```

Objective after:

```text
Dọn góc cây, đặt bát nước và trồng cây non
```

## 13. CS5E - Lời Hứa Nhà Văn Hóa

Trigger: player quay về Nhà văn hóa và nói chuyện Bác Xanh.

Staging:

- Nhà văn hóa sáng hơn.
- NPC chính đứng thành nhóm, không quá nghi thức.
- Cô Hạnh và Em Phúc đứng gần Bé Na hoặc cạnh một cây non runtime.
- Nếu có NPC phụ đã gặp, họ đứng xung quanh.

Dialogue draft:

```text
Cô Tư:
Từ mai cô để thùng ngay trước tiệm. Ai mua xong thì bỏ đúng chỗ, cô nhắc.

Anh Tùng:
Tụi con đá xong sẽ tự dọn sân. Sân của tụi con mà.

Ông Sáu:
Tui ngồi bờ sông mỗi ngày. Ai bỏ rác, tui nhắc liền.

Chị Lan:
Điểm tập kết rác mở sẵn. Miễn mọi người chịu phân loại, tôi hướng dẫn.

Cô Hạnh:
Từ mai mỗi đoạn ngõ có người để ý. Không đợi rác dồn lại mới gọi nhau.

Em Phúc:
Con nhận tưới cây đầu ngõ. Con cũng nhắc mấy bạn đừng đá vỏ bánh xuống mương.

Bé Na:
Con với Phúc sẽ coi góc cây nữa. Nếu chim hay mèo quay lại, tụi con giữ chỗ đó sạch.

Bác Xanh:
Được chứ. Ven Sông xanh lại không phải vì một người làm hết.

Bác Xanh:
Nó xanh lại từ những việc nhỏ mà mọi người không còn xem là nhỏ nữa.
```

End text:

```text
Ven Sông chưa sạch mãi mãi.
Nhưng Ven Sông đã có người cùng chăm.
```
