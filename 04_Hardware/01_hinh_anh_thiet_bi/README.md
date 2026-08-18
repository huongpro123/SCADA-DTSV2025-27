# 01_hinh_anh_thiet_bi

Ảnh tem máy thiết bị thật — bạn đã cung cấp 2026-08-18, xác nhận qua ảnh trực tiếp (không phải suy
đoán). 26/26 ảnh đã xem và nhận diện, đổi tên mô tả đúng thiết bị (từ tên file gốc dạng
timestamp/hash).

## Thiết bị đã xác nhận qua ảnh thật
| File | Thiết bị | Model | Ghi chú |
|---|---|---|---|
| 01 | PLC | Siemens SIMATIC S7-1200 CPU 1211C AC/DC/RLY | Khớp Thuyết minh |
| 02 | Relay trung gian | CNAOM HH52P(MY2NJ) | Chân 13(-)/14(+) có cực → khả năng cuộn hút DC, cần đo lại trước khi đấu |
| 03 | Aptomat | CHINT NXB-63H C32, 3 cực | |
| 04 | Aptomat | CHINT NXB-63 C16, 2 cực | |
| 05 | Aptomat | CHINT NXB-63 C6, 2 cực | |
| 06 | Biến tần (VFD) | **Wecon VNZ100-1R5G-2** | ✅ Model đã xác nhận chính thức qua tem máy — giải quyết dứt điểm nghi vấn VNZ100 vs VNZ200. Input 1PH 220V, Output 3PH 220V 7.0A, 1.5kW |
| 07 | Bộ chuyển đổi PT100 | Loại 4-20mA, Range 0-150°C, nguồn 24VDC | |
| 08 | Bộ chuyển đổi PT100 | Loại 0-10V, Range 0-200°C, nguồn 24VDC | Có 2 loại PT100 converter khác nhau — cần chốt dùng loại nào |
| 09 | SPD (chống sét) | CITEL DSH63 (Coordination Inductor, 63A/15µH) | Hãng Pháp |
| 10-11 | HMI | **Weintek eMT3070B**, S/N 1712100899 | ✅ Model + số serial xác nhận khớp chính xác ghi chú cũ |
| 12 | SPD | Schneider Easy9 EZ9L33620, Type 2 | |
| 13 | Coordination Inductor | CITEL DSH63 (ảnh góc khác) | |
| 14 | Surge Arrester | Schneider Electric, IEC/EN 61643-11 | Có vẻ là bộ SPD thứ 2 khác biệt — cần xác nhận vai trò |
| 15, 22 | Contactor + rơ-le nhiệt | (góc chụp không rõ hãng — đối chiếu với #19-21) | |
| 16-17 | Biến áp điều khiển | CHINT NDK-250, In 415/380/220V, Out 220/110/48/36/24/12V | |
| 18 | Bộ nguồn 24VDC | MEAN WELL LRS-200-24 | |
| 19, 21 | Contactor | Mitsubishi S-T12, cuộn hút 200-240V | |
| 20 | Rơ-le nhiệt bảo vệ quá tải | Mitsubishi Electric Thermal Overload Relay | Có nút Push to Reset (Hand/Auto) |
| 23 | E-Stop | CHINT NP2 + khối tiếp điểm BE102.1-.2 (1 NC) | Khớp mô tả sự cố tự chạy lại đã trao đổi — chỉ 1 NC, chưa có tiếp điểm phụ báo PLC |
| 24-25 | Động cơ | VTC Elec. & Mach Co., YSTP, 0.75kW, 4 cực, 1450/1710rpm, dòng 3.7/1.8A và 3.2/1.5A | |
| 26 | Hộp đấu dây động cơ | **Δ 220V (Lower voltage) / Y 380V (Higher voltage)** | ✅ Giải quyết dứt điểm câu hỏi đấu Δ/Y còn treo trước đó |

## Còn thiếu ảnh
- Đồng hồ đo Selec MFM383A-C (đã có datasheet chính hãng, chưa có ảnh vật lý)
- Đèn báo, còi báo, nút Start/Stop (nếu đã mua)
- Tủ điện, cầu đấu, DIN rail, dây/cáp

*Cập nhật 2026-08-18.*
