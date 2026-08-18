# CHANGELOG

Nhật ký thay đổi của dự án. Mỗi mục theo ngày, phân nhóm Added/Modified/Updated/Created.

## 2026-08-15 (bổ sung 50 — chốt động cơ thật, khớp VFD)
- Ảnh tem máy động cơ đã lấy từ phòng lab (`04_Hardware/01_hinh_anh_thiet_bi/dong co.jpg`, tem bẩn/gỉ
  nhưng đọc được): VTC Elec. & Mach Co., Ltd., series YSTP, 0.75kW, 4 cực, 1450rpm@50Hz/1710rpm@60Hz,
  dòng 3.7/1.8A (50Hz) và 3.2/1.5A (60Hz), khung 80. Suy luận (không đọc trực tiếp được số volt do tem
  gỉ, dựa vào cách ghi dòng dạng cặp + sơ đồ đấu Y/Δ in trên tem — chưa xác minh 100%): nhiều khả năng
  220V(Δ)/380V(Y) — nếu đúng, khớp tốt với VFD VNZ100 (ra 220V, dòng 3.7A << 7.0A tối đa VFD), công
  suất/số cực đều nằm trong tiêu chí đã chốt trước đó. CẦN làm trước khi đấu điện thật: lau tem đọc lại
  số volt cho chắc, mở hộp đấu dây xem tem sơ đồ Y/Δ bên trong để đấu đúng Δ ở 220V.
- Vậy cả 3 việc chờ trước đó (nameplate động cơ, E-stop, sơ đồ đấu nối) đã xong. Bước tiếp theo là đấu
  dây thật theo `So_do_dau_noi_dien_chi_tiet.svg` (bổ sung 49), sau khi giải quyết các điểm còn treo
  trong ghi chú của sơ đồ đó (điện áp cuộn hút HH52P, đèn báo/còi báo).

## 2026-08-15 (bổ sung 49 — sơ đồ đấu nối điện chi tiết + chốt E-stop + đổi tên ảnh thiết bị)
- Xác nhận mua E-stop: CHINT NP2 (đầu nấm đỏ tự giữ) + khối tiếp điểm NP2-BE102 (1 NC, AC-15 220V/4.5A).
  Cập nhật `Danh_muc_thiet_bi_can_xac_dinh.xlsx` mục 13 coi như đã có trong tay.
- Đổi tên 23 file ảnh trong `04_Hardware/01_hinh_anh_thiet_bi/` từ tên timestamp khó đọc sang tên mô tả
  đúng thiết bị (01_PLC... tới 23_Nut_dung_khan...), theo quy tắc đặt tên `FILE_STRUCTURE.md`.
- Tạo `03_System_Design/So_do_dau_noi_dien_chi_tiet.svg` — sơ đồ nguyên lý mạch động lực (CB tổng →
  contactor S-T12 → rơ-le nhiệt → VFD VNZ100 → động cơ) và mạch điều khiển cuộn hút contactor (E-stop
  → NC rơ-le nhiệt → relay HH52P, chuỗi an toàn cứng độc lập PLC), cùng tín hiệu PLC↔VFD/PT100. Ghi chú
  kỹ thuật quan trọng trong sơ đồ: rơ-le nhiệt đặt đầu VÀO VFD (không đặt đầu ra vì dòng PWM đo sai),
  contactor 3 cực chỉ dùng 2 cực cho tải 1 pha, CHƯA xác nhận điện áp cuộn hút relay HH52P (cần đo/tra
  trước khi đấu vào PLC), E-stop hiện chỉ 1 khối NC (ưu tiên cắt cứng, chưa có tiếp điểm phụ báo PLC).
- Còn lại trước khi đấu điện thật: nameplate động cơ thật (đã chốt tiêu chí chọn: Δ220V/Y380V, ≤1.5kW,
  dòng Δ ≤6A, 4 cực — chờ lấy máy từ phòng lab), đèn báo/còi báo (đã quyết định mua, chưa chọn model).

## 2026-08-15 (bổ sung 48 — sửa lỗi Gateway crash khi khởi động cùng Windows)
- Lỗi: `python_gateway.py` bị `TimeoutError` (asyncua) và crash toàn bộ tiến trình mỗi lần Task
  Scheduler tự chạy `start_all_watchdog.bat` lúc đăng nhập Windows — do mạng/PLC chưa kịp sẵn sàng
  đúng thời điểm đó. PLC/mạng vẫn bình thường khi kiểm tra thủ công sau đó — xác nhận đây là race
  condition lúc khởi động, không phải lỗi cấu hình OPC UA/NodeId.
- Gốc lỗi thật: `main_loop()` gọi `plc.connect()` lần đầu KHÔNG có try/except (logic tự kết nối lại
  chỉ tồn tại bên trong vòng lặp polling, áp dụng khi mất kết nối SAU KHI đã chạy, không áp dụng cho
  lần đầu). Sửa: bọc lần kết nối đầu trong vòng lặp tự thử lại mỗi 5 giây, không giới hạn số lần, tới
  khi thành công mới vào vòng lặp chính — không cần dựa vào watchdog bên ngoài khởi động lại cả tiến
  trình Python mỗi 5 giây nữa cho riêng trường hợp này.

## 2026-08-14 (bổ sung 47 — ghi chú kỹ thuật: phụ thuộc laptop + phương án bỏ laptop, CHƯA triển khai)
- **Hiện trạng:** `python_gateway.py` + `telegram_bot.py` chạy trên máy tính (laptop) — nếu tắt/rút máy
  này, lớp SCADA phần mềm (đọc OPC UA, ghi lịch sử `plant.db`, cảnh báo + lệnh qua Telegram) dừng hoàn
  toàn. Lớp PLC (điều khiển động cơ, an toàn, contactor/rơ-le nhiệt/E-stop phần cứng) KHÔNG phụ thuộc
  laptop, vẫn chạy độc lập bình thường. HMI Weintek (nối thẳng PLC qua Ethernet) cũng không phụ thuộc.
- **Phương án bỏ laptop (khuyến nghị, chưa làm):** thay laptop bằng máy tính nhỏ chạy 24/7 kiểu
  Raspberry Pi (đặt cạnh/trong tủ điện) — copy nguyên `mo_phong/04_Gateway/` và `mo_phong/05_Telegram_Bot/`
  sang chạy trên đó, cùng cơ chế watchdog/Task Scheduler (đổi tương đương bằng systemd trên Linux) đã
  làm cho laptop. Đây là mô hình chuẩn công nghiệp — SCADA luôn cần 1 "server" chạy liên tục, không
  phải máy ai đang dùng hàng ngày.
- **Lớp cảnh báo dự phòng (khuyến nghị, chưa làm):** S7-1200 firmware mới có khối gửi Email trực tiếp
  từ PLC (không cần PC/Gateway) — có thể dùng làm kênh cảnh báo dự phòng khi Gateway/Pi bị sập, không
  thay được điều khiển 2 chiều qua Telegram nhưng thêm 1 lớp an toàn thông báo độc lập.
- Không tự ý làm — cần bạn quyết định có đưa vào phạm vi đề tài hay chỉ để tham khảo triển khai thực tế
  sau khi bảo vệ.

## 2026-08-14 (bổ sung 46 — kiến trúc OPC UA/Telegram đầy đủ chạy trên CPU thật; đối chiếu tồn kho thiết bị)
- Tạo `05_Simulation/PLC_Real_Motor_Source.scl` (external source SCL) — build 6 DB thật (DB_Motor,
  DB_Inverter, DB_PLC_Status, DB_FaultSimulation, DB_Alarm, DB_Thresholds) + 6 FC (FC10-FC60) lên CPU
  S7-1211C thật, chuyển thể từ `mo_phong/02_PLC/PLC_Program_Source.scl`, cắt phần chỉ dành cho Factory
  I/O (Btn_Start/Q_Conveyor1/DB_SeparatingStation/FC70). FC10 dùng Option C (mô phỏng ramp phần mềm),
  CHƯA đọc cảm biến thật. Compile/download/publish OPC UA qua ServerInterface_1 thành công, đọc được
  qua UaExpert (NodeId dạng số ns=4;i=X, khác S7-1500 dạng chuỗi).
- Theo yêu cầu người dùng ("phát triển lên từ mo_phong, không tạo lại từ đầu"): chuyển từ bản Gateway
  rút gọn tự viết (`gateway_nckh.py`) sang dùng trực tiếp kiến trúc đầy đủ `mo_phong/04_Gateway/
  python_gateway.py` + `mo_phong/05_Telegram_Bot/telegram_bot.py` + `plant.db` (SQLite, đã có sẵn,
  UserAccount đã có chat_id Admin từ trước). Cập nhật `mo_phong/04_Gateway/config.yaml` — thay toàn bộ
  NodeId ảo S7-1500 (`ns=3;s="DB_x"."Var"`) bằng NodeId thật CPU 1211C (`ns=4;i=X`) lấy từ UaExpert.
  Sửa `mo_phong/start_all.bat` trỏ về bản trong `NCKH_Sinh_Vien\mo_phong` thay vì `D:\mo_phong` gốc.
  Test end-to-end thành công trên máy thật: `/start`, `/status`, `/run` (bật Cmd_Run thật, Motor
  chuyển RUN, giá trị ramp đúng logic FC10), heartbeat tự động — toàn bộ qua Telegram thật.
- Đối chiếu 22 ảnh tem máy thiết bị (`04_Hardware/01_hinh_anh_thiet_bi/`) với
  `03_System_Design/Danh_muc_thiet_bi_can_xac_dinh.xlsx` (đã có sẵn từ 2026-08-09) — xác nhận hầu hết
  quyết định kỹ thuật đã chốt từ trước (PT100 dùng loại 0-10V, contactor S-T12 + rơ-le nhiệt, biến áp
  NDK-250, relay HH52P, SPD quyết định không dùng). Ba điểm còn chặn việc đấu điện/chạy thử động cơ
  thật: (1) chưa có thông số nameplate động cơ thật (cần xác nhận tương thích với VFD 1.5kW/7A), (2)
  nút E-stop/đèn còi báo đã quyết định mua nhưng chưa có trong tay, (3) chưa có sơ đồ đấu nối điện chi
  tiết (mạch động lực + mạch điều khiển) — file `So_do_ket_noi_he_thong.svg` hiện có chỉ là sơ đồ tín
  hiệu mức khối. Khuyến nghị giải quyết cả 3 điểm trước khi cấp điện thật cho động cơ.

## 2026-08-14 (bổ sung 45 — mở rộng scope: I-Device thử nghiệm + OPC UA/Telegram, theo trao đổi miệng với GVHD)
- Theo lời sinh viên báo lại (trao đổi miệng với ThS. Lê Quốc Khương, chưa có văn bản/biên bản chính
  thức): GVHD đồng ý cho thử nghiệm kiến trúc PROFINET I-Device (CPU S7-1211C thật đóng vai IO Device
  dưới CPU S7-1500 ảo qua PLCSIM Advanced đóng vai IO Controller) và đồng ý đưa chính thức vào khoá
  luận phần giám sát/cảnh báo qua OPC UA + bot Telegram/WhatsApp gửi thông báo điện thoại.
- **Đây là mở rộng phạm vi so với Thuyết minh gốc và RESEARCH_PROTOCOL.md mục 6** (vốn loại trừ rõ
  IIoT/Cloud SCADA/thông báo từ xa khỏi phạm vi đề tài) — ghi nhận lại đây theo đúng thông lệ dự án
  (mọi quyết định của GVHD đều phải log), nhưng **CHƯA có xác nhận bằng văn bản/email/biên bản** như
  các quyết định trước đó trong `01_Research_Protocol/00_Trao_doi_GVHD/`. Khuyến nghị: sinh viên nên
  xin GVHD xác nhận lại bằng văn bản (email ngắn cũng được) trước khi bảo vệ, để tránh rủi ro không có
  bằng chứng khi hội đồng chất vấn về việc thay đổi phạm vi đề tài.
- Test A (PUT/GET giữa CPU ảo 1500 và CPU thật 1211C qua PLCSIM Advanced TCP/IP Single Adapter, bridge
  qua card Realtek) đã chạy thành công, xác nhận qua Wireshark (S7COMM Ack_Data liên tục, không lỗi).
  Ghi chú kỹ thuật: gặp và giải quyết loạt lỗi driver/mạng (WinPcap xung đột với Npcap, Windows Firewall
  Public profile chặn cổng TCP 102, PUT/GET communication chưa bật trong Protection & Security của CPU
  thật) — chi tiết xem lịch sử trao đổi, chưa viết thành tài liệu riêng.
- Quyết định tiếp theo (2026-08-14): tạm dừng Test B (I-Device thật) để ưu tiên làm OPC UA + Telegram
  bot trước, tái sử dụng code nền từ project riêng `mo_phong` (đồ án khác, không thuộc NCKH này) —
  phần Telegram bot đã có sẵn code (đánh giá "đã hoàn thành" theo ghi chú kỹ thuật của project đó),
  cần điều chỉnh lại để trỏ đúng CPU 1211C thật của NCKH thay vì CPU ảo của project gốc.

## 2026-08-09 (bổ sung 44 — đóng gói riêng gói gửi GVHD)
- Tạo thư mục `01_Research_Protocol/00_Trao_doi_GVHD/Goi_gui_2026-08-09/` chứa bản sao 4 file chuẩn
  bị gửi GVHD (văn bản trao đổi, Chương 1, Chương 2, Danh mục thiết bị) và file
  `Danh_sach_file_gui.md` — bảng markdown liệt kê tên file, nội dung, thứ tự đọc.
- Cập nhật `FILE_STRUCTURE.md` ghi nhận quy ước thư mục con `Goi_gui_YYYY-MM-DD/` dùng để đóng gói
  các đợt gửi GVHD sau này, không lẫn với bản gốc ở `08_Thesis/`, `03_System_Design/`.

## 2026-08-09 (bổ sung 43 — rút gọn ghi chú trích dẫn, sửa xưng hô)
- Rút gọn "GHI CHÚ QUAN TRỌNG VỀ NGUỒN THAM KHẢO" ở đầu Chương 1 từ 1 đoạn dài xuống 1-2 câu ngắn —
  vẫn giữ tinh thần minh bạch (đã rà soát/sửa danh mục tham khảo so với Thuyết minh) nhưng không đi
  vào chi tiết từng trường hợp trong chính văn, vì chi tiết đã có sẵn ở văn bản trao đổi GVHD mục 2.
  Sửa 2 câu trỏ ngược ("xem Ghi chú quan trọng...") cho khớp tên gọi mới.
- Rà soát xưng hô toàn bộ Chương 1 và Chương 2: phát hiện 3 chỗ đang dùng "bạn" (xưng hô kiểu trò
  chuyện, không phù hợp văn phong báo cáo học thuật khách quan) — sửa lại thành thể khách quan/không
  ngôi. Xác nhận không còn "tôi/em/bạn" nào sót lại trong 2 chương chính thức.
- Bản thảo Chương 1 giữ nguyên "lần 8", Chương 2 giữ nguyên "lần 6" (chỉ là hiệu chỉnh câu chữ, không
  đổi cấu trúc/nội dung kỹ thuật).

## 2026-08-09 (bổ sung 42 — rà soát ngôn ngữ trước khi nộp, sửa mâu thuẫn Chương 1 vs Chương 2)
- Theo yêu cầu rà lại ngôn ngữ trước khi gửi GVHD: đọc lại toàn văn Chương 1, Chương 2, văn bản trao
  đổi GVHD (qua pandoc). Phát hiện 1 lỗi thực chất: ghi chú cuối Chương 1 (thêm ngày 2026-08-08) vẫn
  khẳng định "MFM383A-C và MFM384-C là hai model khác nhau thật" và trỏ tới Chương 2 mục 2.3.2/2.3.6
  — cả hai đều SAI so với hiện tại (đã chốt MFM383A-C là đúng, mục đã đổi số thành 2.4.2/2.4.3 sau khi
  tách cấu trúc). Đây là mâu thuẫn trực tiếp giữa 2 chương nếu GVHD đọc cả hai — đã sửa lại ghi chú
  cho khớp với kết luận mới nhất, bản thảo Chương 1 lên "lần 8".
- Không phát hiện lỗi ngôn ngữ/chính tả đáng kể khác trong 3 file chính (Chương 1, Chương 2, văn bản
  trao đổi GVHD) — văn phong nhất quán, câu hỏi GVHD rõ ràng.

## 2026-08-09 (bổ sung 41 — đóng gói file gửi GVHD)
- Soạn `01_Research_Protocol/00_Trao_doi_GVHD/Trao_doi_GVHD_2026-08-09.docx` — văn bản trao đổi GVHD
  hoàn chỉnh dạng Word (3 trang), gộp toàn bộ nội dung từ file .md + bảng tiêu chí đánh giá định
  lượng, gắn sẵn ảnh sơ đồ kết nối hệ thống (chuyển từ SVG sang PNG để mở được trên mọi thiết bị).
  Đánh dấu rõ từng câu hỏi cần GVHD trả lời (❓) để dễ theo dõi.
- Gói gửi cuối cùng rút gọn còn 4 file: Trao_doi_GVHD_2026-08-09.docx (văn bản chính, có sơ đồ),
  Chuong1_Tong_quan_tai_lieu.docx, Chuong2_Doi_tuong_va_phuong_phap_nghien_cuu.docx,
  Danh_muc_thiet_bi_can_xac_dinh.xlsx — thay vì gửi rời 7 file nhỏ lẻ.

## 2026-08-09 (bổ sung 40 — chốt quyết định thiết bị, tách Chương 2, đồng bộ PROJECT_STATUS.md)
- Theo yêu cầu bạn rà soát sâu, đã xử lý dứt điểm 4 điểm tồn đọng: (1) động cơ + đồng hồ Selec
  MFM383A-C — chốt đã mua (bạn xác nhận trực tiếp, chưa có ảnh); (2) mâu thuẫn model đồng hồ đo —
  chốt Selec MFM383A-C là đúng, "MFM384-C" là nhầm lẫn; (3) SPD (CITEL DSH63 + Schneider Easy9) —
  quyết định KHÔNG dùng, ngoài phạm vi đề tài; (4) nút dừng khẩn cấp + đèn báo + còi — chốt mua,
  nâng ưu tiên vì gắn với Success Criteria đã duyệt.
- Thực hiện đề xuất còn treo từ trước: TÁCH Chương 2 (bản thảo lần 6) — mục 2.3 "Cơ sở lý thuyết"
  giờ chỉ còn lý thuyết tổng quát có trích dẫn học thuật; mục 2.4 mới "Lựa chọn thiết bị cụ thể"
  gộp toàn bộ quyết định/model/thông số thiết bị của đề tài; Phương pháp nghiên cứu dời xuống 2.5.
  Sửa luôn tài liệu tham khảo [A2.2] (MFM384-C → MFM383A-C).
- Đồng bộ lại `PROJECT_STATUS.md` (bị lỗi thời từ 2026-08-07, không phản ánh khối lượng công việc
  2 ngày qua) — cập nhật Phase 2 (System Design) và Phase 3 (Hardware Selection) sang "Đang thực
  hiện", liệt kê rõ 5 việc còn chặn để coi 2 phase này là xong.
- Cập nhật `Danh_muc_thiet_bi_can_xac_dinh.xlsx` (động cơ, Selec, SPD, nút dừng khẩn cấp).

## 2026-08-09 (bổ sung 39 — soạn tiêu chí đánh giá định lượng cho Chương 3 + GVHD)
- Rà soát lại RESEARCH_PROTOCOL.md, PROJECT_GUIDE.md, PROJECT_STATUS.md theo yêu cầu "chất vấn giả
  định" của bạn: phát hiện cả 7 tiêu chí thành công (mục 10 RESEARCH_PROTOCOL.md, đã duyệt) đều viết
  dạng định tính, không có ngưỡng đo lường cụ thể (VD: "VFD hoạt động đúng" không định nghĩa % sai số).
- Tạo mới `06_Experiment/Tieu_chi_danh_gia_dinh_luong.md` — định lượng hóa cả 7 tiêu chí (sai số dữ
  liệu ≤2%, thời gian phản hồi cảnh báo ≤5s, kết nối ổn định ≥30 phút, lưu trend ≥1 giờ...) để dùng
  khi thiết kế thực nghiệm và viết Chương 3. Đánh dấu rõ đây là Khuyến nghị, chưa phải Sự kiện đã
  duyệt — cần GVHD xác nhận.
- Cập nhật `01_Research_Protocol/00_Trao_doi_GVHD/Noi_dung_trao_doi_GVHD_2026-08-08.md`: làm mới mục
  3 (nhiều điểm đã tự giải quyết: HMI, VFD, WinCC, contactor...), thêm mục 5 đề xuất GVHD duyệt bộ
  tiêu chí định lượng mới.

## 2026-08-09 (bổ sung 38 — chốt PT100, xác nhận CT bắt buộc, rà soát mua sắm)
- Chốt dùng bộ chuyển đổi PT100 0-10V (Converter B), đấu thẳng ngõ vào analog CPU 1211C, không cần
  mua thêm module. Xác nhận CT (biến dòng) là thiết bị BẮT BUỘC phải mua (Selec không đo dòng trực
  tiếp) — khuyến nghị 3 CT ~10/5A hoặc 15/5A. Thêm dòng module CB 1241 (bạn xác nhận đã có) vào Danh
  mục thiết bị — dùng để đọc đồng hồ Selec qua Modbus RTU (khác chức năng với module đọc analog).
- Rà soát toàn bộ 22 dòng Danh mục thiết bị, lập danh sách: đã có (12 mục), bắt buộc phải mua (CT),
  cần xác nhận lại (động cơ, đồng hồ Selec — chưa có ảnh xác nhận vật lý), vật tư phụ chưa nêu cụ thể.

## 2026-08-09 (bổ sung 37 — đối chiếu 21 ảnh tem máy thiết bị thật, sửa lỗi VNZ200→VNZ100)
- Bạn cung cấp thư mục `04_Hardware/01_hinh_anh_thiet_bi/` gồm 21 ảnh tem máy thiết bị thật đã có
  trong tay. Đã xem toàn bộ và đối chiếu với Danh_muc_thiet_bi_can_xac_dinh.xlsx.
- SỬA LỖI QUAN TRỌNG: biến tần thực tế là **Wecon VNZ100-1R5G-2** (input 1 pha 220V, 1.5kW), KHÔNG
  PHẢI "VNZ200 Series" như đã ghi nhầm trong Danh mục thiết bị, Chương 2 (mục 2.3.2) và sơ đồ kết nối
  SVG suốt từ 2026-08-08. Đã tìm và xác minh manual chính hãng VNZ100 (Wecon VNZ100 User Manual V3.5,
  250210) và cập nhật lại cả 4 file liên quan. Input 1 pha (không phải 3 pha) ảnh hưởng tới thiết kế
  cấp nguồn tủ điện — cần lưu ý khi vẽ sơ đồ nguyên lý ở Chương 3.
- Xác nhận HMI đúng là **eMT3070B** qua tem máy — giải quyết dứt điểm nghi vấn "eMT3070P không tồn
  tại" đã nêu từ trước.
- Xác nhận vật lý thêm 6 hạng mục vào Danh mục thiết bị: contactor Mitsubishi S-T12 (2 unit) + rơ-le
  nhiệt bảo vệ quá tải cùng hãng (giải quyết câu hỏi mở "rơ-le nhiệt — Thuyết minh chưa liệt kê"),
  Aptomat CHINT NXB-63 (3 loại dòng cắt), bộ nguồn 24VDC MEAN WELL LRS-200-24, biến áp điều khiển
  CHINT NDK-250, relay trung gian CNAOM HH52P.
- Phát hiện nhóm thiết bị hoàn toàn mới, chưa từng có trong Thuyết minh hay Danh mục: thiết bị chống
  sét lan truyền (SPD) — cuộn cảm phối hợp CITEL DSH63 + SPD Type 2 Schneider Easy9 EZ9L33620. Thêm
  hàng mới (STT 19-21) vào Danh mục thiết bị.
- Còn 1 điểm cần bạn xác nhận: 2 bộ chuyển đổi tín hiệu PT100 khác loại đã có (4-20mA/0-150°C và
  0-10V/0-200°C) — chưa rõ dùng loại nào hoặc dùng cả hai.
- Cập nhật: Danh_muc_thiet_bi_can_xac_dinh.xlsx (21 dòng, giữ nguyên 2 ảnh đính kèm cũ), Chuong2_
  Doi_tuong_va_phuong_phap_nghien_cuu.docx (bản thảo lần 5, thêm mục 2.3.7 thiết bị phụ trợ), So_do_
  ket_noi_he_thong.svg (đổi nhãn VNZ200→VNZ100-1R5G-2, eMT3070→eMT3070B), References/manuals_thiet_
  bi/Manual_thiet_bi_da_chon.md (viết lại mục 1, xác nhận mục 3, thêm mục 4).
- Task #13 hoàn tất (đổi tên thành "Xác nhận model HMI eMT3070B + biến tần VNZ100 qua tem máy thật").

## 2026-08-08 (bổ sung 36 — chốt xong WinCC Runtime Advanced)
- Bạn đã bổ sung rõ Model WinCC = "Runtime Advanced" (đã hết mơ hồ). Xác minh (WebSearch): bản 1 trạm
  (single-station), giới hạn theo số tag license (128–65536 PowerTags), tối đa 8 kết nối OPC — phù hợp
  đúng quy mô mini SCADA 1 máy tính giám sát của đề tài, không cần bản Professional (đa client/server).
- Cập nhật Danh_muc_thiet_bi_can_xac_dinh.xlsx (trạng thái "Đã chọn") và Chuong2_Doi_tuong_va_phuong_
  phap_nghien_cuu.docx mục 2.3.4 (bản thảo lần 4) — nêu rõ lý do chọn Runtime Advanced thay vì
  Professional.
- Task #13 thu hẹp lại còn 3 việc: xác nhận đúng mã HMI thật, chốt công suất+điện áp động cơ để chọn
  đúng mã VNZ200, tìm đúng datasheet cho model cuối cùng.

## 2026-08-08 (bổ sung 35 — gộp nội dung trao đổi GVHD thành 1 buổi)
- Tạo 01_Research_Protocol/00_Trao_doi_GVHD/Noi_dung_trao_doi_GVHD_2026-08-08.md — gộp 4 việc đang chờ
  GVHD: (1) xin duyệt Chương 1 bản 7, (2) báo cáo lỗi mô tả trích dẫn trong danh mục tham khảo Thuyết
  minh gốc, (3) xác nhận 4 điểm thiết bị (model HMI thật, WinCC Advanced/Professional, chấp nhận HMI
  khác hãng TIA Portal không, công suất động cơ + điện áp để chọn đúng mã VNZ200), (4) hỏi kinh phí.
- Task #8, #9 hoàn thành (đã chuẩn bị xong nội dung); tạo Task #15 cho bước gửi/trao đổi thật (do
  người dùng tự thực hiện).

## 2026-08-08 (bổ sung 34 — sơ đồ kết nối hệ thống mức tín hiệu cho Chương 3)
- Tạo 03_System_Design/So_do_ket_noi_he_thong.svg: sơ đồ khối mức tín hiệu, dùng đúng tên terminal
  thật lấy từ manual đã tra cứu (VNZ200: FWD/REV/FIV/FIC/RA-RB-RC; MFM383A-C: RS485/Modbus qua CT+PT).
  Gồm PC WinCC + HMI (Ethernet/PROFINET) → PLC S7-1200 → VFD VNZ200 → động cơ 3 pha; đồng hồ đo và
  PT100+bộ chuyển đổi phản hồi về PLC. Có ghi chú rõ: chi tiết I/O còn phụ thuộc module mở rộng PLC
  thật sẽ dùng — đây là sơ đồ mức khối, chưa phải bản vẽ đấu nối chi tiết cuối cùng.
- Task #12 hoàn thành (mức sơ đồ tổng quát); việc vẽ chi tiết đấu nối theo đúng kích thước/board mạch
  vẫn chờ xác nhận đủ thiết bị (Task #13).

## 2026-08-08 (bổ sung 33 — giảm trích dẫn lặp "Thuyết minh mục X" trong Chương 1)
- Rà lại toàn bộ Chương 1, giảm từ ~13 xuống còn 4 lần trích "(Thuyết minh mục X)" — chỉ giữ ở chỗ
  giới thiệu lần đầu (mục 1.1), Ghi chú quan trọng, phần 1.7 (quan trọng nhất, gắn RQ2/RQ4), và kết
  luận 1.8/9.2.1. Các lần lặp lại ý cũ đổi thành tự trỏ nội bộ ("đã nêu ở mục 1.1") thay vì trích lại
  số mục Thuyết minh — đúng hướng đã bàn trước đó (khác với trích dẫn học thuật [1]-[15] vẫn giữ
  nguyên đầy đủ theo yêu cầu GVHD, xem bổ sung 32). Chương 1 nay là bản thảo lần 7.

## 2026-08-08 (bổ sung 32 — ghi nhận nhận xét GVHD về mức trích dẫn theo chương)
- Cập nhật WRITING_GUIDELINES.md mục 1.1 (mới): GVHD xác nhận trực tiếp — Chương 1-2 PHẢI có trích
  dẫn học thuật đầy đủ (đúng như đã làm); Chương 3 trở đi không cần trích dẫn dày, chuyển sang phân
  tích chuyên môn sâu dựa trên lý thuyết đã có. Form trình bày tương tự đồ án môn học thông thường.
  Làm rõ: nhận xét này áp dụng cho trích dẫn HỌC THUẬT [n], không mâu thuẫn với khuyến nghị giảm
  trích dẫn lặp "(mục X Thuyết minh)" nội bộ đã bàn trước đó — hai loại trích dẫn khác nhau.

## 2026-08-08 (bổ sung 31 — tìm manual chính hãng cho 3 thiết bị đã chọn)
- Tạo References/manuals_thiet_bi/Manual_thiet_bi_da_chon.md — tổng hợp thông số + link manual CHÍNH
  HÃNG (không phải nguồn thứ ba) cho: Wecon VNZ200 (User Manual V4.5, ftp.we-con.com.cn), Selec
  MFM383A-C (datasheet qua tme.eu), Weintek eMT3070 (dl.weintek.com).
- Phát hiện quan trọng: (1) MFM383A-C không đo dòng trực tiếp mà PHẢI qua CT (biến dòng) — xác nhận
  CT là thiết bị BẮT BUỘC, không còn là suy luận "có thể cần"; (2) model "eMT3070P" KHÔNG tồn tại theo
  tra cứu — dòng thật là eMT3070A/B (192x138mm) hoặc eMT3105P (259x201mm, khác hẳn) — cần bạn xác
  nhận lại đúng mã; (3) VNZ200 là cả dòng nhiều mã công suất, cần chốt đúng mã theo công suất động cơ
  + điện áp cấp (220V hay 380V) trước khi vẽ đấu nối.
- Không tải được file PDF gốc về máy (sandbox không có mạng ngoài trực tiếp qua curl) — đã để link
  gốc để bạn tự tải. Đã cập nhật cột Ghi chú trong Danh_muc_thiet_bi_can_xac_dinh.xlsx cho 3 dòng
  tương ứng, giữ nguyên ảnh minh họa.
- Task #14 hoàn thành; Task #13 vẫn còn (WinCC chưa rõ, HMI cần xác nhận mã, VFD cần chốt mã công suất).

## 2026-08-08 (bổ sung 30 — cập nhật thiết bị bạn vừa chọn vào Danh_muc_thiet_bi_can_xac_dinh.xlsx)
- Bạn đã tự điền: HMI = Weintek eMT3070P; biến tần = Wecon VNZ200 Series; đồng hồ đo = Selec MFM383A-C;
  WinCC = "Runtime Advanced / Professional)" (có vẻ nhập thiếu/lệch, cần bạn xác nhận lại).
- Đã tra cứu xác minh (WebSearch 2026-08-08): VNZ200 là dòng biến tần thật của Wecon (Netla, Khang Việt
  Electric phân phối tại VN) — khớp đúng nhãn "Wecon" trong Thuyết minh, GIẢI QUYẾT mâu thuẫn biến tần.
  Weintek eMT3070P là HMI thật, có driver kết nối Siemens S7-1200 qua Ethernet (S7CommPlus), nhưng nằm
  ngoài hệ sinh thái TIA Portal (cấu hình bằng EasyBuilder Pro riêng) — cần GVHD xác nhận chấp nhận.
  Selec MFM383A-C khớp đúng Thuyết minh — GIẢI QUYẾT mâu thuẫn đồng hồ đo.
- Lưu ý còn lại: tài liệu hãng đã upload trước đây (manual GD35/INVT, html MFM384-C) KHÔNG khớp model
  thật vừa chọn — cần tài liệu đúng dòng VNZ200 và đúng datasheet MFM383A-C trước khi vẽ đấu nối Chương 3.
- Cập nhật màu trạng thái mới trong file: "Đã chọn — cần lưu ý kỹ thuật" (tím nhạt), "Cần làm rõ — dữ
  liệu vừa nhập chưa rõ" (cam) — đã thêm chú giải tương ứng vào sheet Chu_giai.
- Cập nhật Task #13 phản ánh tiến độ mới.

## 2026-08-08 (bổ sung 29 — rà soát chéo Chương 1 + Chương 2, sửa 3 điểm chưa khớp)
- Rà toàn bộ text 2 chương (dump paragraph-by-paragraph, đếm số trích dẫn [1]-[15] xuất hiện đủ và
  đúng phạm vi, kiểm tra footer số trang tồn tại ở cả 2 file) — cấu trúc SV04 và trích dẫn học thuật
  đều nhất quán, không lỗi.
- Phát hiện & sửa 3 điểm chưa khớp: (1) Chương 1 mục 1.1/1.8 nhắc "Selec MFM383A-C" như đã chốt,
  chưa có caveat về mâu thuẫn model phát hiện sau này khi làm Chương 2 — đã thêm ghi chú bổ sung cuối
  mục 1.8 (bản thảo lần 6); (2) Chương 2 mục 2.2.1 cũng nhắc MFM383A-C không caveat — đã thêm chú
  dẫn sang mục 2.3.6; (3) Chương 2 mục 2.4.1 nói "tài liệu Selec MFM383A-C" nhưng tài liệu tham khảo
  [A2.2] thực tế trích dẫn là "MFM384-C Datasheet" — mâu thuẫn NỘI BỘ ngay trong Chương 2 — đã sửa lại
  câu văn cho khớp với [A2.2] thật, thêm thẻ trích dẫn [A2.1][A2.2] vào đúng vị trí trong văn bản.
  Chương 2 nay là bản thảo lần 3.

## 2026-08-08 (bổ sung 28 — đồng bộ ghi chú mâu thuẫn thiết bị vào Chương 2 bản thảo lần 2)
- Thêm ghi chú trực tiếp trong Chuong2_Doi_tuong_va_phuong_phap_nghien_cuu.docx mục 2.3.2 (biến tần
  Wecon vs INVT GD35) và 2.3.6 (đồng hồ đo MFM383A-C vs MFM384-C), trỏ tới
  03_System_Design/Danh_muc_thiet_bi_can_xac_dinh.xlsx — tránh tình trạng 2 tài liệu không khớp nhau.

## 2026-08-08 (bổ sung 27 — danh mục thiết bị cần xác định trước Chương 3)
- Created `03_System_Design/Danh_muc_thiet_bi_can_xac_dinh.xlsx`: 18 hạng mục thiết bị, phân loại theo
  4 trạng thái màu (Đã nêu rõ / Đã nêu thiếu model / MÂU THUẪN cần xác minh / Suy luận chưa có trong
  Thuyết minh), có sheet Chú giải giải thích rõ Fact vs Suy luận theo CLAUDE.md.
- Phát hiện 2 mâu thuẫn thật (có ảnh minh họa kèm theo trong file): (1) biến tần — Thuyết minh ghi
  "Wecon", manual đã upload là INVT GD35; (2) đồng hồ đo — Thuyết minh ghi Selec MFM383A-C, file hãng
  đã upload là MFM384-C (khác thiết kế mặt hiển thị, không phải lỗi đánh máy).
- Đã tạo Task #13 để xác minh 2 mâu thuẫn này trước khi vẽ sơ đồ đấu nối Chương 3 (Task #12).

## 2026-08-08 (bổ sung 26 — soạn Chương 2: Đối tượng và phương pháp nghiên cứu)
- Created `08_Thesis/Chuong2_Doi_tuong_va_phuong_phap_nghien_cuu.docx` (bản thảo lần 1), theo khung
  SV04, dựa trực tiếp trên Thuyết minh mục 9 (đối tượng/phạm vi), mục 10 (3 phương pháp: tham khảo
  tài liệu, mô hình hóa/thiết kế, thực nghiệm) và mục 11.1.1 (thiết kế phần cứng). Mục 2.3 Cơ sở lý
  thuyết trích dẫn lại 4/5 tài liệu CORE ([2] Trần Văn Hiếu, [7] Kumar, [8] Malla, [13] Rahmatullah,
  [15] Nguyễn Phương Trà) giữ nguyên số [n] của Chương 1 để tránh trùng khi hợp nhất báo cáo.
- Có footer số trang từ đầu (đã rút kinh nghiệm lỗi thiếu số trang ở Chương 1 bản 4).
- Phát hiện điểm cần xác minh: model đồng hồ đo ghi trong Thuyết minh là "Selec MFM383A-C" nhưng
  file datasheet hãng người dùng upload lại tên "MFM384-C" — chưa rõ có phải cùng thiết bị hay không,
  đã ghi chú trong docx mục 2.3.6 và tạo Task #12 để xử lý trước khi chốt thiết kế phần cứng Chương 3.
- Đã cập nhật task list: Task #10, #11 hoàn thành; tạo Task #12 (thiết kế kiến trúc/phần cứng chi tiết).

## 2026-08-07 (bổ sung 19 — tách 5 tài liệu CORE làm nền tảng triển khai đề tài)

**Nguồn:** yêu cầu của bạn — xác định các bài báo "core" (liên quan mạnh nhất) để dựa vào phát
triển đề tài, đưa vào thư mục riêng.

**Tiêu chí chọn CORE:** cùng thành phần trực tiếp với đề tài (PLC S7-1200/PLC công nghiệp +
HMI/WinCC/VFD, không phải chỉ 1 thành phần lẻ), không lệch quy mô/ngữ cảnh (không phải công
nghiệp nặng/đường sắt/cao áp), không dùng AI (đúng Scope).

**Created**
- `References/pdf/_core_de_tai/` — bản sao (không di chuyển) 5 file PDF core:
  - `2020_NguyenPhuongTra_PWM_S71200_ATV310.pdf` — cùng dòng PLC S7-1200 như đề tài
  - `2017_TranVanHieu_ThietKeHeThongHmiScadaTiaPortal.pdf` — tài liệu kỹ thuật nền cho cả
    PLC+HMI+WinCC trên TIA Portal
  - `2021_Rahmatullah_PLCPIDSpeedControl.pdf` — PLC+VFD vòng kín
  - `2019_Kumar_PLCMonitoringProtection.pdf` — PLC+HMI bảo vệ động cơ
  - `2023_Malla_FaultIdentificationPLCSCADA.pdf` — PLC+SCADA bảo vệ động cơ

**Modified**
- `References/literature_matrix.xlsx`: tô vàng cột "Tác giả" và ghi chú "CORE" cho 5 dòng
  tương ứng (STT 1, 5, 7, 14, 15) để dễ nhận diện khi mở lại.
- `FILE_STRUCTURE.md`: ghi nhận thư mục `_core_de_tai/` mới.

**Lưu ý:** 5 bài này không thay thế các bài còn lại — vẫn cần cả 15 bài để đủ Coverage theo RQ
và viết Chương 1. CORE chỉ là gợi ý ưu tiên đọc kỹ/tham khảo trước khi bắt đầu Phase 2 System
Design, vì đây là nhóm sát cấu hình phần cứng/kiến trúc nhất với đề tài.

## 2026-08-07 (bổ sung 18 — sửa lỗi định dạng gạch ngang sai)

**Phát hiện (bạn gửi ảnh chụp màn hình phát hiện):** khi dọn dẹp ở bổ sung 17, việc ghi đè dữ
liệu vào các dòng cũ đã để sót **định dạng gạch ngang (strikethrough)** từ các dòng "LOẠI" cũ —
khiến 4 dòng hợp lệ (STT 4 Nguyễn Chí Ngôn, STT 13 Norimatsu, STT 14 Rahmatullah, STT 15 Kumar)
hiển thị như thể đã bị loại, dù dữ liệu và Coverage vẫn đúng.

**Đã sửa:** xóa toàn bộ định dạng gạch ngang trên 15 dòng đang dùng (STT 1-15) trong
`References/literature_matrix.xlsx`. Xác nhận lại không còn dòng nào bị gạch ngang sai. Dữ
liệu/Coverage không đổi.

## 2026-08-07 (bổ sung 22 — cập nhật hạn nộp thật, đã dùng hết quyền gia hạn)

**Nguồn:** bạn cho biết đề tài đã dùng hết quyền gia hạn tối đa (6 tháng), hạn nộp mới là
tháng 01/2027, có thể nộp sớm hơn nếu hoàn thành trước.

**Modified**
- `PROJECT_STATUS.md`: bước hành chính 9 (Gia hạn) chuyển "✅ Đã xác nhận", ghi rõ hạn mới.
  Thêm mục Vướng mắc/Rủi ro về áp lực thời gian: ~10 tháng đã trôi qua chỉ mới xong Phase 0-1,
  còn ~5 tháng cho 7 phase còn lại, không còn quyền gia hạn thêm.
- `PROJECT_GUIDE.md` mục Timeline: thêm ghi chú hạn thật, khuyến nghị rút gọn/song song hóa
  phase, giữ nguyên bảng đề xuất gốc để tham khảo tỷ trọng công việc.

## 2026-08-07 (bổ sung 25 — sửa lỗi thiếu số trang, đúng định dạng SV04)

**Phát hiện (khi bạn hỏi form Chương 1 dựa vào đâu):** file docx được dựng bằng script
(docx-js) thiếu hoàn toàn phần đánh số trang — vi phạm `WRITING_GUIDELINES.md` mục 3 ("Số
trang đánh ở giữa phía dưới mỗi trang", lấy từ SV04 mục II.2.1). Đã kiểm tra và xác nhận đây
là lỗi thật, không phải do định dạng bị mất khi chuyển đổi.

**Modified**
- `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx`: thêm footer đánh số trang tự động, căn giữa,
  đúng font Times New Roman. Không đổi nội dung, chỉ sửa định dạng.

## 2026-08-07 (bổ sung 24 — Chương 1 bản thảo lần 5: chốt hướng xử lý 7 trích dẫn nghi vấn)

**Nguồn:** quyết định của bạn — bỏ qua 2 tài liệu không tìm được (Phạm & Phạm, Gomboc), áp
dụng đúng 5 tài liệu đã xác minh có file thật.

**Modified**
- `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx` → **bản thảo lần 5**: viết lại Ghi chú quan
  trọng đầu chương cho chính xác hơn — nêu rõ 5/7 nguồn gốc trong Thuyết minh có file thật,
  đúng tác giả, chỉ SAI mô tả trích dẫn (tên bài/tạp chí không khớp file gốc — không phải bịa
  đặt tác giả); 2/7 (Phạm & Phạm 2015, Gomboc 2014) không tìm được file, đã BỎ QUA. Không đổi
  nội dung lược khảo 15 tài liệu (đã đúng từ bản 4), chỉ làm rõ và chính xác hóa phần giải
  thích nguồn gốc trích dẫn.
- 5 file PDF thật (Malla, Manafov, Khoa/Thanh/Ngôn, Orhanen, Gedzurs) đã xác nhận đúng vị trí
  chuẩn sẵn có trong `References/pdf/` (Gedzurs ở `_archive_loai_qua10nam/`, vẫn loại theo quy
  tắc ≤10 năm) — không cần di chuyển gì thêm. Các bản trùng trong `References/file mới/` giữ
  nguyên, không xóa (không tự ý xóa file của bạn).

**Trạng thái:** Chương 1 coi như hoàn thiện về nội dung và nguồn — chỉ còn chờ trình GVHD
duyệt (task #8) kèm báo cáo phát hiện lỗi mô tả trích dẫn trong Thuyết minh gốc (task #9).

## 2026-08-07 (bổ sung 23 — đối chiếu file PDF thật cho 7 nguồn nghi vấn trong Thuyết minh)

**Nguồn:** bạn bổ sung 7 file PDF + tài liệu hãng vào `References/file mới/` để mình đối chiếu
với 7 trích dẫn nghi vấn trong Thuyết minh.

**Kết quả đối chiếu (đọc trang 1 từng file qua pdftotext):**
- 5/7 CÓ file thật, đúng tác giả trùng tên với Thuyết minh, nhưng TIÊU ĐỀ/TẠP CHÍ khác hẳn mô
  tả trong Thuyết minh: Khoa/Thanh/Ngôn (thật: "Điều khiển thông minh...", TNU Journal — không
  phải "Nghiên cứu điều khiển... biến tần và PLC", Tạp chí KH&CN VN); Manafov & Huseynov (thật:
  "Modeling of an Integrated Traction Motor Protection System", Наука та прогрес транспорту —
  không phải "Integration of PLC and SCADA...", Automation and Control Engineering Review);
  Malla & KC (thật: "Fault Identification and Protection...", J. of AI/ML/Neural Network —
  không phải "Modern SCADA architectures...", J. of Smart Systems and Technologies); Gedzurs
  (thật: "Temperature Protection Methods of Induction Motor", hội nghị nông nghiệp Latvia —
  không phải "Advanced motor protection...", Journal of Electrical Engineering 2016); Orhanen
  (thật: luận văn Thạc sĩ "Thermal overload protection...", Univ. of Vaasa — không phải bài báo
  "Predictive maintenance...", International Journal of Industrial Automation).
- 2/7 vẫn KHÔNG tìm ra file: [2] Phạm & Phạm 2015, [3] Gomboc 2014.
- Các file khác bổ sung (không phải trích dẫn khoa học cần xác minh): Manual biến tần GD35,
  Siemens S7-1200 System Manual, trang sản phẩm Selec MFM384-C, sách Trần Văn Hiếu (bản scan
  trùng với file đã có), bản scan Thuyết minh (trùng file đã có).

**Kết luận cập nhật:** không phải 7 tài liệu bịa hoàn toàn — nhiều khả năng là mô tả trích dẫn
(tiêu đề/tạp chí) bị ghi sai/garbled so với file nguồn thật khi soạn Thuyết minh (có thể do
dùng AI hỗ trợ viết mà không đối chiếu lại file gốc). Vẫn là lỗi liêm chính trích dẫn cần báo
GVHD, nhưng nhẹ hơn "bịa đặt hoàn toàn". Cập nhật vào `PROJECT_STATUS.md`.

## 2026-08-07 (bổ sung 21 — viết lại Chương 1 bản 4, kế thừa trực tiếp Thuyết minh; phát hiện
rủi ro liêm chính nghiêm trọng trong toàn bộ danh mục tham khảo của Thuyết minh gốc)

**Nguồn:** yêu cầu của bạn — Chương 1 phải phát triển dựa trên Thuyết minh DTSV2025-27 đã
duyệt, không phải một đề tài/lược khảo hoàn toàn tách rời.

**Phát hiện quan trọng (đọc lại đầy đủ trang 2-3, mục 6.1-6.2 Thuyết minh):** danh mục tham
khảo của Thuyết minh có 7 tài liệu khoa học [1]-[7] (trước đó chỉ ghi nhận 4). Tra cứu độc
lập cả 7: không tài liệu nào xác minh được đúng như mô tả (tên tạp chí không tồn tại được tìm
thấy, hoặc tác giả thật trùng tên nhưng bài thật có tiêu đề/tạp chí khác hẳn — xem chi tiết ở
`PROJECT_STATUS.md` mục Vướng mắc/Rủi ro). Đây là phát hiện nghiêm trọng vì Thuyết minh đã qua
hội đồng duyệt chính thức của trường.

**Modified**
- `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx` → **bản thảo lần 4**, viết lại có chủ đích để
  Chương 1 phát triển trực tiếp từ Thuyết minh: mục 1.1 mới trích dẫn nguyên vấn đề và hai
  khoảng trống đã nêu ở Thuyết minh mục 6.2 ("Quy mô hệ thống", "Hạ tầng kết nối"); các mục
  1.2-1.7 (nội dung lược khảo) được viết lại để bám sát và làm bằng chứng cho đúng hai khoảng
  trống đó thay vì đứng độc lập; mục 1.8 xác thực lại khoảng trống, nối thẳng về mục tiêu/phạm
  vi đã duyệt (Selec MFM383A-C, PT100, PLC S7-1200, PWM, không AI/Cloud). Thêm ghi chú quan
  trọng đầu chương giải thích rõ vì sao danh mục tham khảo KHÁC với Thuyết minh gốc (đã tìm và
  xác minh 15 nguồn thay thế, không dùng 7 nguồn không xác thực được).

**Việc cần làm:** khi trình GVHD duyệt Chương 1 (task đang chờ), PHẢI nêu rõ phát hiện về 7
tài liệu tham khảo gốc không xác thực được — đây không phải lỗi nhỏ, cần thầy xác nhận hướng
xử lý (có thể liên quan tới Mẫu SV05 điều chỉnh).

## 2026-08-07 (bổ sung 20 — hoàn tất số trang, sửa lỗi tác giả bài TNU Journal)

**Nguồn:** rà lại theo yêu cầu của bạn để hoàn thiện 3 chỗ còn "tr. cần bổ sung" trong Chương 1.

**Phát hiện lỗi khi tra cứu (quan trọng):**
- Bài "Điều khiển thông minh động cơ không đồng bộ 3 pha..." (TNU Journal, 2022) trước đó ghi
  tác giả là "Nguyễn Chí Ngôn và cộng sự" — **sai**. Tác giả đầu thực tế là **Đào Huỳnh Đăng
  Khoa**, đồng tác giả Sử Hồng Thạnh, Nguyễn Chí Ngôn là tác giả liên hệ (thứ 3), không phải
  tác giả đầu. Đã xác minh qua bản PDF gốc (jst.tnu.edu.vn). Vì CITATION_POLICY.md mục 4 sắp
  xếp theo tên tác giả ĐẦU, việc sửa tên kéo theo **đổi số trích dẫn** trong Chương 1: từ [10]
  (cũ, sắp theo "Ngôn") sang **[6]** (mới, sắp theo "Khoa"). Đã đánh số lại toàn bộ 15 trích
  dẫn trong thân bài và danh mục cho khớp.
- Bài Manafov & Huseynov (2024) trước đó ghi sai số/trang (số 109, tr.65-77) — đã xác nhận lại
  qua DOI, đúng là số 1(105), tr.51-61 (đã sửa ở bổ sung 19, xác nhận lại lần này).
- Bài Kumar và cộng sự (2019): xác nhận số trang tr. 1-6 (đánh số theo bài trong kỷ yếu điện
  tử IEEE, không phải trang liên tục toàn kỷ yếu — cách đánh số phổ biến của IEEE Xplore).

**Modified**
- `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx` → bản thảo lần 3: sửa tên tác giả, số trang đầy
  đủ cho cả 15 nguồn (không còn "tr. cần bổ sung"), đánh số lại trích dẫn theo đúng ABC.
- `References/literature_matrix.xlsx`: sửa tên tác giả STT 4, bổ sung số trang STT 15.

**Trạng thái:** cả 3 việc "rà số trang thiếu" trong task list đã xong. Phase 1 Literature
Review ước tính ~99% — chỉ còn bước trình GVHD duyệt lần cuối.

## 2026-08-07 (bổ sung 17 — dọn Matrix, lưu trữ PDF không dùng)

**Nguồn:** yêu cầu của bạn — rà lại toàn bộ file, xóa các bài không còn dùng khỏi
`literature_matrix.xlsx`.

**Modified**
- `References/literature_matrix.xlsx`: xóa hẳn 5 dòng đã đánh dấu "LOẠI — quá 10 năm" (Gedzurs
  2015, Adamo 2007, Ferrari 2004, Ferrari 2006, Sowmiya 2013). Đánh số lại STT 1-15 liên tục,
  không còn dòng trống/LOẠI xen giữa. Sửa công thức Coverage từ COUNTIFS (có điều kiện lọc
  LOẠI) sang COUNTIF đơn giản trên phạm vi M2:M16/A2:A16 (không cần lọc nữa vì đã xóa hẳn).
  Cập nhật sheet Huong_dan (A14-19): trạng thái 15/15, đủ ngưỡng, và lưu ý STT trong Matrix
  không trùng số trích dẫn [n] trong Chương 1 (Chương 1 đánh số theo ABC riêng).
- Coverage sau khi dọn: **RQ1=7, RQ2=7, RQ3=6, RQ4=4, Tổng=15 — không đổi**, xác nhận việc dọn
  dẹp không ảnh hưởng số liệu.

**Không xóa file vật lý — chỉ lưu trữ:** theo nguyên tắc an toàn dữ liệu, không tự ý xóa vĩnh
viễn file của bạn. 5 file PDF tương ứng đã **chuyển** (không xóa) sang
`References/pdf/_archive_loai_qua10nam/` — vẫn còn nguyên trên máy nếu sau này cần tham khảo
lại hoặc GVHD đổi ý về mốc 10 năm, chỉ không còn tính vào Literature Matrix/Coverage.
- `FILE_STRUCTURE.md`: ghi nhận thư mục lưu trữ mới.

## 2026-08-07 (bổ sung 16 — sửa lỗi lệch cột nghiêm trọng, rà soát toàn bộ Matrix)

**Phát hiện lỗi (tự kiểm tra theo yêu cầu của bạn):** các lần cập nhật trạng thái PDF cho STT
17-20 ở bổ sung 13-15 đã **ghi nhầm cột** — thay vì ghi vào cột "Trạng thái xác minh" (N) và
"File" (O), script ghi đè lên cột "RQ liên quan" (M) và "Trạng thái xác minh" (N), làm **mất
dữ liệu RQ** của cả 4 dòng. Hậu quả: công thức Coverage (COUNTIFS dựa vào cột M) sẽ đếm sai
nếu mở lại file bằng Excel/LibreOffice, dù số hiển thị lúc báo cáo trước đó (RQ1=7...Tổng=15)
là đúng vì được tính TRƯỚC khi lỗi xảy ra.

**Đã sửa:**
- Khôi phục đúng cột M (RQ liên quan) cho STT 17-20: [17] RQ2,RQ4 — [18] RQ2,RQ4 — [19]
  RQ1,RQ2,RQ3 — [20] RQ1,RQ3 (suy ngược chính xác từ chênh lệch Coverage đã ghi nhận ở bổ
  sung 12: +2 RQ1, +3 RQ2, +2 RQ3, +2 RQ4, khớp tuyệt đối).
- Đưa đúng trạng thái "Đã xác minh, đã có PDF" vào cột N, đường dẫn file vào cột O
  (`References/pdf/...`), giữ nguyên Ghi chú cột P và bổ sung dòng xác minh trang 1.
- Xác nhận lại DOI Müller & Doran (`10.1109/WFCS.2018.8402379`) resolve đúng về IEEE Xplore
  qua doi.org — bỏ tô vàng, chuyển tô xanh (đã xác minh) cùng ô File của cả 4 dòng mới.
- Recalculate lại Coverage sau khi sửa: **RQ1=7, RQ2=7, RQ3=6, RQ4=4, Tổng=15 — không đổi so
  với số đã báo cáo, vì đã khôi phục đúng dữ liệu gốc.**

**Rà soát toàn bộ 20 dòng (ô tô vàng còn lại, không liên quan lỗi trên — tồn tại từ trước):**
- STT 1 (Malla), STT 11 (Alcayde), STT 12 (Kaluz): cột "Phương pháp đánh giá đề cập" tô vàng —
  đánh dấu cần đọc lại kỹ hơn phần phương pháp, chưa phải lỗi, chỉ là nhắc việc.
- STT 2 (Manafov), STT 3 (Phạm Tâm Thành), STT 6 (Nguyễn Phương Trà): cột "Trạng thái xác
  minh" tô vàng, đang ghi tạm thông tin số trang thay vì trạng thái chuẩn hóa "Đã xác minh,
  đã có PDF" — dữ liệu đúng, chỉ chưa đồng nhất định dạng với các dòng khác. Không ảnh hưởng
  Coverage (không chứa chữ "LOẠI").
- STT 3: cột DOI/ISSN cũng tô vàng — ISSN có nhưng chưa tra cứu xác nhận qua nguồn ISSN chính
  thức.
- STT 5 (Nguyễn Chí Ngôn): trạng thái ghi "Một phần — DOI đã có", đúng như thiết kế (nguồn
  AI ngoài Scope, chỉ dùng làm bối cảnh, không cần xác minh đầy đủ như nguồn chính).
- STT 4, 13, 14, 15, 16: giữ nguyên "LOẠI — quá 10 năm (yêu cầu GVHD)", tô xám, không tính
  Coverage — đúng như chủ đích.

**Kết luận:** sau khi sửa lỗi, Literature Matrix hiện chính xác. Coverage đạt ngưỡng tối
thiểu ở cả 4 RQ và tổng số. Các ô vàng còn lại là nhắc việc nhỏ (chuẩn hóa định dạng, không
sai dữ liệu), không bắt buộc phải sửa trước khi dùng Chương 1.

## 2026-08-07 (bổ sung 15 — đủ 20/20 PDF, hoàn tất Literature Matrix)

**Modified**
- File cuối cùng còn thiếu (Müller & Doran 2018, STT 17) đã được bạn tải về, đổi tên
  `2018_Muller_ProtectingPROFINET.pdf`. Đã mở trang 1 xác minh đúng tác giả (Thomas Müller,
  Hans Dermot Doran, ZHAW), 4 trang khớp tr. 1-4 đã ghi trong Chương 1.
- `References/literature_matrix.xlsx`: STT 17 chuyển "Đã xác minh, đã có PDF".

**Trạng thái cuối:** 20/20 dòng trong Matrix đều có PDF đã xác minh trang 1 (khớp tác giả/
tiêu đề/số trang). 15 dòng tính vào Coverage (5 dòng STT 4,13,14,15,16 vẫn LOẠI theo quy tắc
≤10 năm của GVHD, giữ PDF lại chỉ để lưu trữ/tham khảo lịch sử, không dùng trích dẫn). Coverage
không đổi: RQ1=7, RQ2=7, RQ3=6, RQ4=4, Tổng=15 — tất cả Đạt. Phase 1 Literature Review coi như
hoàn tất về mặt tư liệu; còn lại bước rà soát cuối cùng với GVHD trước khi chốt Chương 1.

## 2026-08-07 (bổ sung 14 — bạn tải xong 3/4 PDF mới, đã xác minh trang 1)

**Modified**
- Bạn đã tải và bổ sung 3 file vào `References/pdf/`: đổi tên đúng chuẩn
  `2023_Norimatsu_PROFINETNonRealTime.pdf`, `2021_Rahmatullah_PLCPIDSpeedControl.pdf`,
  `2019_Kumar_PLCMonitoringProtection.pdf`. Đã mở trang 1 từng file qua pdftotext, xác nhận
  đúng tác giả/tiêu đề/nơi công bố cho cả 3 — cập nhật Literature Matrix (STT 18-20) sang
  "Đã xác minh, đã có PDF".
- Xác nhận thêm: bài Rahmatullah có 4 tác giả đúng như đã ghi (Daeng Rahmatullah, Iradiratu
  Diah PK, Belly Yan Dewantara, Fendi Achmad), trang 275-280 — cập nhật số trang trong danh
  mục tham khảo Chương 1 [13] (trước đó ghi "tr. cần bổ sung").
- Bài Kumar xác nhận đúng 4 tác giả (Dileep Kumar, Abdul Basit, Aisha Saleem, Engr. Ghulam
  Abbas) — khớp với sửa lỗi ở bổ sung 13.

**Còn thiếu:** chỉ còn 1/4 file — Müller & Doran 2018 (STT 17) — link bản full-text miễn phí
đã cung cấp ở bổ sung 13 (`scispace.com/pdf/protecting-profinet-cyclic-real-time-traffic-a-performance-1yyu2mysb6.pdf`),
bạn tự tải và đặt tên `2018_Muller_ProtectingPROFINET.pdf`.

**Literature Matrix hiện tại:** 19/20 dòng đang tính có PDF xác minh (17 dòng cũ + STT
18,19,20 mới; 5 dòng STT 4,13,14,15,16 đã LOẠI theo quy tắc GVHD). Chỉ còn STT 17 (Müller)
thiếu PDF vật lý.

## 2026-08-07 (bổ sung 13 — tìm PDF nguồn mới, sửa lỗi tác giả)

**Modified**
- `References/literature_matrix.xlsx`: sửa tác giả STT 20 (Kumar) — bài có **4 tác giả** (D.
  Kumar, A. Basit, A. Saleem, **E.G. Abbas**), không phải 3 như đã ghi ở bổ sung 12. Đã sửa
  đồng bộ trong `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx` (trích dẫn trong bài và danh mục
  tham khảo [6]).
- Chương 1: bổ sung số trang cho nguồn [9] Müller & Doran (tr. 1-4, xác nhận qua bản full-text
  tìm được).

**Kết quả tìm PDF cho 4 nguồn mới (STT 17-20):**
- STT 17 (Müller & Doran 2018): **tìm được bản full-text miễn phí** tại
  `scispace.com/pdf/protecting-profinet-cyclic-real-time-traffic-a-performance-1yyu2mysb6.pdf`
  — bạn tự tải về, lưu `References/pdf/2018_Muller_ProtectingPROFINET.pdf`.
- STT 18 (Norimatsu & Yamauchi 2023), STT 19 (Rahmatullah và cộng sự 2021), STT 20 (Kumar và
  cộng sự 2019): chỉ tìm thấy trên IEEE Xplore (trả phí), không có bản mirror/preprint miễn
  phí nào. Sandbox không tải được PDF trực tiếp (giới hạn mạng, đã ghi nhận từ trước) — cần
  bạn tải qua tài khoản/thư viện số của trường có quyền truy cập IEEE Xplore.

## 2026-08-07 (bổ sung 12 — áp dụng quy tắc ≤10 năm của GVHD)

**Nguồn:** góp ý trực tiếp của GVHD (qua bạn): loại tài liệu quá 10 năm khi trích dẫn cho
quyển báo cáo NCKH sinh viên (khác với bài báo khoa học, nơi tài liệu kinh điển có thể chấp
nhận).

**Modified**
- `LITERATURE_RULES.md` mục Inclusion/Exclusion: bỏ ngoại lệ "tài liệu kinh điển", áp chặt mốc
  ≤10 năm (2016–2026), không ngoại lệ.
- `References/literature_matrix.xlsx`: đánh dấu LOẠI 5 dòng quá 10 năm (STT 4 Gedzurs 2015,
  13 Adamo 2007, 14 Ferrari 2004, 15 Ferrari 2006, 16 Sowmiya 2013 — tô xám, gạch ngang, không
  tính vào Coverage). Thêm 4 dòng mới STT 17-20 (Müller & Doran 2018; Norimatsu & Yamauchi
  2023; Rahmatullah và cộng sự 2021; Kumar/Basit/Saleem 2019 — đều IEEE Xplore, Tier 1, trong
  10 năm). Coverage cuối: RQ1=7, RQ2=7, RQ3=6, RQ4=4, Tổng=15 (tất cả Đạt).
- `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx`: viết lại bản 2 — bỏ trích dẫn 5 nguồn bị loại,
  thêm 4 nguồn mới, đánh số lại toàn bộ trích dẫn [1]-[15] theo đúng thứ tự ABC tác giả
  (`CITATION_POLICY.md` mục 4).
- `RESEARCH_PROTOCOL.md` mục 8 và `PROJECT_GUIDE.md` mục Research Gap: cập nhật số liệu 16→15
  tài liệu, dẫn nguồn sang Chương 1 bản 2, làm rõ kết luận chỉ có giá trị trong phạm vi tài
  liệu đã lược khảo (không phải khẳng định tuyệt đối về mọi nghiên cứu từng công bố).

**Đánh dấu SUPERSEDED**
- `02_Literature_Review/Tong_hop_luoc_khao_theo_chu_de.docx` — giữ nguyên bản 16 nguồn cũ, chỉ
  để tham khảo lịch sử; không dùng để trích dẫn nữa.

**Còn tồn:** 4 file PDF nguồn mới (STT 17-20) chưa có trong `References/pdf/` — sandbox không
tải được PDF trực tiếp, cần bạn tự tải và đặt tên `2018_Muller_ProtectingPROFINET.pdf`,
`2019_Kumar_PLCMonitoringProtection.pdf`, `2021_Rahmatullah_PLCPIDSpeedControl.pdf`,
`2023_Norimatsu_PROFINETNonRealTime.pdf`. Một số số trang trong Chương 1 bản 2 còn đánh dấu
"tr. cần bổ sung" — cần tự tra lại trước khi nộp.

## 2026-08-07 (bổ sung 11 — bản thảo Chương 1 hoàn chỉnh)

**Created**
- `08_Thesis/Chuong1_Tong_quan_tai_lieu.docx` — Chương 1 "TỔNG QUAN TÀI LIỆU" bản thảo lần 1,
  7 mục (1.1–1.7), định dạng đúng `WRITING_GUIDELINES.md` (Times New Roman 13, lề 3/2/2/2cm,
  giãn dòng), trích dẫn đánh số lại theo đúng thứ tự ABC tác giả (`CITATION_POLICY.md` mục 4)
  kèm danh mục 16 tài liệu tham khảo đầy đủ.

**Còn tồn (đánh dấu "tr. cần bổ sung" trong file):** 4 tài liệu thiếu số trang chính xác
(Ferrari 2004, Manafov 2024, Nguyễn Chí Ngôn 2022) — cần bạn tự tra lại trước khi nộp.

**Phase 1 ước tính ~95%** — còn thiếu bước rà soát cuối và xác nhận với GVHD.

## 2026-08-07 (bổ sung 10 — tổng hợp theo chủ đề, xác thực Research Gap)

**Created**
- `02_Literature_Review/Tong_hop_luoc_khao_theo_chu_de.docx` — đọc và tổng hợp 16 tài liệu
  theo 5 chủ đề (PLC, HMI, WinCC, VFD, PROFINET & tích hợp), mỗi chủ đề nêu cách tiếp cận đã
  có, đồng thuận/khác biệt, điều chưa giải quyết — đúng cấu trúc `LITERATURE_RULES.md` Bước 7.

**Modified**
- `RESEARCH_PROTOCOL.md` mục 8 và `PROJECT_GUIDE.md` mục Research Gap: viết lại có trích dẫn,
  không còn đánh dấu "preliminary" — kết luận: chưa tìm thấy nghiên cứu tích hợp đủ 5 thành
  phần PLC S7-1200 + HMI + WinCC + VFD + PROFINET cho giáo dục động cơ 3 pha, đúng như gap
  sơ bộ ban đầu.
- `PROJECT_STATUS.md`: Phase 1 Literature Review ước tính ~80% (Bước 1-8 xong, còn Bước 9 viết
  Chương 1 hoàn chỉnh).

**Lưu ý:** số trích dẫn [STT] dùng trong bản tổng hợp là tạm thời (theo thứ tự Literature
Matrix), sẽ đánh số lại theo đúng thứ tự ABC khi ghép vào Chương 1 chính thức (theo
`CITATION_POLICY.md` mục 4).

## 2026-08-07 (bổ sung 9 — hoàn tất 16/16 PDF)

**Modified**
- Bạn đã tải lại đúng file cho STT 15 (`ETFA2006_WIP_profinet_17.pdf` → đổi tên
  `2006_Ferrari_JitterPROFINET.pdf`). Đã mở trang 1 xác minh đúng tiêu đề/tác giả (Ferrari,
  Flammini, Marioli, Taroni, Venturini). Cập nhật Literature Matrix: cột File + trạng thái
  "Đã xác minh, đã có PDF".
- File sai trước đó (Canuto & Musso, không liên quan đề tài) đã được bạn thay thế, không còn
  trong `References/pdf/`.

**Trạng thái Literature Matrix:** 16/16 tài liệu có PDF đúng, đã xác minh qua trang 1 từng
file. Coverage: RQ1=7, RQ2=7, RQ3=6, RQ4=4 — tất cả đạt ≥3, tổng 16/15-20 đạt.

## 2026-08-07 (bổ sung 8 — đối soát PDF vừa tải)

**Modified**
- 7/8 file PDF bạn tải về đã đổi tên đúng chuẩn và cập nhật cột File trong Literature Matrix
  (STT 9-14, 16). Trang thật của bài Kaluz (ELab) là IFAC-PapersOnLine 53(2), 17228-17233
  (đã sửa lại, khác số trang lấy từ snippet tìm kiếm trước đó).

**Phát hiện lỗi:** file `canuto2006.pdf` (dự kiến là bài Ferrari và cộng sự 2006 về jitter
PROFINET, STT 15) thực chất là một bài **hoàn toàn khác chủ đề** — "Embedded Model Control:
Application to Interferometric Metrology Lines" của Canuto & Musso (quang học/không gian, IFAC
2006). Đã kiểm tra trang 1 để xác nhận. Đánh dấu STT 15 là "PDF tải nhầm" trong Literature
Matrix, chưa tính là đã có PDF.

## 2026-08-07 (bổ sung 7 — đủ ngưỡng tối thiểu)

**Added — 3 tài liệu mới (IEEE Xplore, Tier 1):**
- Ferrari, Flammini, Marioli, Taroni (2004), IEEE WFCS — "Experimental evaluation of
  PROFINET performance" — RQ2, RQ4
- Ferrari, Flammini, Marioli, Taroni, Venturini (2006), IEEE ETFA — "Experimental analysis
  to estimate jitter in PROFINET IO Class 1 networks" — RQ2, RQ4
- Sowmiya, D. (2013), IEEE ISCO — "Monitoring and control of a PLC based VFD fed three phase
  induction motor for powder compacting press machine" — RQ1, RQ2, RQ3

**Coverage sau khi thêm:** RQ1=7, RQ2=7, RQ3=6, RQ4=4 — **tất cả RQ đã đạt ≥3**. Tổng
16/15-20 — **đã đạt ngưỡng tối thiểu** theo `LITERATURE_RULES.md`.

**Còn tồn:** 8 tài liệu mới (từ 2 đợt tìm gần nhất) chưa tải được PDF do giới hạn mạng sandbox
— cần bạn tự tải theo link ở cột Ghi chú, một số cần quyền truy cập IEEE Xplore qua thư viện
trường. DOI của 3 nguồn IEEE mới cũng chưa tra được chính xác — mới có document ID.

## 2026-08-07 (bổ sung 6 — tìm thêm tài liệu RQ1/RQ4)

**Added — 5 tài liệu mới (Tier 1, đã xác minh DOI/nguồn qua WebSearch):**
- Hijazi, Andó, Pödör (2025), *Actuators*, DOI 10.3390/act14110524 — RQ4
- Hijazi, Andó, Pödör (2024), *Heliyon*, DOI 10.1016/j.heliyon.2024.e37560 — RQ4
- Alcayde và cộng sự (2022), *Inventions*, DOI 10.3390/inventions7040115 — RQ1
- Kalúz, Čirka, Fikar (2020), *IFAC-PapersOnLine*, DOI 10.1016/j.ifacol.2020.12.1757 — RQ1
  (kiến trúc "lightweight SCADA" — sát nhất với tinh thần mini SCADA của đề tài)
- Adamo và cộng sự (2007), *IEEE Trans. Instrumentation and Measurement* — RQ1 (ngoại lệ
  tài liệu kinh điển, ngoài khung 10 năm)

**Hạn chế:** chưa tải được PDF (mạng sandbox chặn tải trực tiếp) — 5 file này cần bạn tự tải
thủ công theo link ghi trong cột Ghi chú của Literature Matrix, rồi lưu vào `References/pdf/`.

**Coverage sau khi thêm:** RQ1=6, RQ2=4, RQ3=5, RQ4=2 (còn thiếu 1), Tổng=13/15-20.

## 2026-08-07 (bổ sung 5 — Literature Matrix)

**Created**
- `References/literature_matrix.xlsx` — 8 tài liệu đã điền (sheet Matrix), sheet Coverage tự
  đếm số tài liệu/RQ bằng công thức, sheet Huong_dan giải thích cách dùng.

**Kết luận Coverage:** RQ1 và RQ2 và RQ3 đạt về số lượng (nhưng RQ1 chất lượng yếu — xem
ghi chú), **RQ4 = 0 tài liệu**, tổng 8/15-20 — chưa đủ, cần lược khảo thêm.

## 2026-08-07 (bổ sung 4 — dọn tài liệu, nới Database)

**Modified**
- `LITERATURE_RULES.md`: nới chính sách Database — thêm Tier 2 (tạp chí trong nước có phản
  biện, luận văn Thạc sĩ/Tiến sĩ công khai, ResearchGate của bài đã đăng chính thức, sách
  chuyên khảo có NXB) bên cạnh Tier 1 (8 database gốc).
- `CITATION_POLICY.md`: thêm mục hướng dẫn dùng EndNote 21 (giải quyết đồng bộ trích dẫn↔danh
  mục, không giải quyết xác thực nguồn; cần tạo custom output style cho đúng format của trường).

**Created / Moved**
- 8 bài báo/luận văn/sách chuyển vào `References/pdf/`, đặt tên `YYYY_Author_Title.pdf`.
- 2 tài liệu hãng (Manual GD35, Siemens S7-1200 System Manual) chuyển vào `04_Hardware/`.
- 1 báo cáo NCKH SV khác đề tài (tham khảo hình thức) chuyển vào
  `01_Research_Protocol/01_Mau_de_cuong_chinh_thuc/`.
- 2 file bài tập PLC chuyển vào `05_Simulation/`.
- Xóa thư mục tạm `tài liệu/` sau khi dọn xong.

**Phát hiện khi dọn:** nguồn trích [4] trong thuyết minh ghi "Gedzurs, J. — Journal of
Electrical Engineering, 2016" nhưng file thật là **Aleksejs Gedzurs, kỷ yếu hội nghị
"Research for Rural Development 2015", Volume 1** — sai cả năm (2015 không phải 2016) và sai
loại nguồn (hội nghị, không phải tạp chí "Journal of Electrical Engineering"). Cần sửa lại
trong thuyết minh/Chương 1 khi viết báo cáo chính thức.

## 2026-08-07 (bổ sung 3 — đối chiếu biểu mẫu chính thức)

**Modified**
- `WRITING_GUIDELINES.md`: viết lại cấu trúc báo cáo (3 chương, không phải 5) và định dạng
  (font/lề/giãn dòng/đánh số) theo đúng `SV04_Quy định hinh thuc trinh bay...docx`.
- `CITATION_POLICY.md`: sửa lại từ "IEEE thuần túy" sang style thật của trường (đánh số ngoặc
  vuông trong bài, danh mục tham khảo sắp theo ABC tác giả — không theo thứ tự xuất hiện).
- `PROJECT_STATUS.md`: thêm bảng theo dõi quy trình hành chính 14 bước (theo
  `QT_ Thuchien detaiNCKHSV.pdf`), đối chiếu mã đề tài **DTSV2025-27**.
- `PROJECT_GUIDE.md`: ghi chú liên kết tới mẫu Thuyết minh chính thức SV01.

**Nguồn:** các file trong `01_Research_Protocol/04_Bieu_mau_NCKH_truong/` do bạn cung cấp
(SV01, SV04, QT_Thuchien detaiNCKHSV.pdf).

## 2026-08-07 (bổ sung 2)

**Updated**
- Đề tài chính thức được duyệt (xác nhận từ bạn) — `PROJECT_STATUS.md` Phase 0 chuyển sang
  "Approved (chính thức)".

**Created**
- Thư mục `01_Research_Protocol/04_Bieu_mau_NCKH_truong/` để lưu biểu mẫu/quy định NCKH sinh
  viên chính thức của Trường ĐH Kỹ thuật - Công nghệ Cần Thơ.

## 2026-08-07 (bổ sung)

**Created**
- 4 thư mục con trong `01_Research_Protocol/` để chuẩn bị bước "thống nhất đề tài" với GVHD:
  `00_Trao_doi_GVHD/`, `01_Mau_de_cuong_chinh_thuc/`, `02_Bien_ban_duyet/`,
  `03_Danh_gia_kha_thi/` (cập nhật tương ứng `FILE_STRUCTURE.md`).

## 2026-08-07

**Added**
- Research Gap — mục 8 `RESEARCH_PROTOCOL.md` / `PROJECT_GUIDE.md`.

**Modified**
- Research Question — `RESEARCH_PROTOCOL.md` mục 4 / `PROJECT_GUIDE.md`.

**Updated**
- System Architecture — `03_System_Design/`.

**Created**
- Duyệt Research Protocol v1.0 (`RESEARCH_PROTOCOL.md`).
- Quy trình chuẩn lược khảo tài liệu 12 bước (`LITERATURE_RULES.md`, bản đầy đủ tại
  `02_Literature_Review/Quy_trinh_luoc_khao_tai_lieu.docx`).
- Cấu trúc thư mục dự án theo `FILE_STRUCTURE.md` cùng các file quy chuẩn: `CLAUDE.md`,
  `PROJECT_GUIDE.md`, `PROJECT_STATUS.md`, `WRITING_GUIDELINES.md`, `CITATION_POLICY.md`.

---
*Định dạng mục mới: thêm ở đầu file (mới nhất trên cùng), theo thứ tự ngày giảm dần. Trong
mỗi ngày, dùng nhóm Added/Modified/Updated/Created — chỉ ghi nhóm nào thực sự có thay đổi.*
