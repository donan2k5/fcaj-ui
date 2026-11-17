# FCAJ Event Platform — Frontend Design System

> Design contract cho việc viết lại frontend dựa trên prototype Stitch và backend v1.3. Nguồn hiện trạng backend: `fcajdn-page/docs/SYSTEM_DESIGN.md`; nguồn palette tham khảo: `cloud_enterprise_events/DESIGN.md` và `fcajdn-page/docs/UI_DESIGN/`. Bản này thống nhất một ngôn ngữ hình ảnh riêng cho sản phẩm FCAJ.

## 1. Sản phẩm và nguyên tắc

FCAJ là nền tảng cộng đồng sự kiện công nghệ Đà Nẵng. Giao diện cần có chất enterprise đáng tin cậy nhưng vẫn thân thiện với cộng đồng địa phương. Dùng nền sáng, cấu trúc rõ, typography dễ đọc tiếng Việt, nhấn xanh navy và xanh dương cho hành động. Màu trạng thái chỉ dùng để truyền nghĩa.

- Nội dung và trạng thái do API cung cấp là nguồn sự thật.
- Tập trung vào event, lịch trình, tham gia và đóng góp; không giả vờ có leaderboard/check-in khi backend chưa có.
- Mỗi trang có một hành động chính; hành động rủi ro có xác nhận và phản hồi kết quả.
- Responsive từ mobile trước: các flow đăng nhập, đăng ký event, CFP, account phải dùng được bằng một tay.
- Accessible: semantic HTML, label rõ, keyboard focus, contrast WCAG AA, không dùng màu làm tín hiệu duy nhất.

## 2. Tone of voice

**Tính cách:** kỹ thuật, cởi mở, chính xác, không khoa trương.

**Viết:** tiếng Việt tự nhiên, câu ngắn, động từ rõ. Dùng “Sự kiện”, “Người tham dự”, “Đơn trình bày”, “Chương trình”, “Quản trị”. Giữ thuật ngữ API trong code, không trộn “speaker” vào UI trừ nơi người dùng quen gọi “diễn giả”.

- CTA: “Đăng ký tham dự”, “Gửi đề xuất”, “Lưu thay đổi”, “Xuất bản sự kiện”.
- Trạng thái giải thích nguyên nhân: “Đã hết chỗ”, “Đã đóng nhận đề xuất”, “Sự kiện đã bị hủy”.
- Lỗi nêu hành động tiếp theo; tránh mã lỗi thô. Ví dụ: “Phiên đăng nhập đã hết hạn. Đăng nhập lại để tiếp tục.”
- Không tuyên bố “Vé đã check-in” nếu backend chỉ xác nhận đăng ký.

## 3. Màu sắc

| Token | Giá trị | Dùng cho |
|---|---|---|
| `--color-canvas` | `#F5F7FA` | nền toàn trang |
| `--color-surface` | `#FFFFFF` | panel, card, modal |
| `--color-surface-subtle` | `#EDF2F7` | input, section nhẹ, hover |
| `--color-ink` | `#16202C` | heading/body chính |
| `--color-ink-muted` | `#566477` | metadata, mô tả phụ |
| `--color-border` | `#D9E0E8` | viền và divider |
| `--color-primary` | `#162A43` | header, primary button, nav active |
| `--color-primary-hover` | `#203B5C` | hover/focus action |
| `--color-accent` | `#176FC1` | link, focus, selected |
| `--color-accent-soft` | `#E7F1FC` | selected background, info badge |
| `--color-success` | `#176B48` | thành công/đã duyệt |
| `--color-success-soft` | `#E7F5EE` | nền success |
| `--color-warning` | `#8A5A00` | sắp đóng/chờ xử lý |
| `--color-warning-soft` | `#FFF4D8` | nền warning |
| `--color-danger` | `#B4232D` | lỗi, hủy, destructive |
| `--color-danger-soft` | `#FDEBEC` | nền danger |

Primary navy tiếp nối prototype; action blue kế thừa cloud-enterprise reference. Status colors không được dùng làm thương hiệu hoặc decoration. Đảm bảo contrast trên từng cặp thực tế trước khi release.

## 4. Typography

- Font stack: `Inter, "Segoe UI", system-ui, sans-serif`; nếu bundled font được chọn, tự host để bảo đảm hiển thị và privacy.
- Body 16px / line-height 1.5 trên nội dung dài; UI dense có thể dùng 14px nhưng không hạ cỡ nội dung quan trọng.
- Display 40/48px desktop, 30/38px mobile; H1 trang 30/38px desktop, 26/34px mobile; H2 22/30px; H3 18/26px.
- Weight 400 body, 500 control, 600 heading/label, 700 chỉ cho display.
- Ngày giờ luôn format theo timezone của event (hiển thị timezone khi cần), không format thời gian API bằng timezone thiết bị một cách âm thầm.

## 5. Layout, spacing, shape

- Grid 12 cột desktop; max content width 1200px; gutter 24px. Tablet 16px; mobile 16px lề, 12–16px gap.
- Spacing base 4px; nhịp thường dùng 4, 8, 12, 16, 24, 32, 48, 64px.
- Header public 64–72px desktop; mobile 56px và menu dễ chạm.
- Admin dùng sidebar 240px desktop, drawer trên mobile; nội dung data table có overflow có kiểm soát.
- Card radius 12px, modal 16px, input/button 8px; tránh pill cho mọi thành phần. Shadow nhẹ, ưu tiên border và phân cấp surface.
- Hit target tối thiểu 44×44px; focus ring 2px accent với offset rõ.

## 6. Component contracts

### Navigation
Public nav: logo FCAJ, Sự kiện, Về FCAJ, đăng nhập/avatar. Admin nav: Tổng quan (chỉ khi KPI có dữ liệu), Sự kiện, Duyệt đề xuất, Người dùng, Email. Không có mục “Karma”/“Check-in” cho đến khi backend hỗ trợ.

### Event card/detail
Card: title, date/time + timezone, location mode, venue/city, trạng thái và CTA. Detail: description, location/online mode, deadline/capacity, program, approved speaker, participation panel. Không lộ private online URL nếu API viewer không cho phép.

### Status badge
Tạo component typed theo enum backend; map label + tone rõ. Unknown status có fallback trung tính và log telemetry, không crash.

### Forms
Label persistent, helper/error gần field, server validation hiển thị đúng field, required marker có giải thích. Submit disabled khi đang gửi; giữ dữ liệu người dùng khi lỗi; confirm trước cancel/withdraw/delete/publish nếu hành động khó đảo ngược.

### Tables/lists
Loading skeleton, empty state có CTA, error retry, pagination server-driven, filter state nằm trong URL khi có ích. Không tính global totals bằng số dòng hiện tại.

### Feedback
Inline field error, page alert, toast cho kết quả ngắn; lỗi 409 giải thích conflict cụ thể; 429/503 hiển thị thời gian chờ nếu Retry-After có; network failure có nút thử lại an toàn.

### Dialogs
Modal cho xác nhận nhỏ và form ngắn; trang riêng cho form event/CFP dài. Focus trap, Escape, trả focus về trigger.

## 7. Responsive behavior

- <640px: single column; CTA chính full width trong form/mobile sheet; filter thành disclosure; table chuyển thành list item hoặc scroll ngang có nhãn.
- 640–1023px: 2 cột event cards; admin nav drawer; chi tiết event có sidebar xếp xuống cuối.
- ≥1024px: content max-width; event grid tối đa 3 cột; admin sidebar persistent.
- Không để iframe mock/mobile prototype trong product app. Không phụ thuộc hover cho hành động.

## 8. Motion and imagery

Motion ngắn 120–180ms cho hover/expand; tôn trọng `prefers-reduced-motion`. Dùng ảnh banner chỉ khi event có asset thật và có crop/alt text; fallback graphic trung tính. Không dùng ảnh stock ngẫu nhiên làm dữ liệu giả.

## 9. Data and privacy display

- Hiển thị chỉ trường DTO được phép theo viewer/role; không đưa notes nội bộ hoặc email người khác vào public view.
- Presigned URL không lưu lâu trong state/local storage; chỉ request khi cần và coi như credential tạm thời.
- Không log token, email nhạy cảm hoặc payload file. QR credential (nếu có sau này) tuyệt đối không nhúng PII.

## 10. Definition of done cho UI

Mỗi flow có loading/empty/error/success, responsive behavior, keyboard operation và mapping trạng thái từ backend. Các mutation xử lý conflict và refresh authoritative data. Không có link chết, dữ liệu bịa, trạng thái không thể biểu đạt bởi backend, hoặc màu trạng thái thiếu nhãn chữ.
