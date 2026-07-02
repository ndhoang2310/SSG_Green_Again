# Green Again Docs Guide

> Dùng file này trước khi đọc hoặc sửa docs. Mục tiêu là tránh đọc nhầm tài liệu cũ và tránh viết trùng nội dung.

## 1. Current Source Of Truth

V5 là hướng hiện tại của project. Khi build gameplay/story mới, ưu tiên đọc các file này theo thứ tự:

1. `GDD_GreenAgain_v5.md`
   - Dùng khi cần hiểu tổng quan game v5, pillars, main route, chapter overview và ending.
   - Đây là cửa vào chính.

2. `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
   - Dùng khi cần hiểu map hiện tại theo cụm địa điểm.
   - Source chính cho route: Nhà văn hóa -> Tạp hóa -> Sân bóng -> Ông Sáu/bờ sông -> Cống -> Nhà văn hóa.
   - Dùng để kiểm tra tên kỹ thuật cũ như `PicnicArea`, `Dam_C1/C2/C3`, `Portal1Destination` nên hiển thị thế nào trong story.

3. `GDD_GreenAgain_v5_STORY_BIBLE.md`
   - Dùng khi viết/cải thiện story, tone, arc nhân vật, theme.
   - Không dùng để lấy quest IDs hoặc implementation details.

4. `GDD_GreenAgain_NPC_DIALOGUE_v5.md`
   - Dùng khi viết thoại NPC, dialogue state, hội thoại chính/phụ.
   - Đây là source chính cho nội dung trò chuyện.

5. `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`
   - Dùng khi build cutscene/staging/camera/trigger.
   - Nếu thoại trong cutscene lệch với dialogue doc, ưu tiên dialogue doc rồi cập nhật cutscene cho khớp.

6. `GDD_GreenAgain_v5_QUEST_FLOW.md`
   - Dùng khi build quest chain, objective text, trigger, next quest, notebook entry.
   - Đây là source chính cho `QuestId`.

7. `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`
   - Dùng khi code trong Roblox Studio.
   - Đây là source chính cho milestone, module, build order, QA.

## 2. Legacy Docs

Các file v4 đã được gom vào `docs/legacy_v4/` để không lẫn với v5. Chỉ dùng để tham khảo lịch sử, không dùng làm nguồn thiết kế hiện tại:

- `legacy_v4/GDD_GreenAgain_v4.md`
- `legacy_v4/GDD_GreenAgain_v4_IMPLEMENTATION_BLUEPRINT.md`
- `legacy_v4/GDD_GreenAgain_Map_v4.md`
- `legacy_v4/GDD_GreenAgain_NPC_Dialogue_v4.md`
- `legacy_v4/GDD_GreenAgain_Flow_Audit_v4.md`
- `legacy_v4/GDD_GreenAgain_Friction_Audit_v4.md`
- `legacy_v4/context.md`

Chỉ đọc v4 khi cần biết lịch sử hoặc so sánh vì sao v5 thay đổi. Không copy lại flow v4 vào v5 nếu chưa được chốt lại.

## 3. Deleted Duplicate Docs

Các doc v5 sau đã được bỏ vì trùng vai trò:

- `GDD_GreenAgain_v5_STORY_FRAMEWORK.md`
  - Nội dung đã được tách vào GDD v5, Story Bible, Quest Flow, Dialogue và Cutscene.

- `GDD_GreenAgain_v5_IMPLEMENTATION_BLUEPRINT.md`
  - Được thay bằng `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`.

- `GDD_GreenAgain_v5_MAP_ALIGNMENT_AUDIT.md`
  - Nội dung map-fit đã được gom vào `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md` và guide này.

## 4. Editing Rules

- Nếu sửa route/map: sửa `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md` trước.
- Nếu sửa cốt truyện/nhân vật: sửa `GDD_GreenAgain_v5_STORY_BIBLE.md`.
- Nếu sửa lời thoại: sửa `GDD_GreenAgain_NPC_DIALOGUE_v5.md`.
- Nếu sửa cutscene staging: sửa `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`.
- Nếu sửa quest ID/objective/trigger: sửa `GDD_GreenAgain_v5_QUEST_FLOW.md`.
- Nếu sửa thứ tự build/code plan: sửa `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`.
- Sau khi sửa một doc chuyên biệt, chỉ cập nhật `GDD_GreenAgain_v5.md` nếu quyết định đó ảnh hưởng tổng quan.

## 5. Anti-Drift Rules

- Không gọi `PicnicArea` là công viên/picnic trong story. Hiển thị là `Sân bóng thôn Ven Sông`.
- Không gọi `Dam_C1/C2/C3` là đập trong story. Hiển thị là `Cống thoát nước cuối xóm`.
- Không dùng scanner làm objective chính.
- Không bắt đầu quest bằng nhặt rác nếu chưa có dialogue/cutscene mở lý do.
- Nếu map thật khác docs, sửa map draft trước rồi mới code.
