# Prototype — Trợ lý đổi chuyến khi chuyến bay bị huỷ (T3 Du lịch)

**Cách chạy:** mở `index.html` bằng trình duyệt (double-click, không cần cài gì — một file HTML, không backend, không đăng nhập, không gọi AI thật: câu trả lời của trợ lý là kịch bản soạn sẵn, không có API key).

**Màn hình:** trái — điện thoại của khách; phải — bảng điều khiển demo (bấm một nút kịch bản là tự Reset và chạy ca đó). Dữ liệu dựng theo track T3: đặt chỗ TRV-7Q2K (2 hành khách, bé 5 tuổi), BM 213 đã huỷ do bão, BM 217 còn 1 chỗ / BM 201 còn 9 / BM 205 còn 4.

## Ảnh đánh số

| Ảnh | Chụp cái gì | Các số phải thấy được |
|---|---|---|
| `anh-1.png` | Chạy nút **"② Ca #3 · bẫy 1 chỗ / 2 người"**, chụp **toàn cửa sổ** (cột trái: xung đột 1 chỗ ≠ 2 người, BM 217 bị khoá, giữ chỗ BM 201, thẻ xác nhận đổi vé) | ①②③④⑤ |
| `anh-2.png` | Chạy nút **"③ Ca #5 · hoàn vé"** → tích ô và tự gửi → rồi nút **"Ca lạ · báo đổi nhầm"**, chụp **toàn cửa sổ** (thẻ hoàn vé + màn nhân viên nhận ca) | ⑥⑦⑧ |

> **Cách chụp (30 giây):** mở `index.html` → bấm nút kịch bản ở bảng điều khiển bên phải → chụp toàn cửa sổ trình duyệt (Win+Shift+S) → lưu vào **cùng thư mục này** với đúng tên `anh-1.png`, `anh-2.png`. Trước khi chụp nhớ bật tick "Hiện số chú thích HAX/PAIR".

### Chú giải các số trên ảnh — mỗi số: thể hiện gì · nguyên tắc · mức tự chủ

| Số | Chỗ trên prototype | Thể hiện gì | Nguyên tắc HAX/PAIR | Mức tự chủ |
|---|---|---|---|---|
| ① | Dải xanh đầu khung chat "Bạn đang chat với trợ lý AI (có thể sai)… Đổi vé cần bạn bấm xác nhận · gửi hoàn vé chỉ bạn tự gửi" | Nói rõ đây là AI, làm được gì / không làm gì | G1 · Luật AI 134/2025 Đ.11 | nền |
| ② | Nhãn độ chắc (✓ / ? / ⚠ / ⛔) + dòng "Dựa vào: …" dưới mỗi câu AI | AI chắc tới đâu, dựa vào nguồn nào | G2 · PAIR Explainability + Trust | nền |
| ③ | BM 217 bị khoá 🔒 "Không chọn được — còn 1 chỗ · không đủ cho cả 2 hành khách", không có nút | Chặn tool khi dữ liệu không đủ — chặn kịch bản #3 từ gốc | G10 · PAIR Errors | cấm (chặn từ tầng chọn) |
| ④ | Giữ chỗ BM 201: đếm ngược 20:00 + nút "Nhả chỗ" | Việc AI tự làm có hoàn tác | G8 · G9 | giữ chỗ = tự làm |
| ⑤ | Thẻ "Xác nhận đổi vé": đúng chuyến, ☑ đủ 2 tên, dòng "⚠ Dùng lần đổi miễn phí duy nhất" | Bước duyệt trước việc khó đảo | G10 · G11 | đổi vé = khách xác nhận |
| ⑥ | Thẻ hoàn vé: AI chỉ soạn nháp, ô tích "tôi hiểu gửi rồi không rút lại được", nút gửi mờ tới khi khách tự bấm | Gửi hoàn vé không có trong tay AI | PAIR Errors + Graceful failure | gửi hoàn vé = cấm AI · khách tự gửi |
| ⑦ | Màn nhân viên: ca chuyển kèm tóm tắt (lý do, tin khách nguyên văn, AI đã làm / chưa làm) + nút "Nhận ca" | Đường lui luôn mở, nhân viên không hỏi lại khách | PAIR Graceful failure | chuyển nhân viên = tự làm |
| ⑧ | Link "Báo sai" dưới mỗi câu AI (sai chuyến / sai người / sai chính sách) | Mời feedback gắn với câu trả lời cụ thể | G15 | — |
