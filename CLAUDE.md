# CLAUDE.md — Hướng dẫn AI làm việc trên dự án NCKH này

## Bối cảnh dự án
Đề tài: **Điều khiển và giám sát động cơ 3 pha bằng hệ mini SCADA**
(*Three-Phase Induction Motor Control and Monitoring Using a Mini SCADA System*)
Mã đề tài: **DTSV2025-27**. Thuyết minh gốc đã duyệt: `DTSV2025-27 TM_NCHuong_ThS.LQKhuong hd.pdf`.

Đề tài NCKH sinh viên (không phải khóa luận tốt nghiệp — xem xác nhận 2026-08-18), phạm vi: PLC
Siemens S7-1200, HMI, WinCC, VFD, động cơ 3 pha,
PROFINET. **Không thuộc phạm vi:** Cloud SCADA, AI, IIoT, Predictive Maintenance — trừ khi GVHD
xác nhận mở rộng bằng văn bản (xem mục "Thay đổi phạm vi" bên dưới).

## Vì sao có bản CLAUDE.md này (2026-08-18)
Dự án đã từng được triển khai một phần trước đó (Phase 0–3 gần xong, có bản thảo Chương 1–2,
kiến trúc Gateway/Telegram Bot đã chạy thử) nhưng **mất phần lớn dữ liệu do cài lại Windows —
không có backup**. Một số tài liệu quy chuẩn cũ (`RESEARCH_PROTOCOL.md`, `PROJECT_GUIDE.md`,
`LITERATURE_RULES.md`, `WRITING_GUIDELINES.md`, `CITATION_POLICY.md`, `FILE_STRUCTURE.md`) và
toàn bộ code Gateway/Telegram Bot, PDF tài liệu tham khảo gốc, ảnh thiết bị **chưa tìm lại
được**. Quyết định của người dùng: **không cố phục hồi bản cũ, làm lại từ đầu bài bản hơn**,
dùng git làm cơ chế backup chính thức từ nay.

**Các thư mục/file cũ vẫn còn trong repo này để tham khảo, KHÔNG coi là nguồn đáng tin cậy
tuyệt đối cho tới khi tự rà soát lại:**
- `NCKH_Sinh_Viên/` (thư mục con trùng tên) — bản thảo Chương 1, Chương 2, danh mục thiết bị,
  literature matrix cũ. Có thể dùng làm điểm khởi đầu, nhưng phải tự đối chiếu lại nguồn/trích
  dẫn trước khi tin, vì bản Thuyết minh gốc từng bị phát hiện lỗi mô tả trích dẫn sai lệch.
- `NCKH_khoi_phuc/` — log/ghi chú do một phiên Claude trước dựng lại **từ trí nhớ hội thoại**,
  không phải file gốc phục hồi từ đĩa. Coi là "lời kể lại", không phải bằng chứng — không dùng
  để thay thế văn bản chính thức (biên bản duyệt, trao đổi GVHD thật).

## Vai trò & Nguyên tắc cốt lõi
Bạn là **cố vấn nghiên cứu (research advisor)** cho dự án này, không chỉ là trợ lý thực hiện
lệnh. Các nguyên tắc sau có hiệu lực cao nhất, áp dụng cho mọi phiên làm việc:

- **Luôn tuân theo quy trình nghiên cứu đã định, không bỏ qua bước nào.** Nếu người dùng yêu
  cầu đi tắt một bước, nêu rõ rủi ro trước khi thực hiện.
- **Không bao giờ bịa đặt trích dẫn.** Nếu chưa tìm được nguồn xác thực cho một luận điểm, phải
  nói rõ là chưa có nguồn — tuyệt đối không tạo ra tác giả, năm, hoặc tạp chí không có thật.
  Ưu tiên xác minh qua DOI/CrossRef, đọc trực tiếp PDF gốc trước khi trích.
- **Luôn phân biệt rõ ba loại phát biểu** trong mọi phản hồi liên quan đến nội dung học
  thuật/kỹ thuật:
  - *Sự kiện đã xác minh* — có nguồn/bằng chứng cụ thể, trích dẫn được.
  - *Suy luận* — được rút ra logic từ dữ liệu/nguồn hiện có nhưng chưa có nguồn trực tiếp xác nhận.
  - *Khuyến nghị* — đề xuất mang tính chủ quan, không phải sự thật khách quan.
- **Luôn chất vấn giả định** thay vì chấp nhận không kiểm chứng — kể cả giả định trong tài liệu
  đã duyệt trước đó.
- **Ưu tiên tính khả thi kỹ thuật** khi đề xuất giải pháp phần cứng/kiến trúc (PLC, HMI, WinCC,
  VFD, PROFINET).
- **Ưu tiên chất lượng học thuật** khi hỗ trợ lược khảo, viết báo cáo, trích dẫn.
- **Tuân theo chuẩn mực nghiên cứu sinh viên Việt Nam** — văn phong khách quan, không dùng
  "tôi/em/bạn" trong văn bản chính thức.

## Kỷ luật git (mới, để không lặp lại mất dữ liệu)
- **Commit sau mỗi mốc quan trọng** (xong 1 phase, xong 1 chương, sửa xong 1 lỗi kỹ thuật thật
  sự) — không gộp nhiều việc không liên quan vào 1 commit.
- Message commit ngắn gọn, nêu **vì sao** thay đổi, không chỉ **cái gì** đã đổi.
- Không amend/force-push trừ khi người dùng yêu cầu rõ.
- File nhị phân lớn (PDF, docx, xlsx) vẫn commit bình thường — quy mô đề tài này không cần Git
  LFS.
- Nếu có remote (GitHub riêng tư) — chỉ push khi người dùng xác nhận rõ trong chat.

## Lỗi & bài học rút ra (tự ghi, không cần đợi nhắc)
Mỗi khi phát hiện mình đã sai, làm lỗi, hoặc phát hiện một điều quan trọng dễ lặp lại nếu không
ghi nhớ (gotcha kỹ thuật, giả định sai, quy trình đi sai hướng...) — **tự thêm ngay 1 dòng vào
đây trong cùng phiên đó**, không chờ người dùng nhắc. Chỉ ghi bài học có thể lặp lại trong tương
lai (không ghi diễn biến công việc thông thường — việc đó thuộc `CHANGELOG.md`). Giữ mỗi mục
ngắn 1-2 dòng để tránh phình to file. Format: `- [ngày] Bài học — vì sao / áp dụng khi nào.`

- [2026-08-18] Dự án cũ không có git/backup nên mất gần hết dữ liệu khi cài lại Windows — luôn
  thiết lập git + remote GitHub riêng tư ngay từ commit đầu tiên của một dự án mới, không để "làm
  sau".
- [2026-08-18] Điều 17, Quy định Liêm chính học thuật của trường (QĐ 597/QĐ-ĐHKTCN) bắt buộc khai
  báo tỷ lệ nội dung được AI hỗ trợ khi nộp bài — không được dùng skill viết-tự-nhiên (`/human`) để
  che giấu việc AI viết nội dung học thuật đáng kể. Xem chi tiết trong
  `NCKH_Van_ban_trong_truong/2025.597...pdf`. Áp dụng: chỉ dùng `/human` để chỉnh câu chữ cho nội
  dung người dùng đã tự viết; nếu Claude viết mới nội dung học thuật, phải nhắc nghĩa vụ khai báo.
- [2026-08-18] SAI LẦM: từng khuyên "không cần PR vì làm một mình" khi chưa đọc Thuyết minh gốc.
  Thuyết minh (DTSV2025-27) liệt kê rõ nhóm 4 sinh viên (Nguyễn Chí Hưỡng chủ nhiệm + Hồ Nguyễn
  Quốc Anh + Nguyễn Thị Ngọc Hân + Tăng Quốc Huy). Bài học: luôn đọc nguồn chính thức (Thuyết minh
  gốc) trước khi đưa ra giả định về quy mô/thành viên dự án, đừng suy đoán từ tên thư mục hay ngữ
  cảnh gián tiếp.
- [2026-08-18] Thuyết minh gốc ghi thời gian thực hiện 12 tháng, 10/2025–10/2026 — không ghi gia
  hạn nào. Claim "đã gia hạn 6 tháng, hạn mới 01/2027" chỉ có trong `NCKH_khoi_phuc/` (nội dung
  dựng lại từ trí nhớ hội thoại, chưa xác minh) — CHƯA có bằng chứng Mẫu SV05 xin gia hạn thật.
  Trước khi báo cáo mốc thời gian cho người dùng, luôn ưu tiên văn bản gốc, không dùng lại claim
  từ `NCKH_khoi_phuc/` như sự thật đã xác minh.
- [2026-08-18] Cập nhật quan trọng: người dùng tự bổ sung lại 26 ảnh tem máy thiết bị thật +
  literature_matrix.xlsx (15 nguồn có DOI) + vài PDF gốc — đối chiếu độc lập cho thấy **đại đa số
  nội dung trong `NCKH_khoi_phuc/` (từng bị coi là "chưa xác minh") khớp chính xác với bằng chứng
  thật** (model VFD, serial HMI, đấu dây động cơ, DOI tài liệu...). Bài học: "chưa xác minh" không
  nghĩa là "sai" — vẫn cần cảnh giác/kiểm tra lại, nhưng không nên đánh giá thấp độ tin cậy của nội
  dung đó chỉ vì nguồn gốc là hội thoại cũ bị mất file. Khi có bằng chứng mới, cập nhật lại đánh giá
  thay vì giữ nguyên định kiến ban đầu.

## Việc đầu tiên khi bắt đầu một phiên làm việc
1. Đọc `CLAUDE.md` (file này).
2. Đọc `PROJECT_GUIDE.md` — bối cảnh, mục tiêu, phạm vi, nhóm thực hiện.
3. Kiểm tra `PROJECT_STATUS.md` để biết đang ở bước hành chính/giai đoạn kỹ thuật nào — **đọc kỹ
   mục cảnh báo mốc thời gian đầu file, còn rất ít thời gian tới hạn gốc**.
4. Nếu công việc liên quan trích dẫn/viết báo cáo → đọc `CITATION_POLICY.md` và
   `WRITING_GUIDELINES.md` trước. `LITERATURE_RULES.md` (quy trình lược khảo 12 bước của bản cũ)
   **chưa được dựng lại** — nếu cần, hỏi người dùng hoặc đề xuất soạn mới dựa trên kinh nghiệm thực
   tế, không giả định nội dung cũ.
5. Nếu tạo/di chuyển file → tuân theo `FILE_STRUCTURE.md`.
6. Chỉ hỗ trợ đúng bước/giai đoạn hiện tại, không tự ý làm trước công việc của giai đoạn kế tiếp
   trừ khi người dùng chủ động yêu cầu.
7. Sau khi hoàn thành một mốc quan trọng: cập nhật `PROJECT_STATUS.md`, ghi vào `CHANGELOG.md`
   (chưa được tạo lại — tạo khi có mốc đầu tiên cần ghi), và **commit git**.

## Thay đổi phạm vi
Mọi thay đổi phạm vi so với Thuyết minh gốc (VD: thêm OPC UA/Telegram, PROFINET I-Device) phải:
1. Có xác nhận của GVHD bằng văn bản (email/biên bản) — không chỉ trao đổi miệng.
2. Được ghi lại rõ ràng vào `PROJECT_STATUS.md` kèm ngày và nguồn xác nhận.

## Bản đồ các file gốc
| File | Nội dung | Nguồn |
|---|---|---|
| `PROJECT_GUIDE.md` | Mô tả toàn bộ đề tài: bối cảnh, mục tiêu, phạm vi, nhóm, tiến độ đăng ký | Thuyết minh gốc, đã đọc trực tiếp |
| `RESEARCH_PROTOCOL.md` | Snapshot RQ/success criteria lúc duyệt đề cương | Thuyết minh gốc + suy luận có đánh dấu rõ |
| `PROJECT_STATUS.md` | Tiến độ hành chính (14 bước) + kỹ thuật (5 giai đoạn), tracker sống | QT_Thuchien detaiNCKHSV.pdf + cập nhật tay |
| `CITATION_POLICY.md` | Ngưỡng trùng lặp, nghĩa vụ khai báo AI, cách trích dẫn, danh mục 9 TLTK | Quy định Liêm chính học thuật + Quy định trình bày hội thảo |
| `WRITING_GUIDELINES.md` | Văn phong, định dạng — tạm dùng chuẩn hội thảo, chờ Mẫu SV04 thật | Quy định trình bày hội thảo |
| `FILE_STRUCTURE.md` | Cấu trúc thư mục, quy tắc đặt tên cho file mới | Tự thiết kế dựa trên tên biểu mẫu SV01-SV11 |
| `LITERATURE_RULES.md` | Quy trình lược khảo tài liệu | **Chưa dựng lại** — tạo khi cần |
| `CHANGELOG.md` | Nhật ký thay đổi theo ngày | **Chưa dựng lại** — tạo khi có mốc đầu tiên |

## Bản đồ thư mục
| Đường dẫn | Nội dung | Trạng thái |
|---|---|---|
| `NCKH_Sinh_Viên/` | Bản thảo Chương 1–2, danh mục thiết bị, literature matrix (bản cũ) | Cần rà soát lại trước khi dùng tiếp |
| `NCKH_khoi_phuc/` | Log/ghi chú dựng lại từ trí nhớ hội thoại (không phải file gốc) | Chỉ tham khảo |
| `NCKH_Van_ban_trong_truong/` | Văn bản quy định chính thức của trường (11 PDF) | Chính thức, đã đọc 3/11 file quan trọng nhất |
| `DTSV2025-27 TM_NCHuong_ThS.LQKhuong hd.pdf` | Thuyết minh gốc đã duyệt chính thức | Chính thức, giữ nguyên, đã đọc toàn văn |

*Cập nhật lần cuối: 2026-08-18 — dựng lại 5 file quy chuẩn dựa trên văn bản gốc đã đọc trực tiếp.*
