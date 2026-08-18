# RESEARCH_PROTOCOL.md — Research Protocol gốc, phiên bản chính thức

*File này giữ snapshot tại thời điểm đề cương được duyệt — không sửa lại sau này, mọi cập nhật tiến
độ thực tế nằm ở `PROJECT_STATUS.md`. Nguồn: `DTSV2025-27 TM_NCHuong_ThS.LQKhuong hd.pdf`, đọc trực
tiếp 2026-08-18.*

## 1. Câu hỏi nghiên cứu (RQ)

**Lưu ý:** Thuyết minh gốc không viết dưới dạng RQ1-RQ4 tường minh — đây là 4 câu hỏi được **suy
luận, diễn đạt lại** từ mục "Mục tiêu" và "Nội dung nghiên cứu" (mục 8, 11.1) để tiện theo dõi
xuyên suốt dự án. Đây là *Suy luận có căn cứ*, không phải trích nguyên văn — nên xác nhận lại với
GVHD nếu dùng làm khung chính thức cho báo cáo.

- **RQ1:** Thiết kế phần cứng (tủ điều khiển, PLC S7-1200, biến tần Wecon, động cơ KĐB 3 pha, cảm
  biến PT100, đồng hồ đo Selec MFM383A-C) như thế nào để điều khiển tốc độ vô cấp một động cơ KĐB 3
  pha qua biến tần?
- **RQ2:** Xây dựng kiến trúc truyền thông S7 native/PROFINET giữa PLC, HMI và WinCC như thế nào để
  tạo thành một hệ mini SCADA tích hợp đủ 3 cấp (thiết bị – điều hành – giám sát)?
- **RQ3:** Lập trình logic PLC ra sao để giám sát chính xác các thông số vận hành (tốc độ, dòng
  điện, nhiệt độ) và thực hiện chức năng bảo vệ cơ bản (quá tải/quá dòng, quá nhiệt)?
- **RQ4:** Hệ thống mini SCADA đã xây dựng có đạt hiệu quả cải thiện so với phương pháp khởi động
  trực tiếp truyền thống hay không (mục tiêu định lượng: giảm 15-20% dòng điện khởi động)?

## 2. Mục tiêu (trích nguyên văn Thuyết minh mục 8)
Xem đầy đủ tại `PROJECT_GUIDE.md` mục "Mục tiêu".

## 3. Phạm vi (Fact — trích Thuyết minh mục 9.2)
Xem đầy đủ tại `PROJECT_GUIDE.md` mục "Đối tượng, phạm vi nghiên cứu". Điểm mấu chốt cần nhớ khi
viết bất kỳ chương nào: **chỉ 1 động cơ**, **không Cloud/IIoT/OPC UA mở rộng**, bảo vệ chỉ ở mức cơ
bản (quá tải/quá dòng/quá nhiệt).

## 4. Success criteria — bản chính thức (Fact, trích nguyên văn mục 12.4)
1. Điều khiển được tốc độ động cơ qua biến tần
2. Giám sát được ít nhất 3 thông số: tốc độ, nhiệt độ, dòng điện
3. Hiển thị được dữ liệu lên HMI
4. Có khả năng bảo vệ khi quá tải cơ bản

**Khuyến nghị (chưa phải sự kiện đã duyệt):** 4 tiêu chí trên viết dạng định tính, chưa có ngưỡng đo
lường cụ thể (VD: "giám sát được" chưa nói rõ sai số cho phép bao nhiêu %). Nếu muốn dùng để thiết
kế thực nghiệm Chương 3, nên định lượng hóa thêm — nhưng phải trình GVHD xác nhận trước khi coi là
tiêu chí chính thức, không tự ý thêm số liệu chưa được duyệt.

## 5. Đóng góp/tác động dự kiến (Fact, trích mục 13)
- Giáo dục: mô hình học tập/thực hành cho sinh viên ngành Điện - Điện tử - Tự động hóa
- Khoa học công nghệ: chứng minh tính khả thi xây dựng hệ điều khiển/giám sát cho ứng dụng vừa/nhỏ,
  kết hợp PLC + biến tần + cảm biến + HMI/WinCC thành giải pháp hoàn chỉnh
- Kinh tế - xã hội: giải pháp chi phí đầu tư hợp lý, dễ triển khai cho cơ sở sản xuất vừa/nhỏ

## 6. Nhóm thực hiện & phân công
Xem `PROJECT_GUIDE.md` mục "Nhóm thực hiện" và "Tiến độ thực hiện".

## 7. Điểm cần chất vấn/xác minh thêm (chưa xác nhận)
- Có Mẫu SV05 xin gia hạn thời gian thực hiện hay chưa? Thuyết minh gốc ghi hạn 10/2026, không có
  ghi chú gia hạn nào trong chính văn bản này.
- `NCKH_khoi_phuc/CHANGELOG.md` (nội dung chưa xác minh, dựng lại từ trí nhớ hội thoại) có ghi nhận
  GVHD đồng ý miệng mở rộng phạm vi sang OPC UA + Telegram bot + PROFINET I-Device — nếu đúng, đây
  là thay đổi so với phạm vi gốc ở mục 3 và cần Mẫu SV05 hoặc xác nhận văn bản mới hợp lệ.

*Cập nhật lần cuối: 2026-08-18 — dựng lại từ Thuyết minh gốc sau khi mất dữ liệu dự án cũ.*
