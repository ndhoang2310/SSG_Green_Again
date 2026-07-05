# Green Again v6 - NPC Dialogue Script

> Thoại v6 là gameplay chính. Nhặt rác, phân loại, đặt thùng, dựng biển chỉ là hành động sau khi người chơi đã hiểu một mảnh câu chuyện.

## 1. Dialogue Philosophy

Dialogue không được là "NPC nói một câu rồi giao việc". Mỗi cuộc trò chuyện chính cần có nhịp:

```text
1. Hook: NPC nói một câu đời thường hoặc có cảm xúc.
2. Context: NPC kể hoàn cảnh của mình.
3. Friction: NPC có niềm tin sai, né tránh, hoặc chưa nhìn thấy hậu quả.
4. Player response: player hỏi, lắng nghe, hoặc đề nghị giúp.
5. Turn: NPC bắt đầu nhìn vấn đề khác đi.
6. Objective: hành động gameplay xuất hiện như hệ quả tự nhiên.
7. Aftermath: NPC phản ứng sau khi player làm xong.
```

Quy tắc:

- Một dialogue chính có thể dài 8-16 line, chia thành nhiều bubble.
- Một bubble nên ngắn, dễ đọc.
- NPC nói như người trong làng, không nói như sách giáo khoa.
- Player không phán xét. Player hỏi, giúp, hoặc nhắc điều vừa quan sát.
- Mỗi chương cần ít nhất một cuộc trò chuyện đủ sâu để truyền tải câu chuyện.

## 2. Dialogue States

| State | Mục đích |
|---|---|
| `BeforeQuest` | Tạo đời sống trước khi NPC thành mục tiêu chính |
| `IntroConversation` | Cuộc trò chuyện chính mở vấn đề |
| `PlayerChoice` | 1-2 lựa chọn phản hồi, không cần phân nhánh lớn |
| `DuringQuest` | Nhắc nhẹ khi player đang làm |
| `AfterQuestConversation` | NPC nhận ra điều gì |
| `ChapterTransition` | Bác Xanh hoặc NPC nối sang chương sau |
| `EndingCommitment` | NPC nói cam kết ở Nhà văn hóa |
| `PostEnding` | Free-roam sau ending |

## 3. Bác Xanh

Tone: ấm, chậm, giàu ký ức. Bác không giao việc như người quản lý; bác dẫn người chơi nhìn kỹ hơn.

### Ch1 - IntroConversation: Bác Xanh Và Ảnh Cũ

Trigger: player tới Nhà văn hóa lần đầu.

```text
Bác Xanh:
Cháu mới tới Ven Sông phải không?

Player:
Dạ. Cháu thấy quanh đây có nhiều rác quá.

Bác Xanh:
Ừ, bác cũng thấy. Nhưng cháu đừng để mấy túi rác kia kể hết câu chuyện về nơi này.

Bác Xanh:
Nhìn tấm ảnh cũ bên kia đi. Hồi trước sân Nhà văn hóa chiều nào cũng đông. Trẻ con chạy chơi, người lớn họp xong thì ai cũng tự nhặt phần mình.

Player:
Vậy sao bây giờ lại khác vậy bác?

Bác Xanh:
Không phải vì người dân xấu đi. Cuộc sống chỉ nhanh hơn. Đồ mua mang đi nhiều hơn. Túi, chai, hộp... tiện hơn.

Bác Xanh:
Mà khi mọi thứ tiện quá, người ta dễ nghĩ một cái vỏ nhỏ không đáng kể.

Player:
Cháu có thể giúp gì trước không?

Bác Xanh:
Giúp bác nhìn kỹ đoạn đường vào Nhà văn hóa đã. Nhặt vài thứ trước mắt, rồi mình đem về đúng chỗ.

Bác Xanh:
Rác không biến mất chỉ vì mình nhặt nó lên. Nó cần có nơi để đi.
```

Objective:

```text
Nhặt rác quanh lối vào Nhà văn hóa
```

### Ch1 - After First Cleanup

```text
Bác Xanh:
Đường nhìn thoáng hơn rồi.

Player:
Nhặt lên mới thấy nhiều thứ nhỏ thật bác.

Bác Xanh:
Ừ. Thứ nhỏ nằm một mình thì dễ bỏ qua. Nằm chung lại thì thành câu chuyện khác.

Bác Xanh:
Đi với bác tới điểm tập kết rác. Chị Lan sẽ chỉ cháu phần còn lại.
```

Objective:

```text
Tới Điểm tập kết rác gặp Chị Lan
```

### Chapter Transitions

Ch2:

```text
Bác Xanh:
Muốn hiểu rác bắt đầu từ đâu, cháu ghé tạp hóa Cô Tư trước.

Bác Xanh:
Chuyện lớn nhiều khi bắt đầu từ một cái túi nhỏ, mà người ta cầm trên tay chưa kịp nghĩ tới.
```

Ch3:

```text
Bác Xanh:
Ở tạp hóa, rác đến từ thói quen hằng ngày.

Bác Xanh:
Còn ở sân bóng, nó đến từ những lúc vui nhất. Khi người ta vui, người ta càng dễ nghĩ "lát nữa tính".
```

Ch4:

```text
Bác Xanh:
Rác quanh sân bóng còn dễ thấy.

Bác Xanh:
Nhưng có thứ không ở yên trên sân. Gió cuốn, mưa kéo, rồi nó đi xuống sông.
```

Ch5:

```text
Bác Xanh:
Mình đã thấy rác đi tới đâu.

Bác Xanh:
Giờ phải xem nó mắc lại ở đâu, và làm sao để cả làng không để chuyện đó lặp lại.
```

### EndingCommitment

```text
Bác Xanh:
Hôm nay Nhà văn hóa sáng hơn mọi hôm.

Bác Xanh:
Không phải vì sân đã sạch mãi mãi. Không ai hứa được chuyện đó.

Bác Xanh:
Nhưng hôm nay, mỗi người ở đây đã thấy phần việc nhỏ của mình.

Bác Xanh:
Cháu không làm Ven Sông xanh lại một mình.

Bác Xanh:
Cháu giúp mọi người nhớ rằng từng việc nhỏ đều để lại dấu vết.

Bác Xanh:
Mà nếu từng việc nhỏ có thể làm nơi này xấu đi, thì từng việc nhỏ cũng có thể làm nơi này xanh lại.
```

## 4. Chị Lan

Tone: thực tế, rõ ràng, hơi mệt vì lâu nay làm một mình. Chị là người biến cảm xúc thành cách làm.

### Ch1 - IntroConversation: Rác Đi Đâu?

Trigger: player tới Điểm tập kết rác sau khi nhặt rác đầu.

```text
Chị Lan:
Em đem rác tới hả? Để chị xem.

Player:
Em nhặt quanh lối vào Nhà văn hóa. Tưởng ít mà gom lại cũng nhiều.

Chị Lan:
Đúng rồi. Nhưng nhặt được rác mới là một nửa thôi.

Player:
Nửa còn lại là phân loại ạ?

Chị Lan:
Ừ. Nếu chai nhựa, đồ ăn thừa, giấy ướt, pin cũ lẫn hết vào nhau thì sau này xử lý cực hơn nhiều.

Chị Lan:
Nhiều người nghĩ bỏ vào một bao là xong. Với họ thì xong, nhưng với người gom rác thì mọi thứ mới bắt đầu.

Bác Xanh:
Ven Sông không thiếu người muốn sạch. Chỉ thiếu một cách làm mà ai cũng nhớ để làm theo.

Player:
Chị chỉ em phân loại lượt này với.

Chị Lan:
Được. Chai nhựa để bên này. Giấy khô bên kia. Đồ ăn thừa để riêng. Mấy thứ nguy hiểm thì đừng bỏ chung.
```

Objective:

```text
Phân loại rác đầu tiên tại Điểm tập kết rác
```

### DuringQuest

```text
Chị Lan:
Nhìn nhãn hoặc chất liệu trước.

Chị Lan:
Không chắc thì hỏi chị. Phân loại đúng từ đầu đỡ mất công sửa sau.
```

### AfterQuestConversation

```text
Player:
Xong rồi chị.

Chị Lan:
Tốt đó. Thấy không, không khó. Chỉ cần đừng vội quăng chung hết.

Player:
Sao ít người dùng điểm này vậy chị?

Chị Lan:
Vì ai cũng nghĩ rác của mình ít. Mà đường từ "ít" tới "nhiều" ngắn lắm em.

Chị Lan:
Nếu sau này em nói chuyện với mọi người, nhắc họ đem rác về đây. Một mình chị nhắc hoài không xuể.
```

Notebook:

```text
Nhặt rác mới là một nửa. Nửa còn lại là cho rác về đúng chỗ.
```

### Ch5 - Cống thông nhưng chưa xong

```text
Chị Lan:
Cống thông rồi, nhưng chị không thấy nhẹ hẳn.

Player:
Vì rác có thể quay lại?

Chị Lan:
Ừ. Nếu tạp hóa vẫn không có thùng, sân bóng vẫn để chai lung tung, bờ sông vẫn không ai nhắc... mình sẽ lại đứng trước cái cống này.

Chị Lan:
Mình cần đặt chỗ bỏ rác dễ thấy, biển nhắc dễ nhớ, và người dân chịu nhắc nhau.
```

### EndingCommitment

```text
Chị Lan:
Điểm tập kết rác mở sẵn.

Chị Lan:
Ai chưa biết phân loại cứ đem tới, tôi hướng dẫn. Nhưng từ mai, mong mọi người đừng để rác đi lạc trước khi tới đây.
```

## 5. Cô Tư

Tone: bận rộn, thực tế, đáng mến. Ban đầu hơi phòng thủ vì không muốn bị xem là người gây bẩn.

### BeforeQuest

```text
Cô Tư:
Mua gì không con? Nước suối, bánh, kẹo đủ cả.

Cô Tư:
À, tình nguyện viên hả? Cô bán cả ngày nên trước tiệm hơi bừa chút, lát cô dọn.
```

### Ch2 - IntroConversation: Cái Túi Nhỏ

Trigger: player gặp Cô Tư theo quest.

```text
Player:
Cô Tư ơi, Bác Xanh bảo cháu ghé đây để hiểu chuyện rác trong làng.

Cô Tư:
Trời, bác Xanh lại lo xa rồi. Trước tiệm cô có rác thiệt, nhưng cô vẫn quét mà.

Player:
Cháu thấy nhiều túi nhỏ, vỏ bánh, chai nước quanh đường.

Cô Tư:
Khách giờ ai cũng vội. Mua chai nước, gói bánh, cái túi nilon cho tiện. Cô không đưa túi thì họ than khó cầm.

Cô Tư:
Ngày xưa bán ít hơn. Có khi người ta đem rổ, đem giỏ. Giờ thì cái gì cũng gói sẵn.

Player:
Cô có nghĩ mấy thứ nhỏ đó trôi đi đâu không?

Cô Tư:
Thú thật là cô ít nghĩ. Cô chỉ thấy trước tiệm bẩn thì quét. Cái nào bay xa rồi thì... chắc người khác dọn.

Player choice:
1. "Một cái túi nhỏ, nhưng cả ngày nhiều người cùng bỏ thì sao cô?"
2. "Cháu dọn phụ cô một lượt, rồi mình nhìn lại thử nhé."

Cô Tư:
Ừ, con nói vậy thì cô cũng muốn xem. Chứ nhiều khi mình quen mắt rồi, không thấy nó nhiều nữa.
```

Objective:

```text
Dọn rác quanh tạp hóa và đoạn đường gần đó
```

### DuringQuest

```text
Cô Tư:
Con coi gần gốc cây với cạnh đường đó.

Cô Tư:
Mấy cái vỏ nhỏ nhỏ bị đá vào chỗ khuất, cô quét ngoài mặt đường không thấy.
```

### AfterQuestConversation

```text
Player:
Cô Tư, tụi mình gom được từng này.

Cô Tư:
Nhiều vậy hả? Cô tưởng chỉ vài cái vỏ bánh thôi.

Player:
Mỗi cái đều nhỏ. Nhưng gom lại thì không nhỏ nữa.

Cô Tư:
Cô hiểu rồi. Trước giờ cô cứ nghĩ rác trước tiệm là chuyện cô quét lúc rảnh.

Cô Tư:
Nhưng nếu khách mua ở đây, rác từ đây bay ra đường, rồi trôi đi chỗ khác... cô cũng có phần trong đó.

Player:
Mình đặt thùng gần đây được không cô?

Cô Tư:
Được. Cô còn nhắc khách nữa. Nói nhẹ thôi, nhưng ngày nào cũng nói thì chắc thành quen.
```

Next beat:

```text
Sau đoạn này, quest chuyển sang `Q2_06_TalkToBacXanh`.
```

### Bác Xanh - Q2 After Grocery

Trigger: player gặp Bác Xanh ngoài tạp hóa sau khi nói lại với Cô Tư.

```text
Bác Xanh:
Cháu thấy đó, tiệm tạp hóa cũng là một phần của câu chuyện.

Bác Xanh:
Còn ở sân bóng, rác đến từ những lúc vui nhất. Khi người ta vui, người ta càng dễ nghĩ lát nữa tính.
```

Notebook:

```text
Một cái túi nhỏ không nhỏ nữa nếu cả làng đều nghĩ vậy.
```

### EndingCommitment

```text
Cô Tư:
Từ mai cô để thùng ngay trước tiệm.

Cô Tư:
Ai mua xong cô nhắc bỏ đúng chỗ. Cô cũng bớt đưa túi nếu khách không cần.

Cô Tư:
Tiệm nhỏ thì phần việc cũng nhỏ thôi, nhưng cô làm được.
```

## 6. Anh Tùng

Tone: vui, hơi xuề xòa, nói như thanh niên trong làng. Không xấu tính; chỉ quen vô tư.

### BeforeQuest

```text
Anh Tùng:
Ra sân bóng không? Chiều nay tụi anh đá vui lắm.

Anh Tùng:
À, mấy cái chai kia tụi anh tính lát dọn. Đá xong ai cũng mệt mà.
```

### Ch3 - IntroConversation: Sau Trận Bóng

Trigger: player tới sân bóng.

```text
Player:
Anh Tùng, sân bóng nhiều chai nước quá.

Anh Tùng:
Có mấy chai thôi mà. Tụi anh đá xong mệt, lát quay lại dọn cũng được.

Bé Na:
Hôm nào anh cũng nói lát.

Anh Tùng:
Ủa Na, em ở đây hả?

Bé Na:
Em nhặt bóng giúp mấy anh mà. Bóng lăn vào chỗ rác, em không dám lấy.

Anh Tùng:
Thì... để anh lấy cho. Rác đó đâu tới mức ghê vậy.

Player:
Nếu sân này là chỗ mọi người cùng chơi, ai sẽ là người dọn?

Anh Tùng:
Chắc... ai rảnh? Hoặc cô chú dọn vệ sinh?

Bé Na:
Nhưng người chơi nhiều nhất là mấy anh mà.

Anh Tùng:
Ờ. Nghe cũng hơi kỳ. Tụi anh dùng sân nhiều nhất mà cứ để người khác dọn.

Player choice:
1. "Mình dọn thử một vòng rồi nhìn sân khác thế nào nhé."
2. "Anh giúp em chỉ những chỗ tụi anh hay để chai đi."

Anh Tùng:
Được. Mấy chỗ ghế ngồi với sau khung thành trước. Tụi anh hay để đồ ở đó.
```

Objective:

```text
Dọn rác quanh sân bóng
```

### DuringQuest

```text
Anh Tùng:
Sau khung thành còn mấy chai đó.

Anh Tùng:
Ê, nhìn vậy mới thấy tụi anh để hơi nhiều thật.
```

### AfterQuestConversation

```text
Player:
Sân sạch hơn rồi.

Bé Na:
Giờ em chạy nhặt bóng được.

Anh Tùng:
Nhìn khác hẳn. Mà thật ra dọn cũng đâu lâu.

Player:
Khó nhất chắc là nhớ dọn sau khi chơi.

Anh Tùng:
Ừ. Lúc vui thì ai cũng nghĩ "lát nữa". Nhưng lát nữa thường thành ngày mai.

Anh Tùng:
Lần sau đá xong anh rủ tụi nó gom chai lại. Sân của tụi anh mà.
```

Notebook:

```text
Không gian chung chỉ sạch nếu người dùng nó cũng xem đó là trách nhiệm của mình.
```

### EndingCommitment

```text
Anh Tùng:
Tụi con đá xong sẽ tự dọn sân.

Anh Tùng:
Không phải làm màu đâu. Sân của tụi con mà để bẩn thì tụi con chịu trước.
```

## 7. Bé Na

Tone: ngắn, thật, nhìn vấn đề bằng cảm giác trực tiếp. Bé Na không giảng, chỉ nói điều em thấy.

### Ch3 - Intro Add-on

```text
Bé Na:
Em thích sân này lắm.

Bé Na:
Nhưng có bữa bóng lăn vào chỗ rác, em đứng nhìn thôi. Em sợ dẫm trúng cái gì dơ.

Player:
Em có nói với mấy anh chưa?

Bé Na:
Em có nói. Mấy anh bảo lát dọn.

Bé Na:
Nhưng "lát" lâu lắm.
```

### After sân bóng

```text
Bé Na:
Sạch hơn rồi.

Bé Na:
Không phải sáng bóng như mới, nhưng em thấy muốn chạy vào sân hơn.

Player:
Mai em rủ bạn ra chơi được rồi đó.

Bé Na:
Em sẽ rủ. Nhưng em cũng sẽ nhắc mấy bạn bỏ rác vào thùng.
```

### Ch4 Optional

```text
Bé Na:
Nếu rác trôi xuống sông, cá có bị đau không?

Bác Xanh:
Cá không nói được như mình. Nên mình phải nhìn kỹ hơn.
```

### EndingCommitment

```text
Bé Na:
Vậy mai tụi con chơi bóng được không?

Bé Na:
Con sẽ nhắc mấy bạn bỏ rác đúng chỗ. Nếu con quên, anh Tùng nhắc con nha.
```

## 8. Ông Sáu

Tone: chậm, hoài niệm, hơi cứng đầu lúc đầu. Ông không phủ nhận ô nhiễm, chỉ chưa thấy mình liên quan.

### BeforeQuest

```text
Ông Sáu:
Ngồi đây nhìn sông quen rồi.

Ông Sáu:
Hồi trước cá quẫy sát bờ, giờ thưa lắm. Chắc tại mùa, chắc tại nước đổi.
```

### Ch4 - IntroConversation: Rác Trôi Theo Nước

Trigger: player gặp Ông Sáu sau sân bóng.

```text
Player:
Ông Sáu, Bác Xanh bảo cháu xuống bờ sông xem rác đi đâu.

Ông Sáu:
Rác thì ở trên bờ, dưới nước là chuyện của nước chứ.

Player:
Ông hay câu cá ở đây ạ?

Ông Sáu:
Ừ. Hồi xưa ngồi một lát là thấy cá quẫy. Giờ có khi cả buổi chẳng thấy gì.

Player:
Ông có nghĩ rác trên bờ ảnh hưởng tới sông không?

Ông Sáu:
Tui đâu có vứt xuống sông. Tui ngồi đây còn nhặt dây câu của mình đem về.

Bác Xanh:
Ông Sáu không vứt xuống sông. Nhưng gió không hỏi rác của ai. Mưa cũng không hỏi.

Player:
Chỗ bụi cỏ kia có mấy túi mắc lại. Có thể nước kéo từ trên xuống không ông?

Ông Sáu:
Hừm... chỗ đó sau mưa hay đầy rác thật.

Ông Sáu:
Nếu cháu muốn nhìn kỹ, đi dọc mép nước. Tui chỉ mấy chỗ rác hay mắc.
```

Objective:

```text
Theo dấu rác dọc bờ sông
```

### DuringQuest

```text
Ông Sáu:
Chỗ bụi cỏ kia.

Ông Sáu:
Nước lên là rác mắc lại đó, rồi bữa sau lại trôi tiếp.
```

### AfterQuestConversation

```text
Player:
Rác mắc dọc bờ nhiều hơn cháu nghĩ.

Ông Sáu:
Tui ngồi đây mỗi ngày mà nhìn quen mắt mất rồi.

Player:
Có thứ từ sân bóng, có thứ giống túi ở tạp hóa.

Ông Sáu:
Vậy là rác không ở yên chỗ người ta bỏ.

Bác Xanh:
Nó đi theo đường nước. Và nơi nhận hậu quả nhiều khi không phải nơi bắt đầu.

Ông Sáu:
Tui cứ nói mình không vứt xuống sông là đủ. Chắc chưa đủ thật.
```

Notebook:

```text
Rác không biến mất. Nó chỉ chuyển chỗ, và nơi nhận hậu quả có thể là sông.
```

### EndingCommitment

```text
Ông Sáu:
Tui ngồi bờ sông mỗi ngày.

Ông Sáu:
Ai bỏ rác, tui nhắc liền. Nhắc nhẹ thôi, nhưng không làm ngơ nữa.
```

## 9. Chapter 5 Community Conversations

Chapter 5 cần nhiều đoạn ngắn nối lại câu chuyện, không chỉ một ending line.

### Anh Hòa - Cống Nghẹt

```text
Anh Hòa:
Mỗi lần mưa lớn là nước dềnh lên chỗ này.

Player:
Do cống nhỏ quá hả anh?

Anh Hòa:
Cống nhỏ là một phần. Nhưng nhìn miệng cống đi.

Anh Hòa:
Chai nước, túi nilon, bao snack, lá mục... thứ nào cũng nhỏ. Gặp nhau ở đây thì thành nút chặn.

Bác Xanh:
Rác từ nhiều nơi cuối cùng lại biết đường gặp nhau.

Anh Hòa:
Thông được hôm nay thì tốt. Nhưng nếu trên kia vẫn xả như cũ, cống này chỉ nghỉ được vài bữa.
```

Objective:

```text
Dọn rác mắc ở cống
```

### After Clear Drain - Bác Xanh + Chị Lan

```text
Player:
Nước chảy lại rồi.

Chị Lan:
Ừ, nhưng chị không muốn tuần sau lại đứng đây.

Bác Xanh:
Dọn cống là xử lý phần cuối của câu chuyện.

Player:
Vậy phần đầu là tạp hóa, sân bóng, bờ sông?

Bác Xanh:
Và cả những lúc mọi người nghĩ "một chút thôi mà".

Chị Lan:
Mình cần rủ mọi người đặt lại cách làm. Có chỗ bỏ rác. Có người nhắc. Có điểm tập kết thật sự được dùng.
```

Objective:

```text
Rủ mọi người cùng thay đổi
```

### Gather Community - Cô Tư

```text
Player:
Cô Tư, tụi cháu thấy túi nilon mắc ở cống.

Cô Tư:
Cô nghe mà chột dạ. Không biết có cái nào từ tiệm cô không.

Player:
Không cần biết cái nào của ai. Nhưng mình biết rác ở tiệm có thể đi xa.

Cô Tư:
Ừ. Vậy cô nhận phần tiệm cô.

Cô Tư:
Thùng rác để ngay trước cửa. Khách mua xong cô nhắc. Ai không cần túi thì cô khỏi đưa.
```

### Gather Community - Anh Tùng

```text
Player:
Anh Tùng, có bao snack giống loại tụi anh hay ăn mắc ở cống.

Anh Tùng:
Nghe quê thiệt.

Player:
Không phải để trách anh. Nhưng sân bóng nối với bờ sông gần hơn mình nghĩ.

Anh Tùng:
Ừ. Tụi anh đá xong mà không gom, gió với mưa gom giùm. Mà gom tới chỗ tệ hơn.

Anh Tùng:
Để anh rủ tụi nó làm luật sân: đá xong gom chai, gom túi rồi mới về.
```

### Gather Community - Ông Sáu

```text
Player:
Ông Sáu, rác từ bờ sông trôi xuống cống thật rồi.

Ông Sáu:
Tui thấy. Nhìn cái cống nghẹt mới hết cãi được.

Player:
Ông vẫn ngồi bờ sông mỗi ngày chứ?

Ông Sáu:
Ngồi chứ. Từ mai tui ngồi thêm một việc nữa: ai bỏ rác, tui nhắc.

Ông Sáu:
Sông không tự lên tiếng được. Người ngồi cạnh sông phải lên tiếng giùm.
```

### Residential After Rain - Cô Hạnh + Em Phúc

Trigger: sau khi player đã rủ Cô Tư, Anh Tùng và Ông Sáu nhận phần việc. Marker dẫn về `ResidentialSt` / `ResidentialLane`.

```text
Cô Hạnh:
Con vừa ở cống về hả? Vậy con nhìn thử ngõ này sau mưa đi.

Player:
Cháu tưởng cống nghẹt thì chỉ ảnh hưởng ở cuối xóm.

Cô Hạnh:
Không đâu. Nước dềnh lên là rác quay ngược về mấy đoạn thấp. Sáng ra người đi học, người đi chợ đều phải né.

Em Phúc:
Con đi học ngang đây mỗi ngày. Có bữa mưa xong, vỏ bánh với túi nilon dồn ngay chỗ con bước qua.

Player:
Vậy khu dân cư cũng là một phần của đường rác.

Cô Hạnh:
Ừ. Trước giờ cô hay nhắc chung bằng loa. Nhưng nhắc chung thì dễ trôi đi như nước.

Em Phúc:
Nếu mỗi nhà giữ đoạn trước cửa mình, tụi con đi học đỡ phải né rác.

Cô Hạnh:
Con giúp cô nhìn lại mấy điểm thấp trong ngõ. Mình không đợi tới ngày tổng vệ sinh nữa.
```

Objective:

```text
Quan sát ngõ sau mưa và dọn vài điểm rác thấp
```

Notebook add-on:

```text
Rác không chỉ đi ra xa. Khi mưa xuống, hậu quả có thể quay lại ngay trước ngõ nhà mình.
```

### Care Small Lives - Góc Sống Nhỏ

Trigger: sau `ResidentialAfterRain`, marker dẫn tới một gốc cây/bụi cỏ gần khu dân cư.

Implementation note: không cần hệ thống rescue. Dùng 2-3 interact đơn giản: dọn mảnh nhựa/dây nilon, đặt bát nước hoặc biển nhỏ, sau đó hiện prop/sound cue chim/mèo/cún.

```text
Em Phúc:
Hồi trước chỗ gốc cây này hay có chim xuống uống nước.

Bé Na:
Em cũng từng thấy một con mèo nằm ở đây. Mấy hôm nay nó tránh ra xa.

Player:
Chắc vì rác mắc quanh gốc cây?

Em Phúc:
Dạ. Có cả dây nilon nữa. Nhìn nhỏ thôi, nhưng tụi nó đâu biết gỡ như mình.

Bác Xanh:
Không phải lúc nào mình cũng cần làm chuyện lớn như "cứu" một con vật.

Bác Xanh:
Nhiều khi chỉ cần chừa lại một chỗ sạch để sự sống tự quay về.

Player:
Mình dọn góc này rồi đặt một bát nước nhỏ được không?

Bé Na:
Được ạ. Mai tụi con đi qua còn nhớ xem cây có cần tưới không.
```

Objective:

```text
Dọn góc cây và đặt bát nước/biển nhỏ
```

After action:

```text
Em Phúc:
Nhìn thoáng hơn rồi. Chỉ là một góc nhỏ thôi, nhưng con thấy dễ thở hơn.

Bé Na:
Nếu tụi nó quay lại, tụi con sẽ giữ chỗ này sạch.
```

### Neighborhood Planting - Mỗi Nhà Một Bóng Cây

Trigger: sau `CareSmallLives`.

```text
Cô Hạnh:
Dọn xong rồi, mình cần thứ gì đó để mọi người nhớ chăm tiếp.

Player:
Trồng cây được không cô?

Cô Hạnh:
Được. Một cây ở đầu ngõ, một cây gần Nhà văn hóa, một cây gần bờ sông.

Chị Lan:
Trồng cây không thay thế chuyện bỏ rác đúng chỗ. Nhưng nó nhắc mọi người rằng chỗ sạch cần được chăm mỗi ngày.

Em Phúc:
Con nhận tưới cây đầu ngõ. Nhưng nếu con quên, cô Hạnh nhắc con nha.

Cô Hạnh:
Cô nhắc. Rồi con nhắc lại cô khi cô quên.
```

Objective:

```text
Trồng cây non và đặt phòng ngừa ở khu làng
```

## 10. Ending Scene Dialogue

Trigger: player nói chuyện với Bác Xanh ở Nhà văn hóa sau Q5.

```text
Bác Xanh:
Mọi người tới đủ rồi.

Bác Xanh:
Hôm nay mình không họp để khen ai. Mình họp để nhớ một chuyện đơn giản: Ven Sông là chỗ chung.

Chị Lan:
Điểm tập kết rác mở sẵn. Ai chưa biết phân loại cứ đem tới, tôi hướng dẫn.

Cô Tư:
Tạp hóa của tôi sẽ có thùng rác trước cửa. Tôi cũng bớt đưa túi nếu khách không cần.

Anh Tùng:
Sân bóng tụi con chơi thì tụi con dọn. Đá xong mới được về.

Ông Sáu:
Tui ngồi bờ sông mỗi ngày. Tui sẽ nhắc người câu cá, người đi ngang, và nhắc cả tui nữa.

Cô Hạnh:
Tổ dân phố sẽ chia việc nhỏ theo từng đoạn ngõ. Không đợi tới lúc rác dồn lại mới gọi nhau đi dọn.

Em Phúc:
Con nhận tưới cây đầu ngõ. Con cũng nhắc mấy bạn đừng đá vỏ bánh xuống mương.

Bé Na:
Con với Phúc sẽ coi góc cây nữa. Nếu chim hay mèo quay lại, tụi con giữ chỗ đó sạch.

Bác Xanh:
Nghe chưa? Không ai nhận làm hết. Mỗi người nhận một phần nhỏ.

Bác Xanh:
Ngày trước Ven Sông xanh vì người ta nhớ phần nhỏ đó.

Bác Xanh:
Từ hôm nay, mình nhớ lại.

Player:
Ven Sông sẽ xanh lại chứ bác?

Bác Xanh:
Không phải trong một ngày.

Bác Xanh:
Nhưng hôm nay là một ngày Ven Sông bắt đầu xanh lại.
```

End text:

```text
Ven Sông chưa sạch mãi mãi.
Nhưng Ven Sông đã có người cùng chăm.
```

## 11. NPC Phụ - Expanded Lines

NPC phụ không cần hội thoại dài như NPC chính, nhưng mỗi người nên có ít nhất before/after để tạo cảm giác làng thay đổi.

### Bác Bảy bảo vệ Nhà văn hóa

Before:

```text
Hồi trước họp xong ai cũng tự nhặt một tay.
Giờ người ta vội, nhiều khi quên mất đây là sân chung.
```

After:

```text
Chiều nay sân Nhà văn hóa sáng hơn.
Không phải vì đèn mới đâu. Vì có người chịu nhìn xuống đất nhặt lên.
```

### Chú Minh xe rác

Before:

```text
Rác mà lẫn hết vào nhau thì chở đi cũng cực.
Người ta thấy xe rác tới là tưởng xong, nhưng tụi chú còn cả đoạn sau.
```

After:

```text
Phân loại từ đầu là đỡ cho cả người gom rác.
Làng mà làm đều, tụi chú cũng nhẹ hơn nhiều.
```

### Cô Hạnh tổ dân phố

Before:

```text
Nhắc thì ai cũng gật, nhất là trong buổi họp.
Khó là sáng hôm sau, trước cửa nhà mình, mọi người còn nhớ không.
```

After:

```text
Từ mai cô chia từng đoạn ngõ cho từng nhóm nhà.
Không phải để bắt lỗi nhau. Để ai cũng có một phần nhỏ dễ nhớ.
```

### Em Phúc học sinh

Before:

```text
Con đi học ngang đây mỗi ngày.
Có hôm mưa, rác dồn ngay chỗ con bước qua.
```

After:

```text
Nếu đường sạch hơn, tụi con đi học cũng vui hơn.
Con sẽ nhắc mấy bạn đừng đá vỏ bánh xuống mương, rồi tưới cây đầu ngõ nữa.
```

### Dì Năm bán nước

Before:

```text
Bán nước gần sân bóng vui lắm, mà chai bỏ lại cũng nhiều.
Nhiều khi dì bận bán, quay ra đã thấy chai lăn khắp nơi.
```

After:

```text
Nếu có thùng gần sân, dì nhắc khách bỏ vào.
Bán nước cũng phải giữ chỗ bán sạch chứ.
```

### Nam thủ môn

Before:

```text
Tui bắt bóng dở, dọn sân chắc khá hơn.
Nói chứ đá xong ai cũng mệt nên hay chuồn lẹ.
```

After:

```text
Từ mai thua trận thì đội thua gom rác trước.
Đội thắng cũng gom, không là kỳ.
```

### Cô Mai phụ huynh

Before:

```text
Tụi nhỏ mê sân này.
Nhưng rác nhiều quá cô cũng ngại cho tụi nó chạy lung tung.
```

After:

```text
Sân sạch hơn thì người lớn yên tâm hơn.
Tụi nhỏ có chỗ chơi, người lớn cũng bớt lo.
```

### Chú Lộc câu cá

Before:

```text
Tui cứ tưởng cá ít là do mùa.
Rác trên bờ nhìn riết cũng quen mắt.
```

After:

```text
Giờ nhìn rác mắc ở bờ mới thấy mình cũng phải để ý.
Câu cá thì cũng phải giữ chỗ cá sống.
```

### Bà Tám ven sông

Before:

```text
Hồi xưa nước trong tới mức nhìn thấy đáy.
Tui nói vậy tụi nhỏ tưởng tui kể chuyện cổ tích.
```

After:

```text
Muốn xanh lại chắc không thể chỉ nhớ chuyện xưa.
Phải làm mấy chuyện nhỏ hôm nay nữa.
```

### Anh Hòa thợ sửa cống

Before:

```text
Mưa xuống là nước dềnh lên, không phải tự nhiên đâu.
Cống nghẹt vì rác nhỏ gom lại thành đống lớn.
```

After:

```text
Thông cống một lần thì được.
Nhưng giữ cho nó khỏi nghẹt lại mới là chuyện của cả xóm.
```
