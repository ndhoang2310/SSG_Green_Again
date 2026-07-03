# Green Again V5 Docs Guide

> Dùng file này trước khi đọc hoặc sửa docs. Mục tiêu là tránh đọc nhầm tài liệu cũ, tránh viết trùng nội dung, và giúp nhiều agent làm việc đồng đều trên cùng một hướng V5.

## 1. Current Source Of Truth

V5 là hướng hiện tại của project. Khi build gameplay/story mới, ưu tiên đọc các file này theo thứ tự:

1. `AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`
   - Đọc đầu tiên nếu là agent/Codex chuẩn bị sửa game, Studio, hoặc docs.
   - Chứa luật phối hợp nhiều agent, ownership runtime hiện tại, quy tắc không đè việc nhau, checklist test và handoff.

2. `GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`
   - Document tổng hợp lớn nhất hiện tại.
   - Dùng khi cần một nguồn đầy đủ về game design, build guide, map, dialogue, quest, UI/UX, NPC movement/staging, implementation reference và QA.
   - Đây là tài liệu tốt nhất để agent mới hiểu toàn bộ V5 trước khi implement.

3. `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`
   - Dùng để hiểu MVP hiện đã build gì trong Roblox Studio.
   - Chứa runtime active, UI đã thay, quest flow đã implement, vị trí đã chỉnh, gameplay đã mở rộng, test đã chạy và known console noise.
   - Sau mỗi thay đổi gameplay/code đáng kể, cập nhật file này.

4. `GDD_GreenAgain_v5.md`
   - Dùng khi cần hiểu tổng quan game v5, pillars, main route, chapter overview và ending.
   - Đây là cửa vào chính.

5. `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
   - Dùng khi cần hiểu map hiện tại theo cụm địa điểm.
   - Source chính cho route: Nhà văn hóa -> Tạp hóa -> Sân bóng -> Ông Sáu/bờ sông -> Cống -> Nhà văn hóa.
   - Dùng để kiểm tra tên kỹ thuật cũ như `PicnicArea`, `Dam_C1/C2/C3`, `Portal1Destination` nên hiển thị thế nào trong story.

6. `GDD_GreenAgain_v5_STORY_BIBLE.md`
   - Dùng khi viết/cải thiện story, tone, arc nhân vật, theme.
   - Không dùng để lấy quest IDs hoặc implementation details.

7. `GDD_GreenAgain_NPC_DIALOGUE_v5.md`
   - Dùng khi viết thoại NPC, dialogue state, hội thoại chính/phụ.
   - Đây là source chính cho nội dung trò chuyện.

8. `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`
   - Dùng khi build cutscene/staging/camera/trigger.
   - Nếu thoại trong cutscene lệch với dialogue doc, ưu tiên dialogue doc rồi cập nhật cutscene cho khớp.

9. `GDD_GreenAgain_v5_QUEST_FLOW.md`
   - Dùng khi build quest chain, objective text, trigger, next quest, notebook entry.
   - Đây là source chính cho `QuestId`.

10. `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`
   - Dùng khi code trong Roblox Studio.
   - Đây là source chính cho milestone, module, build order, QA.

## 2. Current Active Implementation

MVP hiện tại đang nằm chủ yếu trong Roblox Studio, không phải một hệ module hoàn chỉnh trong repo.

Active runtime:

- Server: `game.ServerScriptService.GreenAgainProject.Runtime_To_Add.StoryRuntimeMVP`
- Client: `game.StarterPlayer.StarterPlayerScripts.StoryClientMVP`
- Sprint: `game.StarterPlayer.StarterCharacterScripts.SprintStaminaScript`
- Team-owned waiting screen / main menu: `game.StarterGui.MainMenuGui.MainMenuController`

Không tạo lại các hệ cũ:

- `StarterGui.GreenAgainHUD_V5`
- `StarterPlayer.StarterPlayerScripts.GreenAgainObjectiveClient`
- `ServerScriptService.GreenAgainProject.Runtime_To_Add.MapWiringBootstrap`
- Text UI cũ: `Đang nối map Green Again V5...`

Lưu ý phối hợp:

- `MainMenuGui` / `MainMenuController` đang là phần màn hình chờ do thành viên khác trong nhóm làm.
- Agent khác không tự ý thay thế hoặc refactor màn hình chờ nếu chưa được giao.
- Story HUD vẫn nằm trong `StoryClientMVP`; không trộn logic menu vào story HUD.

## 3. Current V5 Document Inventory

Các file V5 hiện có trong `docs/`:

- `AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`
  - Luật làm việc chung cho nhiều agent.

- `GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`
  - Document tổng hợp lớn, dùng như GDD + build guide + implementation reference.

- `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`
  - Tóm tắt trạng thái build thật hiện tại trong Roblox Studio.

- `GDD_GreenAgain_v5.md`
  - GDD tổng quan V5.

- `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
  - Map draft, route, mapping tên kỹ thuật sang tên story.

- `GDD_GreenAgain_v5_STORY_BIBLE.md`
  - Tone, theme, nhân vật, arc cảm xúc.

- `GDD_GreenAgain_NPC_DIALOGUE_v5.md`
  - Dialogue NPC, ambient lines, state dialogue.

- `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`
  - Cutscene script và staging.

- `GDD_GreenAgain_v5_QUEST_FLOW.md`
  - Quest flow, quest id, objective, trigger.

- `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`
  - Plan implement chi tiết theo milestone.

## 4. Legacy Docs

Các file v4 đã được gom vào `docs/legacy_v4/` để không lẫn với v5. Chỉ dùng để tham khảo lịch sử, không dùng làm nguồn thiết kế hiện tại:

- `legacy_v4/GDD_GreenAgain_v4.md`
- `legacy_v4/GDD_GreenAgain_v4_IMPLEMENTATION_BLUEPRINT.md`
- `legacy_v4/GDD_GreenAgain_Map_v4.md`
- `legacy_v4/GDD_GreenAgain_NPC_Dialogue_v4.md`
- `legacy_v4/GDD_GreenAgain_Flow_Audit_v4.md`
- `legacy_v4/GDD_GreenAgain_Friction_Audit_v4.md`
- `legacy_v4/context.md`

Chỉ đọc v4 khi cần biết lịch sử hoặc so sánh vì sao v5 thay đổi. Không copy lại flow v4 vào v5 nếu chưa được chốt lại.

## 5. Deleted Duplicate Docs

Các doc v5 sau đã được bỏ vì trùng vai trò:

- `GDD_GreenAgain_v5_STORY_FRAMEWORK.md`
  - Nội dung đã được tách vào GDD v5, Story Bible, Quest Flow, Dialogue và Cutscene.

- `GDD_GreenAgain_v5_IMPLEMENTATION_BLUEPRINT.md`
  - Được thay bằng `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`.

- `GDD_GreenAgain_v5_MAP_ALIGNMENT_AUDIT.md`
  - Nội dung map-fit đã được gom vào `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md` và guide này.

## 6. Editing Rules

- Nếu chuẩn bị sửa game/code/Studio: đọc `AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md` trước.
- Nếu cần hiểu toàn bộ game và build guide: đọc `GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`.
- Nếu cần biết Studio hiện đã build gì: đọc `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`.
- Nếu sửa runtime hiện tại: ưu tiên cập nhật trong `StoryRuntimeMVP` hoặc `StoryClientMVP`, không tạo script song song nếu không cần.
- Nếu thay đổi behavior đã implement: cập nhật `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`.
- Nếu thay đổi luật phối hợp agent: cập nhật `AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`.

- Nếu sửa route/map: sửa `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md` trước.
- Nếu sửa cốt truyện/nhân vật: sửa `GDD_GreenAgain_v5_STORY_BIBLE.md`.
- Nếu sửa lời thoại: sửa `GDD_GreenAgain_NPC_DIALOGUE_v5.md`.
- Nếu sửa cutscene staging: sửa `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`.
- Nếu sửa quest ID/objective/trigger: sửa `GDD_GreenAgain_v5_QUEST_FLOW.md`.
- Nếu sửa thứ tự build/code plan: sửa `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`.
- Sau khi sửa một doc chuyên biệt, chỉ cập nhật `GDD_GreenAgain_v5.md` nếu quyết định đó ảnh hưởng tổng quan.

## 7. Anti-Drift Rules

- Không gọi `PicnicArea` là công viên/picnic trong story. Hiển thị là `Sân bóng thôn Ven Sông`.
- Không gọi `Dam_C1/C2/C3` là đập trong story. Hiển thị là `Cống thoát nước cuối xóm`.
- Không dùng scanner làm objective chính.
- Không bắt đầu quest bằng nhặt rác nếu chưa có dialogue/cutscene mở lý do.
- Nếu map thật khác docs, sửa map draft trước rồi mới code.
- Không reintroduce UI cũ, marker nhiều điểm, hoặc marker có distance.
- Không tạo placeholder sân bóng/cống vì map hiện đã có object thật.
