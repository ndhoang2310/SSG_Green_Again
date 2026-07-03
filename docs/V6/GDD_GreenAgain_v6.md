# Green Again v5 - Game Design Document

> Bản v5 tập trung vào storytelling. Nhặt rác, đặt thùng, dựng biển, trồng cây là hành động minh họa cho câu chuyện, không phải phần thưởng chính.

## 1. High Concept

Green Again v5 là game Roblox kể chuyện giáo dục môi trường tại thôn Ven Sông. Người chơi là một tình nguyện viên mới đến, gặp Bác Xanh và người dân, rồi dần hiểu vì sao một nơi từng xanh lại xuống cấp vì rất nhiều hành động nhỏ.

Core fantasy:

```text
Mình bước vào một ngôi làng từng xanh,
lắng nghe từng người,
nhìn thấy đường đi của rác,
và giúp cộng đồng bắt đầu thay đổi.
```

## 2. Pillars

| Pillar | Nghĩa là gì | Không làm |
|---|---|---|
| Story first | Mỗi chương mở ra một mảnh sự thật về Ven Sông | Không giao nhiệm vụ kiểu "nhặt 10 rác" nếu không có câu chuyện |
| NPC-driven | Người dân là nguồn cảm xúc và thông tin | Không để NPC chỉ làm máy giao quest |
| Small actions, visible consequences | Hành động nhỏ tạo thay đổi nhìn thấy được | Không biến gameplay thành score grind |
| Vietnamese village texture | Địa điểm, lời thoại, thói quen gần Việt Nam | Không dùng tên/địa điểm generic như Picnic Area trong story |
| One hopeful ending | Một ending truyền cảm hứng tại Nhà văn hóa | Không chia ending A/B/C bằng điểm số |

## 3. Player Experience

Player nên đi qua 5 cảm giác:

1. Lạ lẫm: Ven Sông có gì đó đẹp nhưng đang bị bỏ quên.
2. Hiểu nguyên nhân: rác không đến từ một người xấu.
3. Nhìn thấy thói quen: "chỉ một chút thôi" tạo thành nhiều.
4. Nhìn thấy hệ quả: rác không đứng yên, nó đi theo dòng nước.
5. Hy vọng: cộng đồng bắt đầu cùng thay đổi.

## 4. Main Route

```text
Sảnh chờ
-> Spawner map chính
-> Nhà văn hóa / Bác Xanh
-> Điểm tập kết rác
-> Làng / Tạp hóa Cô Tư
-> Sân bóng / Anh Tùng / Bé Na
-> Bờ sông / Ông Sáu
-> Cống thoát nước cuối xóm
-> Nhà văn hóa ending
```

## 5. Chapter Overview

| Chapter | Title | Story question | Main NPC | Main action |
|---|---|---|---|---|
| 1 | Người Lạ Đến Ven Sông | Ven Sông từng xanh như thế nào? | Bác Xanh, Chị Lan | Gặp Bác Xanh, nhặt/phân loại rác đầu |
| 2 | Chỉ Một Chút Thôi Mà | Rác sinh hoạt bắt đầu từ đâu? | Cô Tư | Đi qua làng, nói chuyện tạp hóa, dọn rác nhỏ |
| 3 | Sau Trận Bóng | Nơi vui chơi chung bị ảnh hưởng thế nào? | Anh Tùng, Bé Na | Dọn rác quanh sân bóng, đặt nhắc nhở |
| 4 | Rác Không Đứng Yên | Rác đi đâu sau khi bị bỏ lại? | Ông Sáu | Theo rác ra bờ sông/khúc sông |
| 5 | Cống Cuối Xóm Và Lời Hứa Ven Sông | Làm sao để chuyện không lặp lại? | Bác Xanh, cộng đồng | Dọn cống, gọi cộng đồng, ending |

## 6. Core Loop

```text
Bác Xanh hoặc NPC đặt vấn đề
-> marker dẫn tới địa điểm/người cần gặp
-> player quan sát bối cảnh
-> trò chuyện để hiểu nguyên nhân
-> làm một hành động nhỏ
-> NPC phản ứng / môi trường đổi nhẹ
-> Sổ tay Ven Sông ghi điều vừa học
```

## 7. Story Gameplay Rules

- Không bắt đầu bằng "nhặt rác ngay" nếu chưa có cảm xúc hoặc bối cảnh.
- Mỗi hành động cleanup phải trả lời: player vừa hiểu điều gì?
- Mỗi NPC chính phải có thay đổi nhỏ trước và sau chương.
- Marker chỉ dẫn rõ, nhưng không thay thế lời dẫn của Bác Xanh/NPC.
- Sổ tay là nơi chốt bài học bằng ngôn ngữ mềm, không giảng đạo đức.

## 8. Ending

V5 chỉ có 1 ending chính.

Trigger:

1. Cống cuối xóm được xử lý.
2. Cộng đồng có ít nhất vài hành động phòng ngừa.
3. Player quay về Nhà văn hóa.
4. Nói chuyện với Bác Xanh để chạy ending sequence.

Ending message:

> Ven Sông không xanh lại vì một người dọn sạch mọi thứ. Ven Sông xanh lại vì mọi người bắt đầu thấy phần việc nhỏ của mình.

## 9. Required Companion Docs

- `README.md`: hướng dẫn dùng tài liệu nào khi nào.
- `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`: map theo cụm địa điểm thật.
- `GDD_GreenAgain_v5_STORY_BIBLE.md`: lore, tone, nhân vật, arc.
- `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`: cutscene và staging từng chương.
- `GDD_GreenAgain_NPC_DIALOGUE_v5.md`: thoại NPC và ambient lines.
- `GDD_GreenAgain_v5_QUEST_FLOW.md`: quest IDs, trigger, marker, state.
- `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`: plan implement chi tiết theo milestone.
