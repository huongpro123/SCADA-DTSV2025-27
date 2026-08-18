# Nội dung xin GVHD xác nhận mở rộng phạm vi đề tài DTSV2025-27

*Bản nháp — chủ nhiệm đọc lại, chỉnh sửa văn phong theo ý muốn trước khi gửi. Mục đích: xin xác nhận
bằng văn bản (email hoặc biên bản) theo đúng quy trình nội bộ đã thống nhất, tránh rủi ro khi hội
đồng chất vấn về sự khác biệt so với Thuyết minh gốc.*

---

Kính gửi Thầy Lê Quốc Khương,

Đề tài DTSV2025-27 hiện đã lắp đặt phần cứng cơ bản đúng theo Thuyết minh đã duyệt (PLC S7-1200
CPU 1211C, biến tần Wecon VNZ100, HMI Weintek eMT3070B, đồng hồ đo Selec MFM383A-C, các thiết bị
bảo vệ/an toàn đi kèm), đang trong giai đoạn hoàn thiện đấu nối và lập trình.

Trong quá trình triển khai, nhóm có mong muốn mở rộng thêm hai nội dung so với phạm vi đã duyệt
trong Thuyết minh (mục 9.2.1, vốn ghi rõ không nghiên cứu tích hợp giao thức mạng mở rộng hay kết
nối lên nền tảng Cloud/IIoT):

1. **Kiến trúc PROFINET I-Device:** CPU S7-1211C thật đóng vai trò I-Device dưới một CPU S7-1500 ảo
   (chạy trên phần mềm PLCSIM Advanced) đóng vai trò IO Controller, nhằm thử nghiệm khả năng tích
   hợp thiết bị thật vào một kiến trúc điều khiển phân cấp lớn hơn.
2. **Giám sát qua giao diện Web (Web SCADA) thông qua API**, bổ sung thêm một kênh giám sát ngoài
   HMI tại chỗ và WinCC.

Nhóm xin phép hỏi ý kiến Thầy về hai nội dung trên:
- Thầy có đồng ý cho phép mở rộng phạm vi đề tài theo hướng này không?
- Nếu đồng ý, nội dung mở rộng nên được ghi nhận theo hình thức nào (điều chỉnh trong Mẫu SV05, hay
  chỉ cần xác nhận qua email để lưu hồ sơ)?
- Phần kiến trúc cơ bản đã duyệt (PLC-HMI-WinCC qua S7 native/PROFINET, đọc đồng hồ đo qua Modbus
  RTU) vẫn được giữ nguyên làm nền tảng chính — hai nội dung trên chỉ là lớp bổ sung phía trên,
  không thay thế.

Nhóm cảm ơn Thầy đã dành thời gian xem xét.

Trân trọng,
Nguyễn Chí Hưỡng — Chủ nhiệm đề tài DTSV2025-27

---
*Ghi chú nội bộ (không gửi kèm): nếu Thầy đồng ý, cập nhật ngay `PROJECT_STATUS.md` mục "Thay đổi
phạm vi đang đề xuất" thành đã duyệt, kèm ngày và hình thức xác nhận (email/biên bản), theo đúng quy
định trong `CLAUDE.md`.*
