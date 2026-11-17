# FCAJ UI ↔ Backend Gap Review

> Đối chiếu bộ Stitch `fcaj-ui/stitch_fcaj_tech_event_platform/` với backend v1.3 tại `fcajdn-page/` (System Design 2026-11-15, API-01..48, controller/service/routes và React SPA hiện có). Đây là phân tích phạm vi, không phải khẳng định lỗi trong backend. Ngày rà soát: 2026-11-17.

## Tóm tắt

Backend đã hỗ trợ tương đối đầy đủ MVP cho khám phá event, đăng nhập, tham dự, nộp/duyệt CFP, quản trị event/user và email notification. Bộ Stitch là prototype trình bày phạm vi rộng hơn ứng dụng thực tế. Các mục cần quyết định trước khi coding FE lại:

1. Leaderboard/karma không có mô hình dữ liệu, quy tắc tính điểm hay API.
2. Check-in QR không có endpoint hoặc trạng thái check-in trong mô hình đăng ký; `registered/cancelled` không thể suy ra `checked-in/absent`.
3. Màn admin overview không có endpoint tổng hợp dashboard.
4. Màn cài đặt admin có thể gộp với quản lý event, nhưng không có API cấu hình hệ thống tổng quát.
5. Màn “Sự kiện của tôi” cần phản ánh đúng participation theo event: attendee đăng ký và speaker submission là hai loại tham gia riêng.
6. Một số badge/trạng thái trong prototype như hết slot, CFP đóng, event hủy có thể được suy ra từ event API; không cần endpoint riêng nếu FE dùng các trường thời hạn/capacity/status có sẵn.

## Bản đồ màn hình → backend

| Stitch screen | Hợp đồng/backend có sẵn | Kết luận / điều chỉnh FE |
|---|---|---|
| 01 Trang chủ / 02 Chi tiết event | `GET /api/v1/events`, `/events/{id}`, `/events/{id}/program` (API-14..16) | Có dữ liệu cho event công khai, lịch, địa điểm, số chỗ, khung CFP, chương trình và trạng thái người xem. API-14 phân trang/lọc theo hợp đồng; thiết kế bộ lọc phải chỉ dùng tham số đã có. |
| 03 Đăng ký attendee | `POST /events/{id}/registrations` (API-17); list/detail/cancel API-18..20 | Có. UI phải xử lý yêu cầu đăng nhập, event không mở/đủ chỗ, đăng ký lặp/đã hủy, hạn hủy; không tự giả lập QR ticket. |
| 04 Đăng ký speaker / CFP | API-21..29; event có cửa sổ CFP; presigned PUT/GET | Có. Duy trì form theo các field backend, quy tắc sửa/rút và upload PDF/PPTX; upload gồm init → PUT trực tiếp storage → complete, không gửi file qua API ứng dụng. |
| 05 Leaderboard | Không có API, bảng điểm, nguồn điểm, xếp hạng hay quyền xem trong API-01..48 | Thiếu backend hoàn toàn. Tạm ẩn route/CTA hoặc để “chưa khả dụng”; muốn làm thật cần chốt semantics, chống gian lận, kỳ tính điểm, quyền riêng tư rồi mới thiết kế backend/API. |
| 06 Admin tổng quan / duyệt CFP | API-38..42 có queue/chi tiết/duyệt/từ chối; API-30 có danh sách event | Duyệt CFP có backend. Tổng quan KPI tổng hợp nhiều miền chưa có API dashboard; dựng bằng nhiều request hiện có hoặc bỏ KPI chưa hỗ trợ. Không đặt tên tổng số như thể đó là dữ liệu authoritative nếu chỉ ước lượng từ trang phân trang. |
| 07 Hồ sơ tài khoản | API-08..10, API-11..12, auth API-01..07 | Có hồ sơ, đổi mật khẩu, notification preferences, logout-all. Avatar/upload ảnh, social links hoặc profile fields chỉ được hiển thị nếu schema/API hiện có trả về; prototype không tạo thêm dữ liệu giả. |
| 08 Sự kiện của tôi | API-18..25, đặc biệt list attendee registrations và speaker submissions riêng | Có cơ sở nhưng không có endpoint “mọi tham gia” hợp nhất. FE có thể tải hai danh sách và hợp nhất ở client, giữ riêng type/status. “Chờ duyệt/từ chối” chỉ áp dụng speaker submission; attendee registration không có trạng thái duyệt. |
| 09 Chi tiết participation | API-19, API-20, API-23..29 | Có thông tin registration và submission, review note, file và program. QR, đã check-in, vắng mặt không có backend. Không hiển thị như trạng thái thật; nhãn “đã xác nhận” phải ánh xạ đúng `registered`, không đồng nghĩa đã check-in. |
| 10 Admin quản lý event | API-30..37: list/create/edit/delete draft/publish/cancel/attendees/notification summary | Có. Phân biệt draft/published/cancelled/completed; không cho sửa/xóa theo affordance nếu backend từ chối do trạng thái. Cấu hình đóng/mở đăng ký và CFP dùng field event hiện hữu. |
| 11 Admin duyệt diễn giả | API-38..42 | Có. Từ chối yêu cầu ghi chú; duyệt có thể xung đột giới hạn `max_speakers`; xử lý 409 và tải file qua URL ký trước. |
| 12 Admin khách tham dự | API-36 | Có danh sách attendee theo event, có email, có phân trang. Không có API check-in, xuất CSV hoặc lọc theo check-in. |
| 13 Điểm đóng góp / karma | Không có API hoặc bảng | Thiếu backend. Tạm bỏ khỏi IA/để feature flag off. Không suy điểm từ số event hoặc submissions nếu chưa có quy tắc sản phẩm. |
| 14 Cài đặt admin | API admin users, event, notification; không có cấu hình hệ thống chung | Tách màn thành các tác vụ có endpoint thật (users/events/email). Nếu prototype muốn setting giao diện cá nhân, lưu client-side chỉ khi thực sự cần; không trình bày nó như cài đặt hệ thống. |
| 15 Chỉnh sửa event | API-31..35 và EventMutationPayload | Có. Kiểm tra location type, timezone/ISO time, capacity, deadline tương quan; validate FE tiện dụng nhưng server là nguồn quyết định. |
| 16 Admin check-in QR | Không có scan/check-in endpoint; schema registration chỉ `registered/cancelled`; không có ticket token/nonce | Thiếu backend hoàn toàn. Không thể làm QR scan thật bằng UI. Cần thiết kế token dùng một lần, check-in atomic/idempotent, quyền staff, audit trail, xử lý QR giả/đã dùng và attendance policy. |
| 17 Full/CFP full/closed/cancelled | Event detail + counters + dates/status trong API-14..15; `speaker_application_window` và `seats_remaining` | Có thể render các trạng thái này từ dữ liệu server. Không tự suy “hết slot diễn giả” từ số proposal; dùng `approved_speaker_count/max_speakers`. Không cho đăng ký attendee vào event cancelled/completed. |
| 18 Về FCAJ | Nội dung tĩnh | Không cần backend. Cần quyết định đây có thuộc scope SPA sản phẩm hay là trang nội dung tĩnh. |

## Các chênh lệch UX / contract cần xử lý

### P0 — Không hiển thị dữ liệu hoặc hành động không tồn tại

- Ẩn hoặc đánh dấu rõ chưa hỗ trợ: leaderboard, karma, QR/check-in, checked-in/absent, admin system settings.
- Gỡ CTA check-in / vé QR khỏi attendee detail cho đến khi API và chính sách tồn tại.
- Không giả lập check-in bằng localStorage, không biến `registered` thành “đã điểm danh”.

### P1 — Ánh xạ trạng thái đúng

- `EventStatus`: `draft | published | cancelled | completed`.
- `RegistrationStatus`: `registered | cancelled`; `effective_status` có thể mô tả event-level hiệu lực, không đại diện check-in.
- `SubmissionStatus`: `pending | approved | rejected | withdrawn`; phân biệt submission với participation type.
- Bản ghi speaker được duyệt có thể hiển thị trong public program; hồ sơ speaker được scope theo event, không phải role speaker toàn cục.
- Event chứa `registered_count`, `seats_remaining`, `speaker_application_window`, `approved_speaker_count`, `max_speakers`; dùng giá trị server, không đếm item ở page hiện tại.

### P1 — Hành vi API và trải nghiệm lỗi

- API cùng origin, prefix `/api/v1`; bearer token; 401 sẽ kết thúc phiên theo client hiện tại.
- Tôn trọng pagination (`page`, `page_size`), không giả định list trả toàn bộ.
- Phân biệt 400 validation, 401/403, 404, 409 conflict, 429/503 kèm Retry-After, lỗi mạng; bảo toàn field errors và request ID khi hiển thị/hỗ trợ.
- Với mutation, khóa nút trong lúc gửi, báo kết quả, refresh dữ liệu authoritative; không tự retry thao tác không idempotent.
- Presigned URL là URL storage ngoài `/api`: PUT cần đúng headers/method trả về; GET URL có hạn, chỉ lấy khi người dùng yêu cầu tải.

## Backend follow-up đề xuất (chỉ khi sản phẩm duyệt)

### Check-in (bắt buộc cho màn 16 và trạng thái check-in)

1. Chốt đối tượng được điểm danh (attendee, speaker, hay cả hai), cửa sổ check-in, quyền staff/admin, policy check-in lặp và vắng mặt.
2. Thiết kế ticket credential khó đoán, không chứa PII; lưu hash hoặc token version/revocation, ràng buộc event + participation.
3. API tạo/hiển thị QR cá nhân và API check-in có thao tác atomic, trả kết quả rõ `checked_in/already_checked_in/invalid/not_eligible`.
4. Lưu `checked_in_at`, actor, event/participation; audit và chống race/replay; chỉ admin/staff được ghi nhận.
5. Thêm migration, policy, rate-limit/proxy policy, tests concurrency/security, admin attendee read view và runbook retention.
6. Chỉ sau đó mới triển khai browser camera permission, scanner, manual fallback và empty/error states.

### Leaderboard / karma (bắt buộc cho screens 05/13)

1. Product xác định điểm nào được cộng/trừ (tham dự thực tế, speaker approved, tình nguyện…), thời điểm ghi nhận, sửa sai, kỳ xếp hạng và opt-out.
2. Quy định tên hiển thị, ẩn danh, quyền truy cập và chống spam/self-dealing.
3. Thiết kế ledger event-based có audit/idempotency, snapshot/query hiệu năng và API phân trang; không chỉ lưu tổng điểm có thể sửa tùy tiện.
4. Thêm migrations, domain service, authz, API/DTO, background aggregation nếu cần, tests và abuse controls.
5. UI chỉ dùng khi contract, semantics và dữ liệu seed đã thống nhất.

### Dashboard và settings

- Tùy nhu cầu, thêm API summary có định nghĩa KPI, quyền admin và cache/consistency rõ; hiện tại có thể tổng hợp event list/notification summary nhưng không thể tạo số liệu global chính xác từ paginated response.
- “Cài đặt” cần tách account preferences (đã có) khỏi system settings (chưa có). Không tạo endpoint settings chung nếu không có setting nghiệp vụ cụ thể.

## Kết luận triển khai

Frontend rebuild có thể hoàn thành MVP bằng API hiện hữu nếu scope loại bỏ/để sau các feature chưa có backend. Phần backend cần thiết kế mới trước khi bật leaderboard/karma và QR check-in. Chi tiết phase FE và quyết định giao diện nằm trong `FE_REBUILD_PLAN.md`, `DESIGN.md`, `UI_TEMPLATE.md`.
