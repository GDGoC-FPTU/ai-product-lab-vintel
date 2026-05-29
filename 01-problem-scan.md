# 01 — Problem Scan & Quick Cards

## Thông tin nhóm

- Nhóm: Vintel
- Chủ đề: Vin Smart Future - AI Product Scoping
- Hướng đào sâu: VinFast route planning cho xe điện đi đường dài

---

## Phase 1 — Scan 12 candidate problems

| # | Thành viên | Subsidiary | Lens | Mô tả ngắn bài toán | Actor đang đau | Dấu hiệu / metric ban đầu |
|---|---|---|---|---|---|---|
| 1 | Quang | VinFast | Lặp lại, Tốn thời gian, AI-upgrade | Chủ xe VinFast phải tự kiểm tra % pin, tuyến đường, trạm sạc, thời gian sạc khi đi đường dài. | Chủ xe VinFast đi tỉnh/đi xa | Mất 20-30 phút chuẩn bị, phải mở 3-4 nguồn/app. |
| 2 | Quang | Vingroup CSKH | Tốn thời gian, AI-upgrade | Nhân viên CSKH phải đọc nhiều lịch sử tương tác để hiểu khách hàng đa dịch vụ. | CSKH, khách hàng dùng nhiều dịch vụ Vin | 8-12 phút đọc context trước khi trả lời. |
| 3 | Quang | Vinschool | Stakeholder Pain | Phụ huynh khó lọc thông báo nào cần hành động ngay. | Phụ huynh Vinschool | 10-15 phút/ngày kiểm tra thông báo, dễ bỏ lỡ deadline. |
| 4 | Dương | Vinmec | AI-upgrade | Kết quả xét nghiệm Vinmec khó hiểu với người không có nền y tế. | Bệnh nhân/khách hàng Vinmec | Người dùng phải hỏi lại bác sĩ hoặc tra cứu chỉ số. |
| 5 | Dương | Vinpearl | Tốn thời gian | Khách phải tự ghép phòng, vé, lịch di chuyển, dịch vụ khi lên kế hoạch đi Vinpearl. | Khách du lịch/gia đình | Mất 30-45 phút so sánh nhiều nguồn. |
| 6 | Dương | VinID | Lặp lại | Điểm/thưởng VinID rải rác, khó biết điểm nào sắp hết hạn hoặc dùng ở đâu. | Khách hàng dùng nhiều dịch vụ Vin | Dễ bỏ lỡ điểm hết hạn, cần dữ liệu giao dịch cá nhân. |
| 7 | Lương | VinFast | Lặp lại | VinFast Service Center phải tổng hợp báo cáo hiệu suất sửa chữa từ CRM, SAP, hệ thống kỹ thuật. | Quản lý Service Center | 90 phút/tuần, hỏi lại số liệu từ 3 nguồn. |
| 8 | Lương | VinID | Tốn thời gian | CSKH VinID mất thời gian kiểm tra lịch sử điểm thưởng và điều kiện khuyến mại. | Nhân viên CSKH VinID | 15-20 phút/lần, khách chờ lâu, dễ sai rule khuyến mại. |
| 9 | Lương | Vinpearl | AI-upgrade | Quản lý VinPearl tổng hợp yêu cầu phòng/dịch vụ từ PMS, email, chat để lập kế hoạch cuối tuần. | Quản lý resort | 40 phút/buổi đọc nhiều nguồn rời rạc. |
| 10 | Đức | Nội bộ Vin Smart Future | Lặp lại | Chuẩn hóa meeting notes sau họp cross-team. | Người tham gia họp | 15-25 phút/buổi để viết notes và action items. |
| 11 | Đức | Nội bộ Vin Smart Future | Tốn thời gian | Chuyển dữ liệu Google Sheets vào slide báo cáo định kỳ. | PM, analyst | 20-30 phút format, dễ sai số. |
| 12 | Đức | Nội bộ Vin Smart Future | Stakeholder Pain | Người mới hỏi lại quy trình onboarding nội bộ cho task mới. | Intern, nhân viên mới | Hỏi 2-3 lần cùng câu, trì hoãn 10-15 phút/lần. |

---

## Phase 2 — Top 3 Quick Problem Cards

### Quick Problem Card #1 — VinFast long-distance route planning

| Field | Nội dung |
|---|---|
| **Bài toán 1 câu** | Chủ xe VinFast khi đi đường dài phải tự kiểm tra nhiều nguồn để quyết định % pin có đủ không, nên dừng sạc ở đâu, sạc bao lâu và đi tiếp lúc nào. |
| **Công ty thành viên** | VinFast |
| **Actor** | Chủ xe VinFast đi đường dài/đi tỉnh, đặc biệt là người đi tuyến mới. |
| **Workflow thủ công hiện tại** | 1. Kiểm tra % pin trên xe/app -> 2. Nhập điểm đến trên bản đồ -> 3. Tìm trạm sạc trên/gần tuyến -> 4. Tự ước lượng pin có đủ không -> 5. Chọn trạm dừng và tính thời gian sạc. |
| **Bước tốn thời gian/lỗi nhất** | Tìm trạm, ước lượng pin và tính thời gian sạc: 15-20 phút trong tổng 20-30 phút chuẩn bị. |
| **AI có thể hỗ trợ ở đâu** | Sau khi có điểm đến, % pin và loại xe: workflow/rule tính dữ liệu cứng, LLM giải thích 1-3 phương án lịch trình dễ hiểu. |
| **Metric có số** | Giảm thời gian lập kế hoạch từ 20-30 phút xuống dưới 5 phút; giảm số nguồn/app phải kiểm tra từ 3-4 xuống 1. |
| **Quick Architecture** | Workflow: Rule + LLM Feature, không chọn Agent ở pilot đầu. |

### Quick Problem Card #2 — Vinmec lab result explanation

| Field | Nội dung |
|---|---|
| **Bài toán 1 câu** | Người nhận kết quả xét nghiệm Vinmec khó hiểu ý nghĩa các chỉ số và không biết chỉ số nào cần hỏi bác sĩ. |
| **Công ty thành viên** | Vinmec |
| **Actor** | Bệnh nhân/khách hàng Vinmec nhận kết quả xét nghiệm. |
| **Workflow thủ công hiện tại** | 1. Nhận kết quả -> 2. Đọc thuật ngữ y tế -> 3. Tự tra Google/hỏi người quen -> 4. Hỏi lại bác sĩ nếu quá lo. |
| **Bước tốn thời gian/lỗi nhất** | Đọc hiểu thuật ngữ y tế và tự diễn giải: 15-30 phút/lần, dễ hiểu sai. |
| **AI có thể hỗ trợ ở đâu** | LLM giải thích thuật ngữ bằng ngôn ngữ dễ hiểu và gợi ý câu hỏi nên hỏi bác sĩ. |
| **Metric có số** | Giảm thời gian đọc hiểu ban đầu xuống dưới 5 phút; tăng tỷ lệ người dùng biết câu hỏi cần hỏi bác sĩ. |
| **Quick Architecture** | LLM Feature có human/doctor boundary rất chặt, không chẩn đoán. |

### Quick Problem Card #3 — VinFast Service Center weekly report

| Field | Nội dung |
|---|---|
| **Bài toán 1 câu** | Quản lý VinFast Service Center mất nhiều thời gian tổng hợp báo cáo hiệu suất sửa chữa từ CRM, SAP và hệ thống kỹ thuật. |
| **Công ty thành viên** | VinFast |
| **Actor** | Quản lý vận hành Service Center. |
| **Workflow thủ công hiện tại** | 1. Export CRM -> 2. Lấy số liệu SAP -> 3. Đọc báo cáo kỹ thuật -> 4. Ghép vào bảng -> 5. Viết nhận xét tuần. |
| **Bước tốn thời gian/lỗi nhất** | Ghép số liệu và viết nhận xét: khoảng 90 phút/tuần. |
| **AI có thể hỗ trợ ở đâu** | Rule/script gom dữ liệu; LLM draft summary và highlight bất thường. |
| **Metric có số** | Giảm thời gian tổng hợp từ 90 phút xuống dưới 30 phút/tuần. |
| **Quick Architecture** | Workflow: Rule/script + LLM summary + manager review. |
