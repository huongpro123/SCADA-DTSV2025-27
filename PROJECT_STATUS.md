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

## Checklist việc cần bổ sung (dựng 2026-08-18, cập nhật cùng ngày sau khi bạn bổ sung ảnh/PDF)
Cấu trúc thư mục mục tiêu đã tạo đủ (xem `FILE_STRUCTURE.md`), mỗi thư mục có `README.md` liệt kê
chi tiết — đây là bản tóm tắt để dễ quét nhanh:

| Thư mục | Đã có | Đang thiếu |
|---|---|---|
| `01_Research_Protocol/00_Trao_doi_GVHD/` | — | Biên bản gia hạn (SV05) thật |
| `03_System_Design/` | Sơ đồ cũ (nhiều chi tiết đã được ảnh thật xác nhận đúng) | Cập nhật sơ đồ theo fix E-Stop mới |
| `04_Hardware/01_hinh_anh_thiet_bi/` | ✅ **26 ảnh tem máy thiết bị thật** — gần như toàn bộ danh mục | Selec MFM383A-C, đèn báo/còi báo/nút bấm |
| `05_Simulation/` | ✅ Project TIA Portal `aovathat.ap20` (chủ nhiệm xác nhận đúng bản, 2026-08-18) | Code PLC xử lý E-Stop vẫn đang chờ |
| `06_Experiment/` | — | Bộ tiêu chí định lượng (cần GVHD duyệt), dữ liệu đo thực nghiệm |
| `08_BaoCao/` | Chương 1-2 cũ (cần rà lại trích dẫn) | Mẫu SV04 thật, Chương 3 trở đi |
| `References/pdf/` | ✅ 6/15 nguồn Matrix có PDF thật (đã xác minh DOI) | 9 nguồn còn lại, phần lớn cần tài khoản thư viện trường |
| `References/pdf/manuals_thiet_bi/` | ✅ Siemens S7-1200, Wecon VNZ100 (model đã CHỐT qua ảnh thật), Selec MFM383A-C | — |

**[2026-08-18] Đã giải quyết dứt điểm qua ảnh tem máy thật:** model VFD chính xác là **VNZ100-1R5G-2**
(không phải VNZ200); HMI là **Weintek eMT3070B** (serial 1712100899 khớp chính xác ghi chú cũ); đấu
dây động cơ **Δ220V/Y380V** xác nhận qua hộp đấu dây; toàn bộ Aptomat/contactor/relay/SPD/nguồn/PT100
converter đã có ảnh thật, khớp gần như hoàn toàn với `NCKH_khoi_phuc/` (nội dung trước đó bị coi là
"chưa xác minh") — đây là bằng chứng mạnh cho thấy phần lớn công việc trước khi mất dữ liệu là có
thật, không phải suy đoán.

**Còn thiếu, chỉ bạn làm được:** Selec MFM383A-C (ảnh), đèn báo/còi báo/nút bấm, xác định đúng
project TIA Portal thật, gửi code PLC xử lý E-Stop.
Đây đều là việc chỉ chủ nhiệm/nhóm làm được (đọc tem máy, hoặc quyết định mua nếu chưa có).

## Việc đang làm (cập nhật liên tục)
- **[2026-08-18]** Dựng lại toàn bộ file quy chuẩn dự án, tạo cấu trúc thư mục mục tiêu đầy đủ, tự
  tìm và tải 2/3 manual thiết bị đã xác nhận model (Wecon VFD, Selec MFM383A-C) từ nguồn chính hãng
  trên web, sau sự cố mất dữ liệu do cài lại Windows không backup.

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
- **[2026-08-18] 🔴 Rủi ro liêm chính trích dẫn — ĐÃ XÁC MINH ĐỘC LẬP LẦN 2, KẾT QUẢ TRÙNG KHỚP:** tự
  tra cứu lại (không đọc ghi chú cũ trước) qua WebSearch, kết quả trùng khớp với phát hiện cũ — ít
  nhất 3/7 tài liệu [1]-[7] trong Thuyết minh có tiêu đề/tạp chí không khớp bài thật, 2/7 hoàn toàn
  không tìm ra dấu vết. Đây là vấn đề thật, cần **báo GVHD**, không tự sửa âm thầm. Chi tiết đầy đủ
  trong `CITATION_POLICY.md`.

---
*Cập nhật lần cuối: 2026-08-18 — cập nhật tiến độ kỹ thuật thật + gia hạn theo xác nhận của chủ nhiệm.*
