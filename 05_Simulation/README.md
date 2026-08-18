# 05_Simulation

Code/project TIA Portal, PLC source (SCL/ladder), file mô phỏng.

## `project_tia_portal/` — project TIA Portal chính thức
Project `aovathat.ap20`, chủ nhiệm xác nhận 2026-08-18 đây đúng là project TIA Portal đang dùng cho
đề tài DTSV2025-27 (không phải Đồ án 1 hay project nào khác trong số nhiều bản trùng tên từng thấy
tại `D:\project tia portal\`). File nhị phân, không đọc/kiểm tra được nội dung logic bằng công cụ
text — chỉ xác nhận qua lời chủ nhiệm, tự mở bằng TIA Portal để rà lại khi cần.

## Còn thiếu
- Code xử lý E-Stop hiện tại (đoạn logic Cmd_Run/HH52P) — bạn đã đồng ý gửi để rà soát lỗi tự chạy
  lại khi nhả E-Stop (xem `PROJECT_STATUS.md` mục Rủi ro). Có thể export trực tiếp từ project trong
  `project_tia_portal/` (TIA Portal → chuột phải khối logic liên quan → Export nguồn ngoài dạng .scl)
  thay vì gửi riêng, nếu tiện hơn.

*Cập nhật 2026-08-18.*
