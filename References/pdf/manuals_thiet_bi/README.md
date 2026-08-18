# Manual thiết bị chính hãng — tự động tải về 2026-08-18

*Khác với `NCKH_khoi_phuc/References/manuals_thiet_bi/Manual_thiet_bi_da_chon.md` (bản cũ chỉ ghi
link, chưa tải được file do môi trường không có mạng) — lần này đã tải được file PDF thật, xác minh
qua `file` (kiểm tra định dạng thật, không chỉ đuôi tên file).*

## Đã tải thành công

| File | Thiết bị | Nguồn | Trạng thái xác nhận |
|---|---|---|---|
| `Siemens_S7-1200_System_Manual` — **chưa tải được, xem bên dưới** | PLC CPU 1211C | support.industry.siemens.com | Model đã xác nhận (Thuyết minh mục 11.1.1) |
| `Wecon_VNZ100_User_Manual_V3.5.pdf` (41 trang) | Biến tần | ftp.we-con.com.cn (chính hãng) | ⚠️ **Model CHƯA xác nhận** — xem cảnh báo bên dưới |
| `Selec_MFM383A-C_Datasheet.pdf` (2 trang) | Đồng hồ đo đa năng | tme.eu (nhà phân phối chính hãng) | Model đã xác nhận (Thuyết minh mục 11.1.1) |

## ⚠️ Cảnh báo model biến tần — CẦN BẠN TỰ XÁC NHẬN
Thuyết minh gốc chỉ ghi "biến tần Wecon", không nêu model cụ thể. File cũ (`Danh_muc_thiet_bi...xlsx`,
2026-08-08) từng ghi "Wecon VNZ200"; ghi chú khác chưa xác minh trong `NCKH_khoi_phuc/` từng nói đã
sửa lại thành "VNZ100" sau khi soi tem máy thật. Trong phiên tìm kiếm này:
- **VNZ100**: có trang chính thức trên `we-con.com.cn` (domain thật của Wecon), tải được manual đầy
  đủ 41 trang — có vẻ là dòng sản phẩm thật, đang bán chính hãng
- **VNZ200**: KHÔNG tìm thấy trang nào trên `we-con.com.cn` — chỉ có kết quả từ ManualsLib (bên thứ
  ba) và một kết quả tên gần giống ("NZ200 Series") lại thuộc **hãng khác hoàn toàn**
  (whzoncn.com — Wuhu Zhongchen, không phải Wecon)

**→ Bằng chứng nghiêng về VNZ100 là đúng, nhưng đây vẫn chỉ là suy luận từ tìm kiếm web, KHÔNG thay
thế được việc tự đọc tem máy thật.** Trước khi dùng file manual này để thiết kế đấu nối, tự kiểm tra
lại tem máy biến tần thật.

## Chưa tải được — cần bạn tự tải
- **Siemens S7-1200 System Manual** — trang `support.industry.siemens.com` có bot protection, script
  tự động không tải được (lỗi 403). Link xác nhận thật, tự mở bằng trình duyệt và tải về:
  https://support.industry.siemens.com/cs/attachments/36932465/s71200_system_manual_en-US_en-US.pdf

## Chưa tìm — model chưa chốt, không suy đoán thêm
- HMI (Thuyết minh không nêu model cụ thể — bản cũ từng chọn Weintek eMT3070P/B nhưng chưa xác nhận
  lại trong phiên này)
- Bộ chuyển đổi tín hiệu PT100 (chưa chốt hãng/model)
- Contactor, rơ-le nhiệt, Aptomat, relay trung gian, bộ nguồn 24VDC, E-Stop (chưa chốt model cụ thể
  trong Thuyết minh — cần đối chiếu ảnh tem máy thật nếu đã mua)
