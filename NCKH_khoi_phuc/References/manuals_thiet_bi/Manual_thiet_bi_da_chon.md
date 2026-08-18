# Tài liệu kỹ thuật thiết bị đã chọn — tra cứu 2026-08-08, cập nhật 2026-08-09

Ghi chú: đây là tổng hợp trích từ manual/datasheet CHÍNH THỨC của hãng (link trực tiếp bên dưới).
Chưa tải được file PDF gốc về máy do môi trường làm việc không có kết nối mạng trực tiếp — bạn nên
tự tải về từ link gốc và lưu vào `References/` để dùng khi vẽ sơ đồ đấu nối ở Chương 3.

**Cập nhật 2026-08-09:** đối chiếu 21 ảnh tem máy thiết bị thật, phát hiện biến tần thực tế là dòng
**VNZ100** (không phải VNZ200 như tra cứu trước đó). Mục 1 bên dưới đã được viết lại hoàn toàn theo
VNZ100. HMI xác nhận đúng là eMT3070B (mục 3), không còn là nghi vấn.

---

## 1. Biến tần Wecon VNZ100 Series (SỬA LỖI — trước đó ghi nhầm VNZ200)

**Nguồn chính thức:** Wecon VNZ100 Series User Manual, phiên bản V3.5 (10/02/2025)
Link: https://ftp.we-con.com.cn/Download/WIKI/Inverter/Manual/Wecon%20VNZ100%20User%20Manual%20V3.5%20250210.pdf

**Model đã xác nhận qua tem máy:** VNZ100-1R5G-2. Giải mã theo manual (mục 1.2 Nameplate):
- VNZ100 = tên dòng sản phẩm
- 1R5 = 1.5kW (công suất định mức)
- G = mô-men không đổi (constant torque); P = mô-men biến đổi (variable torque)
- 2 = ngõ vào 1 pha AC220V; 4 = ngõ vào 3 pha AC380V

**Thông số chính (theo bảng Models, mục 1.2):** ngõ vào 1PH AC220V±15%, dòng vào định mức 10.0A,
dòng ra định mức 7.0A, công suất áp dụng động cơ 1.5kW. Kích thước (mục 1.3): W68×H132×D102mm, hỗ
trợ gắn ray DIN 35mm tiêu chuẩn. Quá tải cho phép 150% trong 60 giây (mô-men không đổi). Dải tần số
0.10–400.00Hz. Điều khiển V/F. Bảo vệ: quá dòng, quá áp, thấp áp, quá nhiệt module, lỗi ngoài, lỗi
truyền thông.

**Thông tin đấu nối (Chương 3 — Wiring, giữ nguyên tên terminal như dòng VNZ200 đã tra cứu trước đó):**
| Terminal | Chức năng |
|---|---|
| FWD | Lệnh chạy thuận (ngõ vào đa chức năng) |
| REV | Lệnh chạy nghịch (ngõ vào đa chức năng) |
| S1–S4 | Ngõ vào đa chức năng (reset lỗi, tốc độ đa cấp...) |
| FIV | Ngõ vào analog điện áp 0–10V (đặt tần số) |
| FIC | Ngõ vào analog dòng điện 0–20mA (đặt tần số, chọn qua switch J2) |
| 10V | Nguồn phụ cấp cho mạch đặt tần số |
| GND | Chân chung tín hiệu vào |
| FOV / MCM / MO1 | Ngõ ra đa chức năng / analog ra |
| RS- / RS+ | Truyền thông RS485 (Modbus RTU/ASCII) |
| RA / RB / RC | Ngõ ra relay (thường mở / thường đóng / chung) — dùng cho cảnh báo lỗi |

**Lưu ý khi dùng L1/L2 (nguồn vào 1 pha):** manual ghi rõ "When using a single-phase power supply,
please access from terminals L1 and L2" — cần cập nhật thiết kế cấp nguồn tủ điện theo 1 pha 220V,
KHÔNG phải 3 pha như giả định ban đầu khi còn tưởng là VNZ200 dòng "-4".

---

## 2. Đồng hồ đo đa năng Selec MFM383A-C

**Nguồn chính thức:** Selec MFM383A Datasheet (qua TME.eu, phân phối chính hãng Selec)
Link: https://www.tme.eu/Document/abc85625e8052bc0d4a95e0eb4a405f3/MFM383A.pdf
Trang sản phẩm chính hãng: https://www.selec.com/product-details/economical-lcd-multifunction-meter

**Thông số chính:**
- Kích thước: 96 × 96 mm (mặt trước), cutout lắp tủ điện: 91.5 × 91.5 mm, sâu 90.5mm
- Nguồn phụ (Auxiliary Supply): 100–240V AC, -15%/+12%, 50/60Hz
- Đo được: điện áp (L-N 11–300V AC, L-L 19–519V AC), dòng điện (định mức 5A AC qua CT, min 11mA – max 6A),
  tần số 45–65Hz, công suất, điện năng, hệ số công suất — sai số ±0.5%
- Cách đấu nối: 3 pha 3 dây / 3 pha 4 dây / 2 pha 3 dây / 1 pha 2 dây (chọn được)
- Ngõ vào dòng điện qua CT (biến dòng): CT sơ cấp lập trình được 1–10000A, CT thứ cấp 1A hoặc 5A —
  XÁC NHẬN: đề tài SẼ CẦN cảm biến dòng CT (đúng như đã suy luận trong bảng thiết bị, mục "Cảm biến
  dòng điện CT") vì đồng hồ này không đo dòng trực tiếp mà qua CT
- Ngõ vào điện áp: đo trực tiếp qua PT (biến áp đo lường), PT sơ cấp lập trình 100V–10kV
- Truyền thông: RS485, Modbus RTU (tùy chọn — chỉ có ở bản có "-C" hoặc "-CU" theo bảng Ordering
  Information) — MFM383A-C đã chọn CÓ RS485/Modbus, phù hợp yêu cầu truyền dữ liệu về PLC
- Ký hiệu đấu dây (Terminal Connection): I1/I2/I3 (dòng điện qua CT, cặp S1-S2 mỗi pha), V1/V2/V3
  (điện áp từng pha), L/N (nguồn cấp cho đồng hồ), cổng RS485 riêng

---

## 3. HMI Weintek eMT3070B (đã xác nhận qua tem máy 2026-08-09)

**Đã xác nhận:** tem máy vật lý thật ghi rõ "eMT3070B" (S/N: 1712100899), khớp đúng với dự đoán
trước đó khi tra cứu thấy "eMT3070P" không tồn tại là sản phẩm Weintek — dòng thật là eMT3070A/B
(192×138mm), không phải eMT3105P (259×201mm).

**Nguồn chính thức:**
- Datasheet: https://dl.weintek.com/public/eMT3000/eng/Datasheet/eMT3070B1_Datasheet_ENG.pdf
- Installation Guide (chung cho cả dòng eMT3105P/3070/3120/3150A): https://dl.weintek.com/public/eMT3000/eng/Installation/GME3105P1_eMT3105P_3070_3120_3150A_Installation.pdf

**Thông số chính (eMT3070B):**
- Màn hình: 7" TFT 800×480, cảm ứng điện trở 4 dây
- Kích thước: 200.3 × 146.3 × 42.5 mm; cutout lắp tủ/panel: 192 × 138 mm
- Nguồn cấp: 24V DC ±20% (dòng tiêu thụ ~400mA@24VDC) — CẦN nguồn 24VDC riêng (khớp với mục "Bộ
  nguồn 24VDC" đã suy luận trong bảng thiết bị)
- Cổng: Ethernet 10/100 (dùng để kết nối S7-1200 qua Ethernet), USB Host, USB Client, khe thẻ SD,
  COM1/COM3 (RS232 hoặc RS485), CAN Bus
- Không có cổng PROFINET/S7 riêng — kết nối PLC Siemens qua driver Ethernet S7CommPlus của Weintek
  (không phải giao thức PROFINET/S7 native đúng nghĩa TIA Portal)
- Phần mềm cấu hình: EasyBuilder Pro (tải project vào HMI qua Ethernet, phím tắt F7)

---

## 4. Thiết bị phụ trợ tủ điện mới xác nhận (2026-08-09, chưa tra manual chính hãng riêng)

Các thiết bị này được xác nhận qua ảnh tem máy vật lý, thông số kỹ thuật đầy đủ đã ghi trong
`03_System_Design/Danh_muc_thiet_bi_can_xac_dinh.xlsx` (mục 6, 12, 17, 19, 20, 21). Là vật tư
tủ điện tiêu chuẩn (contactor, rơ-le nhiệt, Aptomat, bộ nguồn, biến áp, SPD, relay trung gian) —
không cần manual riêng cho báo cáo học thuật, chỉ cần khi thi công thực tế thì tra catalog hãng
tương ứng (Mitsubishi Electric, CHINT, MEAN WELL, CITEL, Schneider Electric, CNAOM).

---

*Nguồn trích dẫn đầy đủ (để đối chiếu khi cần):*
- https://ftp.we-con.com.cn/Download/WIKI/Inverter/Manual/Wecon%20VNZ100%20User%20Manual%20V3.5%20250210.pdf
- https://www.tme.eu/Document/abc85625e8052bc0d4a95e0eb4a405f3/MFM383A.pdf
- https://dl.weintek.com/public/eMT3000/eng/Datasheet/eMT3070B1_Datasheet_ENG.pdf
- https://dl.weintek.com/public/eMT3000/eng/Installation/GME3105P1_eMT3105P_3070_3120_3150A_Installation.pdf
