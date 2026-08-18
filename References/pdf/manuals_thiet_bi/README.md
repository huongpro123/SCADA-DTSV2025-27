# Manual thiết bị chính hãng

## Đã có

| File | Thiết bị | Nguồn | Trạng thái xác nhận |
|---|---|---|---|
| `Siemens_S7-1200_System_Manual.pdf` | PLC CPU 1211C | support.industry.siemens.com (bạn tự tải, script tự động bị chặn bot) | ✅ Model xác nhận qua ảnh tem máy thật (`04_Hardware/01_hinh_anh_thiet_bi/01_...`) |
| `Wecon_VNZ100_User_Manual_V3.5.pdf` (41 trang) | Biến tần | ftp.we-con.com.cn (chính hãng) | ✅ **Model VNZ100-1R5G-2 đã xác nhận qua ảnh tem máy thật 2026-08-18** — giải quyết dứt điểm nghi vấn VNZ100 vs VNZ200 |
| `Selec_MFM383A-C_Datasheet.pdf` (2 trang) | Đồng hồ đo đa năng | tme.eu (nhà phân phối chính hãng) | Model đã xác nhận (Thuyết minh mục 11.1.1) — còn thiếu ảnh tem máy thật |
| `KHONG_DUNG_INVT_GD35_manual_SAI_thiet_bi.pdf` | ❌ KHÔNG dùng | — | Manual biến tần **INVT GD35, khác hãng hoàn toàn** với Wecon VNZ100 thật đang dùng. Giữ lại chỉ để đối chiếu lịch sử lỗi cũ — đặt tên rõ để không ai nhầm dùng nhầm file này khi thiết kế đấu nối |

## Đã xác nhận qua ảnh tem máy thật (2026-08-18) — xem chi tiết đầy đủ tại `04_Hardware/01_hinh_anh_thiet_bi/README.md`
Không cần manual PDF riêng (thiết bị đơn giản, thông số đủ đọc từ tem máy): CHINT NDK-250 (biến áp
điều khiển), CHINT NP2+BE102 (E-Stop), CHINT NXB-63 (Aptomat 3 loại dòng cắt), CNAOM HH52P (relay
trung gian), Mitsubishi S-T12 + rơ-le nhiệt (contactor), MEAN WELL LRS-200-24 (nguồn 24VDC), CITEL
DSH63 (SPD), Schneider Easy9 EZ9L33620 (SPD), Weintek eMT3070B (HMI — model + serial khớp chính xác
ghi chú cũ), 2 loại bộ chuyển đổi PT100 (4-20mA và 0-10V), động cơ VTC Elec (kèm xác nhận đấu
Δ220V/Y380V).

## Còn thiếu hoàn toàn
- Đồng hồ đo Selec MFM383A-C — chưa có ảnh vật lý tem máy
- Đèn báo, còi báo, nút Start/Stop — chưa rõ đã mua hay chưa

*Cập nhật lần cuối: 2026-08-18.*
