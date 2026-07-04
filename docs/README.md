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

4. `GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`
   - Dùng để hiểu toàn bộ cấu trúc code hiện có trong Roblox Studio.
   - Chứa inventory script active, RemoteEvents, Attribute contract, runtime folders, server/client ownership và quy trình thêm quest/gameplay.
   - Đọc file này trước khi tạo script mới hoặc sửa `StoryRuntimeMVP` / `StoryClientMVP`.

5. `GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md`
   - Dùng khi cần hiểu hoặc sử dụng các model rác trong `game.Workspace.Trash`.
   - Chứa cấu trúc thư viện rác, categories, attributes template, cách clone sang runtime, và quy tắc không bật interaction trên source asset.
   - Đọc file này trước khi thay runtime trash visuals, sorting props, hoặc thêm model rác mới.

6. `GDD_GreenAgain_v5.md`
   - Dùng khi cần hiểu tổng quan game v5, pillars, main route, chapter overview và ending.
   - Đây là cửa vào chính.

7. `GDD_GreenAgain_v5_CURRENT_MAP_DRAFT.md`
   - Dùng khi cần hiểu map hiện tại theo cụm địa điểm.
   - Source chính cho route: Nhà văn hóa -> Tạp hóa -> Sân bóng -> Ông Sáu/bờ sông -> Cống -> Nhà văn hóa.
   - Dùng để kiểm tra tên kỹ thuật cũ như `PicnicArea`, `Dam_C1/C2/C3`, `Portal1Destination` nên hiển thị thế nào trong story.

8. `GDD_GreenAgain_v5_STORY_BIBLE.md`
   - Dùng khi viết/cải thiện story, tone, arc nhân vật, theme.
   - Không dùng để lấy quest IDs hoặc implementation details.

9. `GDD_GreenAgain_NPC_DIALOGUE_v5.md`
   - Dùng khi viết thoại NPC, dialogue state, hội thoại chính/phụ.
   - Đây là source chính cho nội dung trò chuyện.

10. `GDD_GreenAgain_v5_CUTSCENE_SCRIPT.md`
   - Dùng khi build cutscene/staging/camera/trigger.
   - Nếu thoại trong cutscene lệch với dialogue doc, ưu tiên dialogue doc rồi cập nhật cutscene cho khớp.

11. `GDD_GreenAgain_v5_QUEST_FLOW.md`
   - Dùng khi build quest chain, objective text, trigger, next quest, notebook entry.
   - Đây là source chính cho `QuestId`.

12. `GDD_GreenAgain_v5_IMPLEMENTATION_PLAN.md`
   - Dùng khi code trong Roblox Studio.
   - Đây là source chính cho milestone, module, build order, QA.

## 2. Current Active Implementation

MVP hiện tại đang nằm chủ yếu trong Roblox Studio, không phải một hệ module hoàn chỉnh trong repo.

Active runtime:

- Startup loader: `game.ReplicatedFirst.GreenAgainStartupLoader`
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
- `GreenAgainStartupLoader` là lớp loading sớm ở `ReplicatedFirst`; giữ riêng khỏi `MainMenuController` để chờ menu render xong trước khi fade.
- Story HUD vẫn nằm trong `StoryClientMVP`; không trộn logic menu vào story HUD.
- Performance hiện tại phụ thuộc vào việc `StoryClientMVP` cache interactables; không thêm lại scan toàn `workspace:GetDescendants()` trong `Heartbeat`.
- Trash asset library hiện nằm ở `game.Workspace.Trash`; đây là source template/scene dressing, không phải runtime quest folder. Runtime props vẫn spawn dưới `Workspace.GreenAgainV5_StoryRuntime`.
- Sorting quest hiện dùng mini game kéo-thả trong `StoryClientMVP`; item kéo-thả là visual card render model rác 3D từ `Workspace.Trash` bằng `ViewportFrame`, server `StoryRuntimeMVP` validate từng item qua `OnSortingMinigameSubmit`. Không quay lại kiểu auto-sort khi bấm trực tiếp từng thùng.

## 3. Current V5 Document Inventory

Các file V5 hiện có trong `docs/`:

- `AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`
  - Luật làm việc chung cho nhiều agent.

- `GREEN_AGAIN_V5_FULL_GAME_DOCUMENT_AND_BUILD_GUIDE.md`
  - Document tổng hợp lớn, dùng như GDD + build guide + implementation reference.

- `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`
  - Tóm tắt trạng thái build thật hiện tại trong Roblox Studio.

- `GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`
  - Cấu trúc code Roblox V5: active scripts, RemoteEvents, Attributes, runtime folders, server/client ownership và quy trình thêm code.

- `GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md`
  - Cấu trúc `Workspace.Trash`: asset categories, template attributes, runtime clone rules, disabled imported scripts và checklist thêm model rác.

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
- Nếu chuẩn bị tạo/sửa code trong Roblox: đọc `GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md` và viết plan logic/cấu trúc trước khi code.
- Nếu sửa runtime hiện tại: ưu tiên cập nhật trong `StoryRuntimeMVP` hoặc `StoryClientMVP`, không tạo script song song nếu không cần.
- Nếu thay đổi behavior đã implement: cập nhật `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`.
- Nếu thay đổi luật phối hợp agent: cập nhật `AGENT_COLLABORATION_RULES_GREEN_AGAIN_V5.md`.
- Nếu thay đổi interaction scan, prompt UI, movement/menu, sprint hoặc performance loop: cập nhật cả `GREEN_AGAIN_V5_ROBLOX_CODE_STRUCTURE.md`.
- Nếu thêm/sửa model rác trong `Workspace.Trash`: cập nhật `GREEN_AGAIN_V5_TRASH_ASSET_LIBRARY.md`; nếu runtime sử dụng asset đó thay đổi behavior, cập nhật thêm `GREEN_AGAIN_V5_MVP_IMPLEMENTATION_SUMMARY.md`.

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
- Không bật `Interactable=true` trực tiếp trên source template trong `Workspace.Trash`; clone sang runtime folder rồi mới enable theo quest.
- Không dùng `workspace:GetDescendants()` hoặc scan lớn trong `Heartbeat`/`RenderStepped` nếu chưa cache/throttle rõ ràng.
- Không set UI text/visibility hoặc `Humanoid.WalkSpeed` mỗi frame nếu giá trị không đổi.
