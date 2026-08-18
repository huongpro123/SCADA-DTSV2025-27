# 03_System_Design

Sơ đồ hệ thống: sơ đồ khối tín hiệu, sơ đồ đấu nối điện chi tiết, kiến trúc truyền thông PLC-HMI-WinCC.

**Đang thiếu (cần bổ sung):**
- Sơ đồ đấu nối điện chi tiết bản chính thức — có bản cũ tham khảo tại
  `NCKH_khoi_phuc/03_System_Design/So_do_dau_noi_dien_chi_tiet.svg` và `So_do_ket_noi_he_thong.svg`
  (từ nội dung chưa xác minh, nhưng đối chiếu kỹ thuật với mô tả thật của bạn về mạch E-Stop khớp
  đúng — có thể dùng làm điểm khởi đầu, cần tự kiểm tra lại từng chi tiết trước khi coi là chính
  thức)
- Cần cập nhật sơ đồ để thêm: tiếp điểm phụ E-Stop về DI PLC (fix lỗi tự chạy lại đã phát hiện
  2026-08-18)

## `Dinh_huong_mo_rong_WebSCADA_S71500ao_ChuaDuyetGVHD.txt`
Định hướng mở rộng kiến trúc (Web SCADA qua API, PLC S7-1500 ảo qua PLCSIM Advanced, Modbus RTU cho
đồng hồ đo) — **chủ nhiệm xác nhận đây là hướng muốn theo, nhưng CHƯA có xác nhận GVHD bằng văn bản**.
Đây là thay đổi phạm vi thật so với Thuyết minh gốc — xem chi tiết và bước cần làm trong
`PROJECT_STATUS.md` mục "Thay đổi phạm vi đang đề xuất". Không dùng làm căn cứ thiết kế chính thức
cho tới khi có xác nhận.
