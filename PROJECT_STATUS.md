# PROJECT STATUS

*Nguồn theo dõi tiến độ "sống" — cập nhật mỗi khi hoàn thành một mốc, kèm commit git. Khác với
`RESEARCH_PROTOCOL.md` (snapshot cố định lúc duyệt đề cương), file này phản ánh thực tế hiện tại.*

## ⚠️ Cảnh báo mốc thời gian (đọc trước khi lập kế hoạch)
Thuyết minh gốc ghi thời gian thực hiện gốc: **10/2025 – 10/2026** (12 tháng). **[2026-08-18] Chủ
nhiệm xác nhận bằng lời: đã xin gia hạn.** `NCKH_khoi_phuc/` (chưa xác minh) từng ghi hạn mới là
01/2027 — con số này CHƯA được đối chiếu với văn bản Mẫu SV05 thật trong phiên này, chỉ dựa trên lời
xác nhận miệng. Nếu tìm được file quyết định gia hạn thật, nên chụp/scan lưu vào
`01_Research_Protocol/00_Trao_doi_GVHD/` và cập nhật lại dòng này thành Fact có nguồn thay vì suy
luận từ lời kể.

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
| 9 | Gia hạn (nếu có, tối đa 1 lần, ≤6 tháng) | 🟡 Đã xin (lời xác nhận, chưa có văn bản) | Chủ nhiệm xác nhận 2026-08-18 đã xin gia hạn — chưa có file Mẫu SV05/quyết định gia hạn thật để xác minh ngày hết hạn mới chính xác |
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
| 1 | Cơ sở lý thuyết, mô phỏng TIA Portal | 1/10 – 15/11 | Nguyễn Chí Hưỡng | 🟡 Suy luận: chắc đã làm (đã sang lắp phần cứng) — **chưa xác nhận rõ ràng** |
| 2 | Thiết kế & lắp đặt phần cứng | 16/11 – 15/1 | Hưỡng, Huy, Quốc Anh | 🟡 Đang làm — đã đấu tới E-Stop, VFD chạy bình thường, **đang kẹt ở lỗi E-Stop** (xem Rủi ro) |
| 3 | Lập trình & cài đặt biến tần | 16/1 – 31/1 | Quốc Anh, Ngọc Hân | 🟡 Một phần — VFD đã kết nối/chạy được, nhưng phụ thuộc việc xử lý xong lỗi E-Stop ở giai đoạn 2 |
| 4 | Lập trình & tích hợp PLC/HMI/WinCC | 1/2 – 15/4 | Quốc Anh, Ngọc Hân | ⬜ Cần bạn xác nhận — đã bắt đầu chưa? |
| 5 | Vận hành, kiểm tra, hoàn thiện, viết báo cáo | 16/4 – 1/10 | Hưỡng, Huy, Ngọc Hân | ⬜ Chưa tới |

**[2026-08-18] Cập nhật từ chủ nhiệm (lời xác nhận, chưa có ghi chép kỹ thuật chi tiết):** đã đấu
nối và chạy thử tới mạch E-Stop, biến tần (VFD) kết nối và chạy bình thường khi chưa kích E-Stop.
Còn 2 vấn đề kỹ thuật thật đang chặn tiến độ — xem mục Rủi ro bên dưới để biết chi tiết và mức độ
ưu tiên.

**Về các giai đoạn còn để trống:** tiến độ **vật lý** khác (thiết bị đã mua thêm, code trên máy
khác nếu còn...) chưa được đối chiếu đầy đủ — cần chủ nhiệm và các thành viên tiếp tục xác nhận,
không tự suy đoán thêm ngoài những gì đã báo ở trên.

## Việc đang làm (cập nhật liên tục)
- **[2026-08-18]** Dựng lại toàn bộ file quy chuẩn dự án (`PROJECT_GUIDE.md`, `RESEARCH_PROTOCOL.md`,
  `PROJECT_STATUS.md` — file này, đang dựng tiếp `CITATION_POLICY.md`, `FILE_STRUCTURE.md`) dựa trên
  văn bản gốc đã đọc trực tiếp, sau sự cố mất dữ liệu do cài lại Windows không backup.

## Vướng mắc / Rủi ro
- **[2026-08-18] 🔴 AN TOÀN — lỗi E-Stop không dừng đúng khi nhả nút:** chủ nhiệm báo hệ thống "không
  dừng được khi nhả E-Stop" — mô tả còn mơ hồ, cần làm rõ gấp trước khi thử điện tiếp: (a) khi ấn
  E-Stop, động cơ có dừng ngay không, hay chỉ lỗi xảy ra lúc **nhả** E-Stop ra (VD: động cơ tự chạy
  lại ngoài ý muốn, hoặc mạch không reset đúng trạng thái an toàn)? (b) mạch E-Stop hiện là an toàn
  cứng (relay/contactor cắt điện trực tiếp) hay đi qua logic PLC? Đây là vấn đề **an toàn điện, không
  chỉ là bug phần mềm thông thường** — nếu chưa xác định rõ nguyên nhân, không nên vận hành động cơ
  thật cho tới khi hiểu chắc hành vi mạch E-Stop.
- **[2026-08-18] Chưa có phương pháp xử lý khi mất kết nối RTU** — kết nối Modbus RTU (đồng hồ Selec
  MFM383A-C và/hoặc biến tần) chưa có cơ chế phát hiện/phục hồi khi mất kết nối. Ảnh hưởng tới giai
  đoạn 3-4 (đọc dữ liệu về PLC, giám sát qua HMI/WinCC) — cần thiết kế trước khi tích hợp WinCC.
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
*Cập nhật lần cuối: 2026-08-18 — cập nhật tiến độ kỹ thuật thật + gia hạn theo xác nhận của chủ nhiệm.*
