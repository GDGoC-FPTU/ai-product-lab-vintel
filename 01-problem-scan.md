# 01-problem-scan.md

## Phase 1 — SCAN: Quét 5 bài toán thực tế cho Vin Smart Future

| # | Công ty thành viên | Lens | Mô tả ngắn bài toán |
|---|--------------------|------|---------------------|
| 1 | Xanh SM (GSM) | Tốn thời gian | Xử lý sự cố xe điện hết pin giữa đường: điều phối viên phải tra cứu trạm sạc và soạn hướng dẫn thủ công mất 12-15 phút. |
| 2 | VinFast | Lặp lại | So khớp và đối chiếu hóa đơn sạc điện, dữ liệu pin xe và lịch sử bảo trì hàng tuần bằng tay. |
| 3 | Vinhomes | AI-upgrade | Phân loại và trả lời phản hồi/khiếu nại cư dân trên app bằng tay, mất nhiều thời gian và phản hồi chưa sát thực tế. |
| 4 | Vinmec | Pain từ người khác | Bác sĩ mất 20-30 phút mỗi bệnh nhân để tóm tắt hồ sơ xuất viện và ghi chú điều trị bằng văn bản. |
| 5 | Vinpearl / VinWonders | AI-upgrade | Hỗ trợ đặt vé và trả lời câu hỏi thông tin du lịch qua chat của khách, hiện tại vẫn xử lý thủ công và phản hồi chậm. |

---

## Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

### QUICK PROBLEM CARD #1

Bài toán (1 câu): Tài xế Xanh SM báo xe hết pin giữa đường, điều phối viên phải tra cứu trạm sạc trống và soạn nội dung hướng dẫn bằng tay.
Công ty thành viên: [x] Xanh SM

Ai đang đau (Actor)? Điều phối viên trung tâm điều vận và tài xế đang chờ hỗ trợ.

Workflow thủ công hiện tại (3-5 bước):
  1. Tài xế báo sự cố pin qua tổng đài/ứng dụng.
  2. Điều phối viên kiểm tra vị trí xe và loại xe.
  3. Tra cứu thủ công trạm sạc VinFast còn trống phù hợp.
  4. Soạn tin nhắn hướng dẫn đường đi và gửi qua App tài xế.

Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ 12-15 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 và 4: tìm trạm phù hợp và soạn draft tin nhắn.

Đo thành công bằng gì (Metric có số)? Giảm thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút; nâng tỷ lệ đề xuất trạm đúng cổng sạc lên 98%.

Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

---

### QUICK PROBLEM CARD #2

Bài toán (1 câu): Nhân viên Vinhomes phải phân loại, gán mức ưu tiên và soạn phản hồi cho khiếu nại cư dân bằng tay.
Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)

Ai đang đau (Actor)? Nhân viên chăm sóc cư dân và cư dân mong nhận phản hồi nhanh.

Workflow thủ công hiện tại (3-5 bước):
  1. Nhận khiếu nại từ app/call center.
  2. Đọc nội dung và xác định loại vấn đề.
  3. Tìm template phản hồi phù hợp.
  4. Soạn và gửi lại cư dân.

Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 10-12 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3: phân loại nội dung và đề xuất phản hồi.

Đo thành công bằng gì (Metric có số)? Giảm thời gian xử lý phản hồi từ 12 phút xuống dưới 4 phút; tăng tỷ lệ phản hồi đúng loại lên 95%.

Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent

---

### QUICK PROBLEM CARD #3

Bài toán (1 câu): Bác sĩ Vinmec dành nhiều thời gian viết tóm tắt xuất viện và kết luận điều trị cho hồ sơ bệnh án.
Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  [x] Vinmec  [ ] Khác (Ghi rõ)

Ai đang đau (Actor)? Bác sĩ khám chữa bệnh và nhân viên hồ sơ y tế.

Workflow thủ công hiện tại (3-5 bước):
  1. Bác sĩ đọc hồ sơ bệnh án và chẩn đoán.
  2. Ghi tay tóm tắt xuất viện.
  3. Kiểm tra lại nội dung và sửa lỗi ngôn ngữ.
  4. Lưu hồ sơ vào hệ thống.

Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 20-30 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Tự động tóm tắt và chuẩn hóa văn bản.

Đo thành công bằng gì (Metric có số)? Giảm thời gian soạn tóm tắt từ 25 phút xuống dưới 7 phút; đạt độ chính xác y khoa 98%.

Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent
