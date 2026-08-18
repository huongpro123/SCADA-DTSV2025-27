# PROJECT_GUIDE.md — Mô tả toàn bộ đề tài

*Nguồn: toàn văn `DTSV2025-27 TM_NCHuong_ThS.LQKhuong hd.pdf` (Thuyết minh gốc đã duyệt, ký
27/10/2025) — đọc trực tiếp ngày 2026-08-18, không suy đoán từ nguồn thứ cấp.*

## Thông tin đề tài
- **Tên đề tài:** Điều khiển và giám sát động cơ 3 pha bằng hệ mini SCADA
- **Mã số:** DTSV2025-27
- **Thời gian thực hiện:** 12 tháng, 10/2025 – 10/2026 (theo Thuyết minh gốc — xem cảnh báo mốc
  thời gian trong `PROJECT_STATUS.md`)
- **Kinh phí:** 6.600.000đ (5.600.000đ Trường cấp + 1.000.000đ nguồn khác)
- **Địa chỉ ứng dụng:** Phòng thí nghiệm Vật liệu điện và cao áp, Trường ĐH Kỹ Thuật - Công Nghệ
  Cần Thơ

## Nhóm thực hiện
| Vai trò | Họ tên | MSSV | Khoa/Bộ môn |
|---|---|---|---|
| Chủ nhiệm đề tài | Nguyễn Chí Hưỡng | KTNL2311010 | Khoa Điện - Điện Tử, ngành CNKT Năng lượng |
| Thành viên | Hồ Nguyễn Quốc Anh | KTNL2311050 | |
| Thành viên | Nguyễn Thị Ngọc Hân | KTNL2311037 | |
| Thành viên | Tăng Quốc Huy | KTNL2311011 | |
| GVHD | ThS. Lê Quốc Khương | | BM Điện - Điện Tử |

**Đây là đề tài nhóm 4 sinh viên, không phải một mình chủ nhiệm làm.** Nếu về sau các thành viên
khác cùng thao tác trên repo git này, cân nhắc thêm họ làm collaborator trên GitHub và dùng lại
quy trình PR cho các thay đổi lớn (xem `CLAUDE.md` mục Kỷ luật git).

## Bối cảnh & lý do đề xuất
Động cơ không đồng bộ 3 pha là thiết bị cốt lõi trong hầu hết dây chuyền sản xuất công nghiệp, nhưng
các phương pháp điều khiển/bảo vệ truyền thống (rơ-le, công-tắc-tơ) đáp ứng chậm, thiếu linh hoạt,
khó tích hợp vào hệ thống tự động hóa hiện đại. Đề tài xây dựng một hệ mini SCADA hoàn chỉnh — không
dừng ở điều khiển động cơ bằng PLC đơn lẻ, mà tích hợp đủ 3 cấp: giám sát trực quan qua HMI tại chỗ,
thu thập/lưu trữ dữ liệu qua WinCC, dùng chuẩn truyền thông công nghiệp PROFINET/S7 của Siemens làm
nền tảng kết nối — nhằm khắc phục 2 khoảng trống đã xác định trong các nghiên cứu trong nước: thiếu
kiến trúc tích hợp đầy đủ từ cấp thiết bị đến cấp giám sát, và hạ tầng kết nối theo chuẩn công nghiệp
hiện đại còn hạn chế.

## Mục tiêu

**Mục tiêu tổng quát:** Nghiên cứu và xây dựng thành công một hệ thống mini SCADA có khả năng điều
khiển, giám sát động cơ không đồng bộ 3 pha thông qua biến tần.

**Về thực hành (mục tiêu cụ thể):**
- Thiết kế và lắp đặt phần cứng: tủ điều khiển, động cơ, biến tần, PLC, cảm biến
- Lập trình điều khiển logic trên PLC để điều khiển biến tần
- Thiết kế giao diện HMI để giám sát và điều khiển
- Thiết lập kênh truyền thông giữa PLC và máy tính chạy phần mềm SCADA (WinCC)

**Kết quả dự kiến:** Giảm 15-20% dòng điện khởi động so với phương pháp khởi động trực tiếp khi kết
nối với biến tần và cảm biến.

## Đối tượng, phạm vi nghiên cứu

**Đối tượng:**
- Lý thuyết & phương pháp: nguyên lý điều khiển động cơ KĐB 3 pha, kỹ thuật PWM qua biến tần, giải
  pháp bảo vệ/chẩn đoán động cơ công nghiệp; kiến trúc và cơ chế truyền thông S7 native/PROFINET
  giữa PLC S7-1200, HMI, và WinCC
- Thực nghiệm & ứng dụng: mô hình mini SCADA vật lý hoàn chỉnh, điều khiển/giám sát trực tiếp 1 động
  cơ KĐB 3 pha cấp nguồn từ biến tần

**Phạm vi nội dung (đọc kỹ — đây là ranh giới chính thức đã duyệt):**
- Chỉ điều khiển tốc độ vô cấp và giám sát thông số vận hành của **01 động cơ KĐB 3 pha duy nhất**
  qua biến tần (PWM)
- Thu thập dữ liệu qua đồng hồ đa năng **Selec MFM383A-C** truyền về PLC
- Chức năng bảo vệ/chẩn đoán tập trung vào lỗi cơ bản, quan trọng nhất: quá tải/quá dòng, quá nhiệt
  (dùng cảm biến PT100). Lỗi phức tạp khác chỉ dừng ở mức nghiên cứu lý thuyết/mô phỏng đơn giản
  trên PLC/HMI
- Công nghệ tích hợp SCADA xây dựng trên Siemens TIA Portal (PLC S7-1200, HMI, WinCC), giao thức
  S7 native/PROFINET để truyền thông nội bộ
- **KHÔNG nghiên cứu** tích hợp giao thức mạng mở rộng hay kết nối lên nền tảng Cloud/IIoT — dù xu
  hướng thế giới đang dịch chuyển mạnh sang OPC UA để tích hợp Cloud/IoT, đề tài **cố tình** chỉ tập
  trung hoàn thiện nền tảng SCADA công nghiệp cơ bản trên mạng LAN, tạo bước đệm cho việc mở rộng
  sau này chứ không làm trong phạm vi đề tài
- Phạm vi thời gian/không gian: 12 tháng (10/2025–10/2026), tại phòng thực hành cao áp của Trường

**Lưu ý quan trọng:** phạm vi gốc này **khác** với những gì `NCKH_khoi_phuc/CHANGELOG.md` (nội dung
chưa xác minh) mô tả — bản đó ghi nhận GVHD đã đồng ý miệng mở rộng sang OPC UA + Telegram bot,
PROFINET I-Device. Nếu mở rộng đó có thật, nó là **thay đổi so với Thuyết minh gốc này** và cần xác
nhận lại bằng văn bản trước khi coi là phạm vi chính thức — xem `CLAUDE.md` mục "Thay đổi phạm vi".

## Phương pháp nghiên cứu
1. **Lý thuyết & tổng hợp:** phân tích nguyên lý động cơ KĐB 3 pha, thuật toán điều khiển biến tần
   (PWM), cấu trúc hệ mini SCADA; tham khảo tài liệu kỹ thuật chính hãng (Siemens, Selec) để chọn
   phương pháp truyền thông và tiêu chuẩn thiết kế tủ điện
2. **Mô hình hóa & thiết kế:** dùng TIA Portal mô phỏng hoạt động PLC, kiểm tra logic điều khiển và
   các hàm bảo vệ trước khi nạp vào phần cứng thật; xây dựng sơ đồ nguyên lý, sơ đồ đấu nối, thiết
   kế giao diện HMI/WinCC theo nguyên tắc công thái học
3. **Thực nghiệm (phương pháp cốt lõi):** đo thông số cơ bản khi động cơ chạy trực tiếp không qua
   biến tần để lập dữ liệu nền; vận hành hệ mini SCADA đã chế tạo để thu thập/xử lý/giám sát dữ liệu
   theo thời gian thực; phân tích dữ liệu thu được để đánh giá hiệu suất, độ chính xác, khả năng xử
   lý lỗi của hệ thống

## Sản phẩm dự kiến
| Sản phẩm | Số lượng | Yêu cầu khoa học |
|---|---|---|
| Mô hình hệ thống điều khiển mini SCADA | 01 bộ | Điều khiển được tốc độ động cơ qua biến tần; giám sát được ≥3 thông số (tốc độ, nhiệt độ, dòng điện); hiển thị được dữ liệu lên HMI; có khả năng bảo vệ khi quá tải cơ bản |

Loại sản phẩm khoa học đăng ký: bài đăng kỷ yếu hội nghị/hội thảo quốc tế. Loại sản phẩm ứng dụng:
thiết bị máy móc + sơ đồ/bản thiết kế.

## Tiến độ thực hiện (theo Thuyết minh gốc, mục 11.2)
| # | Nội dung | Thời gian | Người phụ trách |
|---|---|---|---|
| 1 | Nghiên cứu cơ sở lý thuyết, mô phỏng trên TIA Portal | 1/10 – 15/11 (46 ngày) | Nguyễn Chí Hưỡng |
| 2 | Thiết kế & lắp đặt phần cứng, cấu hình đồng hồ đo/cảm biến | 16/11 – 15/1 (61 ngày) | Hưỡng, Huy, Quốc Anh |
| 3 | Lập trình & cài đặt thông số biến tần | 16/1 – 31/1 (15 ngày) | Quốc Anh, Ngọc Hân |
| 4 | Lập trình & tích hợp hệ thống (PLC/HMI/WinCC) | 1/2 – 15/4 (91 ngày) | Quốc Anh, Ngọc Hân |
| 5 | Vận hành, kiểm tra, hoàn thiện, viết báo cáo | 16/4 – 1/10 (169 ngày) | Hưỡng, Huy, Ngọc Hân |

*Cập nhật lần cuối: 2026-08-18*
