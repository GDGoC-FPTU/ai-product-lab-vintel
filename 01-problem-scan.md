# 01 — Problem Scan & Quick Cards

## Thông tin cá nhân

- Họ tên: Đoàn Minh Quang
- MSSV: 2A202600757
- Lab: AI Product Scoping - Vin Smart Future
- Mục tiêu cá nhân: tìm các bài toán vận hành/thực tế trong hệ sinh thái Vingroup trước khi nhóm chọn 1 bài để deep-dive.

---

## Phase 1 — SCAN

### Bảng quét cơ hội

| # | Subsidiary | Lens | Mô tả ngắn bài toán | Actor / Operator đang đau | Dấu hiệu thật / cách đo ban đầu |
|---|---|---|---|---|---|
| 1 | VinFast | Lặp lại, Tốn thời gian, AI-upgrade | Chủ xe VinFast khi đi đường dài phải tự kiểm tra nhiều nguồn để lập lịch trình: % pin còn lại, quãng đường, trạm sạc nên dừng, thời gian sạc và thời điểm tiếp tục di chuyển. | Chủ xe VinFast đi đường dài/đi tỉnh. | Mất khoảng 20-30 phút chuẩn bị trước chuyến đi; phải mở 3-4 nguồn/app; dễ phải đổi kế hoạch sạc giữa đường. |
| 2 | VinFast / Service Center | Lặp lại, Tốn thời gian | VinFast Service Center phải tổng hợp báo cáo hiệu suất sửa chữa từ CRM, SAP và hệ thống kỹ thuật mỗi tuần. | Quản lý vận hành Service Center. | Mất khoảng 90 phút/tuần; nhiều lần phải hỏi lại số liệu từ 3 nguồn khác nhau. |
| 3 | Vinmec | AI-upgrade, Stakeholder Pain | Người nhận kết quả xét nghiệm Vinmec khó hiểu ý nghĩa các chỉ số và không biết chỉ số nào cần hỏi bác sĩ. | Bệnh nhân/khách hàng Vinmec. | Người dùng phải tra cứu Google hoặc hỏi lại bác sĩ; dễ hiểu sai thuật ngữ y tế. |
| 4 | Vinpearl | Tốn thời gian, AI-upgrade | Khách muốn đi Vinpearl phải tự ghép phòng, vé, lịch di chuyển, dịch vụ, ngân sách và ưu đãi từ nhiều nguồn. | Khách du lịch/gia đình đặt chuyến đi Vinpearl. | Mất 30-45 phút so sánh nhiều nguồn; dữ liệu giá/phòng/vé thay đổi realtime. |
| 5 | VinID | Lặp lại, Stakeholder Pain | Người dùng VinID khó theo dõi điểm thưởng rải rác, điểm sắp hết hạn và nơi có thể dùng điểm. | Khách hàng dùng nhiều dịch vụ Vin. | Dễ bỏ lỡ điểm hết hạn; phải mở app hoặc hỏi CSKH để kiểm tra điều kiện sử dụng. |
| 6 | Vinschool | Stakeholder Pain, Tốn thời gian | Phụ huynh Vinschool nhận nhiều thông báo học tập/sự kiện/y tế nhưng khó biết việc nào cần hành động ngay. | Phụ huynh có con học Vinschool. | Mất 10-15 phút/ngày kiểm tra thông báo; có thể bỏ lỡ deadline xác nhận. |
| 7 | Vinhomes | AI-upgrade, Stakeholder Pain | Cư dân Vinhomes có yêu cầu liên quan nhiều dịch vụ không biết gửi đúng kênh nào: ban quản lý, VinFast, Vinmec, Vinschool hay CSKH chung. | Cư dân Vinhomes dùng nhiều dịch vụ Vin. | Có thể bị chuyển sai bộ phận, phải mô tả lại nhiều lần. |
| 8 | Xanh SM | Lặp lại, AI-upgrade | Tài xế Xanh SM cần gợi ý điểm đón/trả tối ưu hơn khi khu vực đông khách hoặc đường cấm/đường nhỏ. | Tài xế Xanh SM, khách đặt xe. | Tài xế phải gọi lại khách hoặc vòng xe; ảnh hưởng thời gian đón. |

---

## Phase 2 — QUICK-ASSESS

Tôi chọn 3 bài toán tiềm năng nhất để viết Quick Problem Cards:

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Chủ xe VinFast lập lịch trình đi đường dài có tính đến pin và trạm sạc. | Actor rõ, workflow hiện tại vẽ được, bottleneck cụ thể, metric đo được, phù hợp so sánh Rule / LLM / Agent. | Cần dữ liệu realtime về trạm sạc, giao thông, thời tiết và mức tiêu hao thực tế. |
| 2 | Kết quả xét nghiệm Vinmec khó hiểu. | Pain thật, AI intervention point rõ: giải thích thuật ngữ y tế bằng ngôn ngữ dễ hiểu. | Ranh giới giữa giải thích và chẩn đoán rất nhạy, cần bác sĩ/human review. |
| 3 | VinFast Service Center tổng hợp báo cáo hiệu suất sửa chữa. | Metric thời gian rõ, workflow vận hành lặp lại hằng tuần, có thể dùng Rule + LLM summary. | Cần quyền truy cập CRM, SAP và hệ thống kỹ thuật nội bộ. |

---

## Quick Problem Card #1 — VinFast long-distance route planning

| Field | Nội dung |
|---|---|
| **Tên bài toán** | Lập lịch trình đi đường dài cho chủ xe VinFast có tính đến pin và trạm sạc. |
| **Công ty thành viên** | VinFast |
| **Bài toán 1 câu** | Chủ xe VinFast khi đi đường dài phải tự kiểm tra nhiều nguồn để quyết định xe có đủ pin không, nên dừng sạc ở đâu, sạc bao lâu và đi tiếp lúc nào. |
| **Actor / Operator** | Chủ xe VinFast đi đường dài/đi tỉnh, đặc biệt là người đi tuyến mới hoặc chưa quen lập kế hoạch sạc. |
| **Workflow thủ công hiện tại** | 1. Kiểm tra % pin hiện tại trên xe/app -> 2. Nhập điểm đến trên bản đồ -> 3. Tìm trạm sạc VinFast trên hoặc gần tuyến -> 4. Tự ước lượng pin có đủ đến trạm/điểm đến không -> 5. Chọn trạm dừng -> 6. Tự tính thời gian sạc và lịch trình đi tiếp. |
| **Bước tốn thời gian/lỗi nhất** | Bước 3-6: tìm trạm, ước lượng pin và tính thời gian sạc. Ước tính 15-20 phút trong tổng 20-30 phút chuẩn bị. |
| **AI có thể hỗ trợ ở đâu** | Sau khi có điểm đến, % pin và loại xe: rule tính quãng đường/buffer/trạm khả thi; LLM giải thích 1-3 phương án lịch trình theo preference của tài xế. |
| **Metric có số** | Giảm thời gian lập kế hoạch từ 20-30 phút xuống dưới 5 phút; giảm số nguồn/app phải kiểm tra từ 3-4 xuống 1; giảm số lần đổi kế hoạch sạc giữa đường. |
| **Quick Architecture** | Rule + LLM Feature trong một workflow. Không chọn Agent ở pilot đầu vì liên quan an toàn di chuyển và dữ liệu realtime. |

### Sơ đồ quy trình thủ công hiện tại

```text
[Kiểm tra % pin: 1']
-> [Nhập điểm đến: 2-3']
-> [Tìm trạm sạc trên/gần tuyến: 5-10']  Bottleneck
-> [Ước lượng pin có đủ không: 3-5']
-> [Chọn trạm dừng: 5']
-> [Tính thời gian sạc/lịch trình: 5-10']  Bottleneck

Tổng: 20-30 phút trước chuyến đi.
```

---

## Quick Problem Card #2 — Vinmec lab result explanation

| Field | Nội dung |
|---|---|
| **Tên bài toán** | Giải thích kết quả xét nghiệm Vinmec bằng ngôn ngữ dễ hiểu. |
| **Công ty thành viên** | Vinmec |
| **Bài toán 1 câu** | Người nhận kết quả xét nghiệm Vinmec khó hiểu ý nghĩa các chỉ số và không biết chỉ số nào cần hỏi bác sĩ. |
| **Actor / Operator** | Bệnh nhân/khách hàng Vinmec nhận kết quả xét nghiệm. |
| **Workflow thủ công hiện tại** | 1. Nhận kết quả xét nghiệm -> 2. Đọc thuật ngữ/chỉ số y tế -> 3. Tự tra Google hoặc hỏi người quen -> 4. Hỏi lại bác sĩ nếu quá lo hoặc không hiểu. |
| **Bước tốn thời gian/lỗi nhất** | Bước 2-3: đọc hiểu thuật ngữ và tự diễn giải. Ước tính 15-30 phút/lần, rủi ro hiểu sai. |
| **AI có thể hỗ trợ ở đâu** | LLM giải thích thuật ngữ y tế bằng ngôn ngữ phổ thông, tóm tắt chỉ số cần chú ý và gợi ý câu hỏi nên hỏi bác sĩ. |
| **Metric có số** | Giảm thời gian đọc hiểu ban đầu từ 15-30 phút xuống dưới 5 phút; tăng tỷ lệ người dùng biết câu hỏi cần hỏi bác sĩ. |
| **Quick Architecture** | LLM Feature với boundary rất chặt: chỉ giải thích, không chẩn đoán, không khuyên điều trị, cần bác sĩ/human review với case nhạy cảm. |

### Sơ đồ quy trình thủ công hiện tại

```text
[Nhận kết quả]
-> [Đọc thuật ngữ y tế: 5-10']
-> [Tự tra cứu/diễn giải: 10-20']  Bottleneck
-> [Hỏi lại bác sĩ nếu không hiểu]

Tổng: 15-30 phút đọc hiểu ban đầu.
```

---

## Quick Problem Card #3 — VinFast Service Center weekly report

| Field | Nội dung |
|---|---|
| **Tên bài toán** | Tổng hợp báo cáo hiệu suất sửa chữa hằng tuần tại VinFast Service Center. |
| **Công ty thành viên** | VinFast |
| **Bài toán 1 câu** | Quản lý VinFast Service Center mất nhiều thời gian tổng hợp báo cáo hiệu suất sửa chữa từ CRM, SAP và hệ thống kỹ thuật. |
| **Actor / Operator** | Quản lý vận hành Service Center. |
| **Workflow thủ công hiện tại** | 1. Export dữ liệu ticket từ CRM -> 2. Lấy số liệu vật tư/chi phí từ SAP -> 3. Đọc báo cáo kỹ thuật -> 4. Ghép dữ liệu vào bảng -> 5. Viết nhận xét tuần và highlight bất thường. |
| **Bước tốn thời gian/lỗi nhất** | Bước 4-5: ghép số liệu và viết nhận xét. Ước tính khoảng 90 phút/tuần. |
| **AI có thể hỗ trợ ở đâu** | Rule/script gom dữ liệu từ các nguồn; LLM draft summary, phát hiện bất thường và tạo bản nháp báo cáo cho manager review. |
| **Metric có số** | Giảm thời gian tổng hợp từ 90 phút xuống dưới 30 phút/tuần; giảm số lần hỏi lại số liệu từ 3 nguồn xuống tối đa 1 lần. |
| **Quick Architecture** | Workflow: Rule/script + LLM summary + manager review. Chưa cần Agent vì flow báo cáo khá tuyến tính. |

### Sơ đồ quy trình thủ công hiện tại

```text
[Export CRM: 15']
-> [Lấy số SAP: 15']
-> [Đọc báo cáo kỹ thuật: 20']
-> [Ghép dữ liệu: 20']  Bottleneck
-> [Viết nhận xét tuần: 20']  Bottleneck

Tổng: khoảng 90 phút/tuần.
```
