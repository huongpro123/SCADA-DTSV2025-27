# FILE_STRUCTURE.md — Quy định đặt tên và tổ chức thư mục

*Áp dụng cho file MỚI từ 2026-08-18 trở đi. Không tự ý di chuyển/đổi tên file cũ đang có sẵn trong
repo — nếu cần dọn lại cấu trúc cũ, phải bàn trước và làm thành một commit riêng, rõ ràng.*

## Cấu trúc thư mục mục tiêu (cho file mới)

```
NCKH_Sinh_Viên/                        (gốc repo git)
├── CLAUDE.md, PROJECT_GUIDE.md, RESEARCH_PROTOCOL.md,
│   PROJECT_STATUS.md, CITATION_POLICY.md, FILE_STRUCTURE.md,
│   WRITING_GUIDELINES.md, CHANGELOG.md      ← file quy chuẩn dùng chung, luôn ở gốc
├── DTSV2025-27 TM_NCHuong_ThS.LQKhuong hd.pdf   ← Thuyết minh gốc đã duyệt, KHÔNG sửa
├── NCKH_Van_ban_trong_truong/           ← văn bản quy định chính thức của trường (đã có)
├── 01_Research_Protocol/
│   └── 00_Trao_doi_GVHD/               ← biên bản duyệt, trao đổi GVHD (từng buổi 1 file)
├── 03_System_Design/                    ← sơ đồ hệ thống, sơ đồ đấu nối (đã có 2 file SVG)
├── 04_Hardware/
│   └── 01_hinh_anh_thiet_bi/           ← ảnh tem máy thiết bị thật
├── 05_Simulation/                       ← code TIA Portal, PLC source, project mô phỏng
├── 06_Experiment/                       ← tiêu chí đánh giá định lượng, dữ liệu đo thực nghiệm
├── 08_Thesis/                           ← các chương báo cáo/khóa luận (bản chính thức)
├── References/
│   ├── pdf/                            ← toàn văn PDF các tài liệu tham khảo
│   └── literature_matrix.xlsx
└── NCKH_Sinh_Viên/                      ← thư mục cũ (bản thảo trước khi dựng lại cấu trúc này) — giữ nguyên để tham khảo
```

## Vì sao đánh số thư mục theo phase (01, 03, 04...)
Số thứ tự khớp với thứ tự các phase làm việc trong `PROJECT_STATUS.md`. Bỏ trống 02, 07 có chủ đích
(dự phòng nếu sau này cần chèn phase mới mà không phải đổi số toàn bộ thư mục sau nó).

## Quy tắc đặt tên file mới
- **Không dấu cách, không dấu tiếng Việt trong tên file** khi có thể — dùng `Tieng_Viet_Khong_Dau`
  hoặc `snake_case`. File cũ đã có dấu cách/dấu tiếng Việt (VD: `luoc khao tai lieu.xlsx`) giữ
  nguyên, không đổi tên chỉ vì không đúng quy tắc mới.
- Ảnh thiết bị: đặt tên mô tả đúng thiết bị, không giữ tên timestamp máy ảnh (VD:
  `01_PLC_S71200.jpg`, không phải `IMG_20260101_120000.jpg`)
- Bản thảo báo cáo: giữ số phiên bản trong tên file nếu chưa dùng git để track version (VD:
  `Chuong1_Tong_quan_tai_lieu_v3.docx`) — nếu đã commit git đều đặn, không cần đánh version trong
  tên file nữa vì git tự giữ lịch sử, tránh trùng lặp 2 cơ chế versioning
- Gói file gửi GVHD: đóng trong thư mục con `Goi_gui_YYYY-MM-DD/` dưới
  `01_Research_Protocol/00_Trao_doi_GVHD/`, không lẫn với bản gốc ở `08_Thesis/`

## Thư mục hiện có nhưng chưa dùng quy ước trên
- `NCKH_Sinh_Viên/NCKH_Sinh_Viên/` — bản thảo Chương 1-2, danh mục thiết bị, literature matrix cũ.
  Khi làm việc tiếp với các file này, cân nhắc di chuyển vào đúng cấu trúc mục tiêu ở trên (`08_Thesis/`,
  `References/`) — nhưng đây là việc cần làm **có chủ đích, thành 1 commit riêng**, không lẫn vào
  commit khác.
- `NCKH_khoi_phuc/` — log/ghi chú cũ dựng lại từ trí nhớ hội thoại, không phải cấu trúc chính thức,
  chỉ giữ tham khảo.

*Cập nhật lần cuối: 2026-08-18*
