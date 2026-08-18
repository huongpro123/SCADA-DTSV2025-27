# PROJECT STATUS

*Nguồn theo dõi tiến độ "sống" — cập nhật mỗi khi hoàn thành một mốc, kèm commit git. Khác với
`RESEARCH_PROTOCOL.md` (snapshot cố định lúc duyệt đề cương), file này phản ánh thực tế hiện tại.*

## ⚠️ Cảnh báo mốc thời gian (đọc trước khi lập kế hoạch)
Thuyết minh gốc ghi thời gian thực hiện: **10/2025 – 10/2026** (12 tháng), không ghi gia hạn. Hôm
nay là **2026-08-18** — còn khoảng **1,5 tháng** tới hạn gốc nếu chưa có gia hạn chính thức (Mẫu
SV05). Cần xác nhận ngay: đã nộp/duyệt gia hạn chưa? Nếu chưa, đây là rủi ro tiến độ nghiêm trọng
cần ưu tiên xử lý hành chính song song với kỹ thuật.

## Quy trình hành chính (theo `QT_ Thuchien detaiNCKHSV.pdf` — quy trình thật của trường)

| Bước | Nội dung | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Thông báo đăng ký | ✅ Đã xác nhận | |
| 2 | Xây dựng thuyết minh và kinh phí (Mẫu SV01, SV02) | ✅ Đã xác nhận | |
| 3 | Duyệt đề xuất cấp khoa | ✅ Đã xác nhận | |
| 4 | Khoa gửi danh sách về Phòng | ✅ Đã xác nhận | |
| 5 | Duyệt đề xuất và kinh phí cấp Trường | ✅ Đã xác nhận | |
| 6 | Thẩm định thuyết minh (Mẫu SV03) | ✅ Đã xác nhận | |
| 7 | Ra Quyết định giao và ký hợp đồng (Mẫu SV11) | ✅ Đã xác nhận | Mã đề tài DTSV2025-27 đã cấp, Thuyết minh có đủ chữ ký Khoa/GVHD/Chủ nhiệm/Hiệu trưởng, ngày 27/10/2025 |
| 8 | **Triển khai thực hiện** (Mẫu SV05 nếu điều chỉnh) | 🟡 Đang ở đây | Xem tiến độ kỹ thuật bên dưới |
| 9 | Gia hạn (nếu có, tối đa 1 lần, ≤6 tháng) | ⬜ **CHƯA XÁC NHẬN** | Cần hỏi trực tiếp: đã nộp Mẫu SV05 xin gia hạn chưa? |
| 10 | Nộp hồ sơ nghiệm thu (Mẫu SV04, SV06) | ⬜ Chưa tới | |
| 11 | Nghiệm thu đề tài (Mẫu SV07, SV08, SV09) | ⬜ Chưa tới | |
| 12 | Nộp hồ sơ sau nghiệm thu (Mẫu SV04, SV10) | ⬜ Chưa tới | Trong 50 ngày kể từ ngày có QĐ HĐNT |
| 13 | Ra QĐ công nhận đề tài | ⬜ Chưa tới | |
| 14 | Hoàn tất thanh toán kinh phí | ⬜ Chưa tới | |

Nguồn xác nhận bước 1-7: chữ ký đầy đủ trên Thuyết minh gốc (Khoa Điện-Điện Tử, GVHD Lê Quốc Khương,
Chủ nhiệm Nguyễn Chí Hưỡng, Hiệu trưởng PGS.TS Huỳnh Thanh Nhã), mã số DTSV2025-27 đã cấp.

## Tiến độ kỹ thuật (theo 5 giai đoạn đã đăng ký trong Thuyết minh mục 11.2)

| # | Giai đoạn | Thời gian đăng ký | Người phụ trách | Trạng thái thực tế |
|---|---|---|---|---|
| 1 | Cơ sở lý thuyết, mô phỏng TIA Portal | 1/10 – 15/11 | Nguyễn Chí Hưỡng | ⬜ **Cần bạn xác nhận** |
| 2 | Thiết kế & lắp đặt phần cứng | 16/11 – 15/1 | Hưỡng, Huy, Quốc Anh | ⬜ **Cần bạn xác nhận** |
| 3 | Lập trình & cài đặt biến tần | 16/1 – 31/1 | Quốc Anh, Ngọc Hân | ⬜ **Cần bạn xác nhận** |
| 4 | Lập trình & tích hợp PLC/HMI/WinCC | 1/2 – 15/4 | Quốc Anh, Ngọc Hân | ⬜ **Cần bạn xác nhận** |
| 5 | Vận hành, kiểm tra, hoàn thiện, viết báo cáo | 16/4 – 1/10 | Hưỡng, Huy, Ngọc Hân | ⬜ **Cần bạn xác nhận** |

**Vì sao cột trạng thái để trống:** dự án đã mất dữ liệu số (xem `CLAUDE.md`), nên không có bằng
chứng số hóa nào để tự suy ra tiến độ thật. Tiến độ **vật lý** (thiết bị đã mua, dây đã đấu, code đã
viết trên máy khác...) có thể vẫn còn tồn tại ngoài đời thật dù file bị mất — cần chủ nhiệm và các
thành viên tự đối chiếu và điền lại, không tự suy đoán.

## Việc đang làm (cập nhật liên tục)
- **[2026-08-18]** Dựng lại toàn bộ file quy chuẩn dự án (`PROJECT_GUIDE.md`, `RESEARCH_PROTOCOL.md`,
  `PROJECT_STATUS.md` — file này, đang dựng tiếp `CITATION_POLICY.md`, `FILE_STRUCTURE.md`) dựa trên
  văn bản gốc đã đọc trực tiếp, sau sự cố mất dữ liệu do cài lại Windows không backup.

## Vướng mắc / Rủi ro
- **[2026-08-18] Mốc thời gian** — xem cảnh báo đầu file. Ưu tiên cao nhất hiện tại.
- **[2026-08-18] Tiến độ kỹ thuật thật chưa xác định** — cần chủ nhiệm đối chiếu thực tế (thiết bị,
  phần cứng đã lắp, code cũ trên máy khác nếu còn) trước khi tin bất kỳ % hoàn thành nào.
- **[2026-08-18] Rủi ro liêm chính trích dẫn (chưa xác minh lại trong phiên này):** `PROJECT_STATUS.md`
  cũ (`NCKH_khoi_phuc/`, chưa xác minh) từng ghi nhận phát hiện 5/7 tài liệu tham khảo trong Thuyết
  minh có tiêu đề/tạp chí không khớp file PDF gốc thật. Danh sách 9 tài liệu tham khảo chính thức
  (7 bài báo + 2 tài liệu hãng) đã xác nhận lại từ Thuyết minh gốc, xem `CITATION_POLICY.md`. Cần tự
  tra cứu lại từng nguồn trước khi dùng làm nền cho Chương 1, không tin lại kết luận cũ chưa kiểm
  chứng trong phiên này.

---
*Cập nhật lần cuối: 2026-08-18 — dựng lại sau khi khởi tạo git, dựa trên văn bản gốc.*
