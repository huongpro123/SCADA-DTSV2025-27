# PROJECT STATUS

*File này là nguồn theo dõi tiến độ "sống" (living tracker) — cập nhật mỗi khi hoàn thành
một mốc. `RESEARCH_PROTOCOL.md` mục 11 chỉ giữ snapshot tại thời điểm duyệt đề cương, không
sửa lại mục đó; mọi cập nhật tiến độ thực tế nằm ở đây.*

## Tổng quan theo Phase

| Phase | Tên | Trạng thái | Ngày bắt đầu | Ngày hoàn thành | Ghi chú |
|---|---|---|---|---|---|
| 0 | Research Protocol | ✅ Approved (chính thức) | 2026-08-07 | 2026-08-07 | v1.0 — đề tài đã được duyệt; xác nhận lưu tại `01_Research_Protocol/02_Bien_ban_duyet/` |
| 1 | Literature Review | 🟡 Đang thực hiện (~99%) | 2026-08-07 | | Bước 1-9 `LITERATURE_RULES.md` xong, 15/15 nguồn đủ PDF + số trang đầy đủ. Bản thảo Chương 1 (bản 7) tại `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx`. Còn lại duy nhất: trình GVHD duyệt lần cuối (task đang chờ bạn gửi). |
| 2 | System Design | 🟡 Đang thực hiện (~80%) | 2026-08-08 | | Đã xong: sơ đồ kết nối hệ thống (`03_System_Design/So_do_ket_noi_he_thong.svg`), Danh mục thiết bị đầy đủ 22 hạng mục có ảnh xác minh (`Danh_muc_thiet_bi_can_xac_dinh.xlsx`), Chương 2 bản 6 (đã tách lý thuyết/lựa chọn thiết bị). Còn thiếu: bản vẽ Inventor/AutoCAD Electrical (đã hoãn, chưa gấp), tiêu chí đánh giá định lượng đã soạn xong (`06_Experiment/Tieu_chi_danh_gia_dinh_luong.md`) chờ GVHD xác nhận. |
| 3 | Hardware Selection | 🟡 Đang thực hiện (~85%) | 2026-08-08 | | 12/13 hạng mục chính đã xác nhận vật lý qua ảnh tem máy (PLC, HMI eMT3070B, VFD VNZ100-1R5G-2, contactor, rơ-le nhiệt, Aptomat, nguồn 24VDC, biến áp, relay trung gian, động cơ, đồng hồ Selec MFM383A-C, CB 1241). Còn thiếu: 3 CT (biến dòng) — bắt buộc chưa mua; nút dừng khẩn cấp/đèn báo/còi — đã chốt mua, chưa có model cụ thể. |
| 4 | Simulation | ⬜ Not Started | | | |
| 5 | Implementation | ⬜ Not Started | | | |
| 6 | Experiment | ⬜ Not Started | | | |
| 7 | Evaluation | ⬜ Not Started | | | |
| 8 | Thesis Writing | ⬜ Not Started | | | |

Trạng thái dùng: ⬜ Chưa bắt đầu · 🟡 Đang thực hiện · ✅ Hoàn thành · ⛔ Tạm dừng/Vướng mắc

## Quy trình hành chính (theo QT_Thuchien detaiNCKHSV.pdf — quy trình thật của trường)
*Đây là quy trình **thủ tục hành chính** (đăng ký → duyệt → hợp đồng → nghiệm thu → thanh
toán) của trường, khác với bảng "8-phase" ở trên (bảng 8-phase là quy trình **nghiên cứu học
thuật nội bộ**, nằm gọn trong bước "Triển khai thực hiện" của quy trình hành chính này).*

| Bước | Đơn vị thực hiện | Trạng thái | Ghi chú |
|---|---|---|---|
| 1. Thông báo đăng ký | P.QLKHCN-ĐMST-HTQT | ✅ Đã xác nhận | |
| 2. Xây dựng thuyết minh (Mẫu SV01, SV02) | Chủ nhiệm đề tài | ✅ Đã xác nhận | File thuyết minh có trong `00_Trao_doi_GVHD/` |
| 3. Duyệt đề xuất cấp khoa | Hội đồng KH&ĐT Khoa | ✅ Đã xác nhận | |
| 4. Khoa gửi danh sách về Phòng | Hội đồng KH&ĐT Khoa | ✅ Đã xác nhận | |
| 5. Duyệt đề xuất và kinh phí cấp Trường | Hội đồng KH&ĐT Trường | ✅ Đã xác nhận | |
| 6. Thẩm định thuyết minh (Mẫu SV03) | Tổ thẩm định | ✅ Đã xác nhận | |
| 7. Ra Quyết định giao và ký hợp đồng (Mẫu SV11) | P.QLKHCN-ĐMST-HTQT | ✅ Đã xác nhận | Mã đề tài: **DTSV2025-27** |
| 8. **Triển khai thực hiện** (Mẫu SV05 nếu điều chỉnh) | Chủ nhiệm đề tài | 🟡 Đang thực hiện | ← **Đang ở đây** — dùng bảng 8-phase bên trên để theo dõi chi tiết |
| 9. Gia hạn (nếu có, tối đa 1 lần, ≤6 tháng) | Chủ nhiệm đề tài | ✅ Đã xác nhận | Đã xin gia hạn 6 tháng (đã dùng hết mức tối đa cho phép). Hạn nộp mới: **tháng 01/2027**. Có thể nộp sớm hơn ngay khi hoàn thành, không cần chờ đúng hạn. |
| 10. Nộp hồ sơ nghiệm thu (Mẫu SV04, SV06) | Chủ nhiệm đề tài | ⬜ Chưa tới | |
| 11. Nghiệm thu đề tài (Mẫu SV07, SV08, SV09) | Hội đồng nghiệm thu | ⬜ Chưa tới | |
| 12. Nộp hồ sơ sau nghiệm thu (Mẫu SV04, SV10) | Chủ nhiệm đề tài | ⬜ Chưa tới | Trong 50 ngày kể từ ngày có QĐ HĐNT |
| 13. Ra QĐ công nhận đề tài | P.QLKHCN-ĐMST-HTQT | ⬜ Chưa tới | |
| 14. Hoàn tất thanh toán kinh phí | Chủ nhiệm đề tài / P.KH-TC | ⬜ Chưa tới | |

*Các bước 1–7 đã được bạn xác nhận hoàn tất (2026-08-07) — chuyển từ "suy luận" sang "sự kiện
đã xác minh".*

## Tổng quan rút gọn (milestone view)
Cách nhìn đơn giản hơn, đối chiếu với bảng 8-phase ở trên:

| Nhóm | Nội dung | Tương ứng phase |
|---|---|---|
| ✔ Completed | Proposal, Research Question, Objectives | Phase 0 |
| 🟡 Current | Literature Review (chờ GVHD duyệt), System Design + Hardware Selection (đang song song) | Phase 1–3 |
| ⬜ Next | Simulation | Phase 4 |
| ⬜ Remaining | Implementation, Experiment, Evaluation, Thesis Writing | Phase 5–8 |

⚠️ *Lưu ý:* nhóm "Remaining" ở đây gộp chung Hardware Selection, Simulation, Implementation,
Evaluation vào "Experiment", và gộp Thesis Writing vào "Discussion/Conclusion" cho gọn — bảng
8-phase phía trên vẫn là nguồn theo dõi chi tiết, đầy đủ. Nếu bạn muốn dùng đúng 7 mục
(Proposal, Literature Review, System Design, Experiment, Discussion, Conclusion — bỏ chi tiết
8-phase), báo mình đổi cấu trúc bảng chính luôn cho nhất quán.

## Success Criteria (đối chiếu mục 10 Research Protocol)

| Tiêu chí | Đạt? |
|---|---|
| PLC giao tiếp được với HMI | ⬜ |
| PLC giao tiếp được với WinCC | ⬜ |
| VFD hoạt động đúng | ⬜ |
| Động cơ điều khiển được | ⬜ |
| Dữ liệu giám sát hiển thị chính xác | ⬜ |
| Chức năng cảnh báo hoạt động đúng | ⬜ |
| Dữ liệu lịch sử ghi nhận được | ⬜ |

## Việc đang làm (cập nhật liên tục)
- **[2026-08-09] Phase 2-3 (System Design/Hardware Selection) tiến triển mạnh, chưa xong hẳn.**
  Đã xác nhận vật lý 12 hạng mục thiết bị qua ảnh tem máy, sửa lỗi quan trọng (biến tần thật là
  VNZ100-1R5G-2, không phải VNZ200 như ghi nhầm trước đó), giải quyết mâu thuẫn model đồng hồ đo
  (chốt Selec MFM383A-C). Tách lại Chương 2 theo góp ý của bạn: mục 2.3 chỉ còn lý thuyết thuần
  túy, mục 2.4 mới gộp toàn bộ quyết định thiết bị cụ thể. Soạn thêm bộ tiêu chí đánh giá định
  lượng cho 7 Success Criteria (`06_Experiment/Tieu_chi_danh_gia_dinh_luong.md`) vì bản gốc toàn
  viết định tính, không đo lường được — cần GVHD xác nhận.
  **Còn CHƯA XONG (chặn việc coi Phase 2-3 là hoàn tất):**
  1. Mua 3 CT (biến dòng) — bắt buộc, chưa có.
  2. Chốt model cụ thể nút dừng khẩn cấp + đèn báo + còi báo (đã quyết định mua, chưa chọn hãng).
  3. Lấy thông số kỹ thuật thật của động cơ (công suất, dòng định mức) — đã xác nhận có mua nhưng
     chưa có tem máy/thông số, cần để chọn đúng tỷ số CT.
  4. Gửi nội dung trao đổi GVHD đã gộp (`01_Research_Protocol/00_Trao_doi_GVHD/`) — soạn xong,
     chưa gửi.
  5. Bản vẽ Inventor/AutoCAD Electrical — đã bàn và hoãn lại (chưa gấp), không chặn tiến độ hiện
     tại nhưng cần nhớ quay lại trước Chương 3.
- **[2026-08-07] Literature Matrix hoàn tất và đã dọn dẹp.** 15/15 nguồn đã xác minh đủ PDF,
  Coverage đạt cả 4 RQ và tổng (RQ1=7, RQ2=7, RQ3=6, RQ4=4, Tổng=15). Đã tách 5 nguồn quá 10
  năm sang `References/pdf/_archive_loai_qua10nam/` (không xóa, chỉ lưu trữ, không tính vào
  Matrix), và tách 5 nguồn CORE liên quan mạnh nhất sang `References/pdf/_core_de_tai/` để ưu
  tiên đọc kỹ trước khi vào Phase 2.
- **Còn CHƯA HOÀN THIỆN (chặn việc coi Phase 1 là xong):**
  1. Rà lại 3 chỗ trong Chương 1 còn đánh dấu "tr. cần bổ sung" — Manafov [8], Nguyễn Chí Ngôn
     [10], Kumar [15] — cần tự tra số trang chính xác trong kỷ yếu/tạp chí gốc.
  2. Gửi `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx` (bản 2, đã áp quy tắc ≤10 năm) cho GVHD
     duyệt lần cuối — CHƯA gửi, chỉ mới tự hoàn thiện nội bộ.
  3. Chuẩn hóa định dạng cột "Trạng thái xác minh" cho STT 2, 3, 6 trong Matrix (đang ghi tạm
     thông tin số trang thay vì cụm chuẩn "Đã xác minh, đã có PDF") — không sai dữ liệu, chỉ
     chưa đồng nhất định dạng, có thể để sau.
  4. Đọc kỹ hơn phần "Phương pháp đánh giá" cho STT 1 (Malla), 10 (Alcayde), 11 (Kaluz) — đang
     đánh dấu vàng "cần đọc kỹ hơn toàn văn", chưa xác nhận chi tiết phương pháp.

## Vướng mắc / Rủi ro
- **[2026-08-07] Mốc thời gian còn lại.** Đề tài đăng ký 12 tháng (10/2025–10/2026 theo Thuyết
  minh mục 5), đã gia hạn tối đa cho phép (6 tháng, không còn quyền gia hạn lần 2) — hạn mới
  tháng 01/2027, có thể nộp sớm hơn khi hoàn thành. Còn khoảng 5 tháng cho 7 phase còn lại
  (System Design → Thesis Writing). Bạn đã cân nhắc và chủ động chọn nhịp độ làm từ từ, tự tin
  kịp tiến độ — ghi nhận ở đây chỉ để tham khảo mốc ngày, không phải cảnh báo. Lý do tự tin:
  bạn đã làm Đồ án 1 liên quan trực tiếp tới PLC S7-1200 và HMI trước đây, nên có thể rút ngắn
  đáng kể phần cứng/thiết kế cơ bản ở Phase 2-3 (System Design, Hardware Selection) nhờ tái sử
  dụng kinh nghiệm/tài liệu đã có — chưa xác nhận file Đồ án 1 có sẵn trong máy hay không, khi
  nào cần dùng lại thì đưa vào `03_System_Design/` hoặc `04_Hardware/` để mình đối chiếu.
- **[2026-08-07] Rủi ro liêm chính trích dẫn trong Thuyết minh đã duyệt (DTSV2025-27).**
  Đối chiếu trực tiếp file đã nộp (`00_Trao_doi_GVHD/DTSV2025-27 TM_NCHuong...pdf`, trang 2,
  mục 6): danh mục "Tài liệu tham khảo" chỉ có 4 nguồn đánh số [1]-[4] (Khoa và cộng sự 2022;
  Phạm & Phạm 2015; Gomboc 2014; Gedzurs 2016), nhưng phần 6.2 còn trích dẫn trong bài 3 tác
  giả **không có trong danh mục**: Manafov & Huseynov (2024), Malla & KC (2023), Orhanen
  (2021). Chủ nhiệm đề tài xác nhận chưa tự đọc/xác minh nguồn nào trong số này trước khi
  nộp. Cần xác minh lại toàn bộ 7 nguồn (4 có số + 3 thiếu số) trước khi dùng làm nền cho
  Chương 1 báo cáo tổng kết — xem hành động cụ thể ở `LITERATURE_RULES.md`.
  *Suy luận, chưa xác minh:* có thể một số nguồn là thật nhưng ghi thiếu thông tin, cũng có
  thể một số không tồn tại như mô tả — không kết luận trước khi tự tra cứu.
  **[2026-08-07] Cập nhật:** cả 3 tác giả từng thiếu số trong danh mục (Manafov & Huseynov,
  Malla & KC, Orhanen) nay đã xác minh là nguồn có thật, có DOI/nguồn xác định, đã đưa đúng
  vào `References/literature_matrix.xlsx` và Chương 1 mới. Tuy nhiên **bản Thuyết minh đã nộp/
  duyệt chính thức (DTSV2025-27) vẫn còn nguyên lỗi này trên giấy** — mình chưa sửa vì đó là
  văn bản đã qua hội đồng duyệt. Câu hỏi còn mở: có cần làm Mẫu SV05 (điều chỉnh) để chính
  thức sửa danh mục tham khảo trong hồ sơ đã duyệt hay không — nên hỏi trực tiếp GVHD.
  **[2026-08-07] Phát hiện thêm (khi đối chiếu lại trang 2 Thuyết minh):** tài liệu [1] trong
  danh mục tham khảo của Thuyết minh ghi "Khoa, Đ.H.Đ., Thanh, S.H., & Ngôn, N.C. — Nghiên cứu
  điều khiển động cơ không đồng bộ ba pha bằng biến tần và PLC, Tạp chí Khoa học & Công nghệ
  Việt Nam, 2022" — nhưng bài thật đã xác minh của đúng 3 tác giả này (DOI
  10.34238/tnu-jst.5358) có tiêu đề và tạp chí khác hẳn ("Điều khiển thông minh động cơ không
  đồng bộ 3 pha dựa trên mạng nơ-ron mờ hồi quy", TNU Journal of Science and Technology). Tìm
  không ra bài nào khớp đúng tên/tạp chí như Thuyết minh mô tả. *Suy luận, chưa kết luận chắc:*
  khả năng tên tài liệu/tạp chí trong Thuyết minh gốc bị ghi sai — cùng mẫu vấn đề với 3 tác
  giả thiếu ở trên. Nên hỏi GVHD cùng lúc với câu hỏi về Mẫu SV05.
  **[2026-08-07] MỞ RỘNG PHÁT HIỆN — đã đọc lại toàn bộ trang 2-3 (mục 6.1-6.2) của Thuyết
  minh:** danh mục tham khảo đầy đủ của Thuyết minh có **7 tài liệu khoa học** (không phải 4
  như ghi nhận ban đầu): [1] Khoa/Thanh/Ngôn 2022, [2] Phạm & Phạm 2015, [3] Gomboc 2014, [4]
  Gedzurs 2016, [5] Orhanen 2021, [6] Manafov & Huseynov 2024, [7] Malla & KC 2023 (cộng [8][9]
  là 2 tài liệu hãng Siemens/Selec, không phải bài báo). Đã tra cứu độc lập cả 7 qua WebSearch
  và CrossRef API — KHÔNG tài liệu nào xác minh được đúng như mô tả.
  **[2026-08-07] CẬP NHẬT — bạn đã bổ sung 7 file PDF thật vào `References/file mới/`.** Đối
  chiếu xong: **5/7 trường hợp** (Khoa/Thanh/Ngôn, Manafov & Huseynov, Malla & KC, Gedzurs,
  Orhanen) hóa ra CÓ file PDF thật, và tác giả trùng tên đúng như Thuyết minh ghi — nhưng bản
  thân file thật lại có TIÊU ĐỀ và TẠP CHÍ khác hẳn những gì Thuyết minh mô tả (VD: Orhanen
  thật là luận văn Thạc sĩ "Thermal overload protection...", không phải bài báo "Predictive
  maintenance..." như Thuyết minh ghi). Kết luận: đây không phải 7 tài liệu bịa hoàn toàn từ
  đầu, mà nhiều khả năng là **mô tả trích dẫn (tiêu đề/tạp chí) bị viết sai/garbled** so với
  file nguồn thật khi soạn Thuyết minh — vẫn là lỗi liêm chính trích dẫn cần báo GVHD, nhưng
  bản chất nhẹ hơn "bịa đặt hoàn toàn". Còn **2/7 vẫn hoàn toàn chưa tìm ra**: [2] Phạm & Phạm
  2015 ("Ứng dụng PLC S7-1200...", Hội thảo Tự động hóa toàn quốc) và [3] Gomboc 2014
  ("Industrial communication standards...", IEEE Industrial Informatics Conference) — không có
  file, không tra được qua WebSearch/CrossRef. Chương 1 bản 4
  (`08_Thesis/Chuong1_Tong_quan_tai_lieu.docx`) đã viết lại theo hướng: GIỮ NGUYÊN vấn đề/mục
  tiêu/hai khoảng trống đã nêu ở Thuyết minh mục 6.2 (không đổi đề tài), dùng đúng 15 tài liệu
  đã xác minh (trong đó nhiều tài liệu chính là các file thật vừa đối chiếu ở đây, chỉ khác là
  đã sửa đúng tiêu đề/tạp chí thật).

---
*Cập nhật lần cuối: 2026-08-07*
