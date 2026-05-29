# 02 — Deep-Dive Report

## Nhóm và thành viên

- Nhóm: Vintel
- Chủ đề: Vin Smart Future - AI Product Scoping
- Thành viên:
  - Đoàn Minh Quang - 2A202600757
  - Nguyễn Thái Dương - 2A202600823
  - Trần Đức Lương - 2A202600881
  - Hồ Thái Đức - 2A2026968

---

## Quyết định lựa chọn

Nhóm chọn bài toán:

```text
Chủ xe VinFast khi đi đường dài phải tự kiểm tra nhiều nguồn để lập lịch trình: % pin còn lại, quãng đường, trạm sạc nên dừng, thời gian sạc và thời điểm tiếp tục di chuyển.
```

Lý do chọn:

- Actor rõ và dễ mô tả: chủ xe VinFast đi đường dài/đi tỉnh.
- Workflow hiện tại có thể vẽ được theo từng bước.
- Bottleneck cụ thể: ghép pin, tuyến đường, trạm sạc, thời gian sạc và buffer an toàn.
- Metric có số: thời gian lập kế hoạch, số nguồn/app phải kiểm tra, số lần đổi kế hoạch.
- Ít rủi ro hơn bài Vinmec vì không chạm chẩn đoán y tế.
- Ít phụ thuộc hệ thống nội bộ hơn bài Service Center CRM/SAP.

---

## Group Convergence từ 12 candidates

| # | Người đưa ra | Candidate problem | Người gặp vấn đề | Điểm nghẽn | Kết quả |
|---|---|---|---|---|---|
| 1 | Quang | Chủ xe VinFast lập lịch trình sạc đường dài | Chủ xe VinFast | Tự ghép pin, route, trạm sạc, thời gian dừng | Chọn |
| 2 | Quang | CSKH đọc context khách hàng đa dịch vụ | CSKH | Dữ liệu khách rải rác | Không chọn vì data access |
| 3 | Quang | Phụ huynh Vinschool lọc thông báo | Phụ huynh | Thông báo nhiều, khó biết action | Không chọn vì privacy trẻ em |
| 4 | Dương | Kết quả xét nghiệm Vinmec khó hiểu | Bệnh nhân | Ngôn ngữ y tế khó hiểu | Shortlist nhưng rủi ro y tế cao |
| 5 | Dương | Lên kế hoạch đi Vinpearl | Khách du lịch | Ghép phòng, vé, lịch, dịch vụ | Shortlist nhưng cần dữ liệu realtime |
| 6 | Dương | Điểm VinID rải rác | Khách hàng VinID | Theo dõi điểm/hạn dùng | Không chọn vì dữ liệu cá nhân |
| 7 | Lương | Service Center tổng hợp báo cáo sửa chữa | Quản lý Service Center | CRM/SAP/kỹ thuật rời rạc | Shortlist nhưng khó access data |
| 8 | Lương | CSKH VinID kiểm tra điểm và khuyến mại | CSKH VinID | Tra rule và lịch sử thủ công | Không chọn vì privacy/permission |
| 9 | Lương | VinPearl tổng hợp yêu cầu phòng/dịch vụ | Quản lý resort | PMS/email/chat rời rạc | Không chọn vì data nội bộ |
| 10 | Đức | Chuẩn hóa meeting notes | Người họp | Viết notes thủ công | Không chọn vì ít đặc thù Vin |
| 11 | Đức | Sheets to slides định kỳ | PM/analyst | Format, kiểm số liệu | Không chọn vì automation phổ biến |
| 12 | Đức | Hỏi lại onboarding nội bộ | Intern/người mới | Quy trình khó tìm | Không chọn vì scope chung |

Shortlist và score:

| Candidate | Actor rõ | Workflow rõ | Impact đo được | Làm trong lab | AI fit rõ | Rủi ro boundary thấp | Tổng |
|---|---:|---:|---:|---:|---:|---:|---:|
| VinFast route planning | 5 | 5 | 5 | 5 | 5 | 4 | 29 |
| Vinmec lab result explanation | 5 | 5 | 5 | 4 | 5 | 2 | 26 |
| VinFast Service Center report | 5 | 5 | 5 | 3 | 5 | 4 | 27 |
| Vinpearl trip planning | 5 | 5 | 4 | 4 | 4 | 3 | 25 |

---

## 3.1 Current-State Workflow Mapping

```text
CURRENT STATE — khoảng 20-30 phút lập kế hoạch trước chuyến đi

[1. Chủ xe kiểm tra % pin hiện tại trên xe/app: 1']
  Handoff: xe/app -> người lái
    ↓
[2. Nhập điểm đến trên bản đồ để xem quãng đường/thời gian: 2-3']
  Handoff: app bản đồ -> người lái
    ↓
[3. Tìm trạm sạc VinFast trên hoặc gần tuyến đường: 5-10'] Bottleneck
  Handoff: app/trang trạm sạc -> người lái
    ↓
[4. Tự ước lượng pin có đủ đến trạm/điểm đến không: 3-5']
    ↓
[5. Chọn trạm dừng dựa trên khoảng cách, vị trí, tiện ích: 5']
    ↓
[6. Tự tính thời gian sạc và lịch trình đi tiếp: 5-10'] Bottleneck
    ↓
[7. Kiểm tra lại khi pin/giao thông/trạm sạc thay đổi trên đường]

Tổng cộng: 20-30 phút trước chuyến đi, chưa tính thời gian đổi kế hoạch giữa đường.
```

---

## 3.2 Problem Statement 6-field

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Chủ xe VinFast đi đường dài/đi tỉnh, đặc biệt là người chưa quen tuyến hoặc chưa quen lập kế hoạch sạc. |
| **2. Current Workflow** | Kiểm tra % pin -> nhập điểm đến -> xem tuyến đường -> tìm trạm sạc -> ước lượng có đủ pin không -> chọn trạm dừng -> tính thời gian sạc -> điều chỉnh khi có thay đổi. |
| **3. Bottleneck** | Bước tìm trạm sạc, ước lượng pin và tính lịch trình sạc mất thời gian vì chủ xe phải tự ghép nhiều nguồn dữ liệu. |
| **4. Business Impact** | Mất 20-30 phút lập kế hoạch; phải kiểm tra 3-4 nguồn/app; tăng lo lắng khi đi xa; dễ đổi kế hoạch giữa đường. Điều này ảnh hưởng trực tiếp đến trải nghiệm xe điện VinFast. |
| **5. Success Metric** | Giảm thời gian lập kế hoạch xuống dưới 5 phút; giảm số nguồn/app phải kiểm tra từ 3-4 xuống 1; giảm số lần đổi kế hoạch sạc giữa đường; tăng điểm tự tin trước chuyến đi qua survey 1-5. |
| **6. Operational Boundary** | AI không tự quyết định thay tài xế, không cam kết tuyệt đối tình trạng trạm/giao thông/pin, không che giấu độ không chắc chắn, phải có fallback an toàn. Nếu pin dưới 5%, không đề xuất trạm xa hơn 5km mà trigger `dispatch_mobile_charger`. |

---

## 3.3 Future-State Flow & AI Fit

AI Fit:

```text
Chọn: Workflow = Rule / State-Machine + LLM Feature.
Không chọn Agentic Loop ở pilot đầu.
```

Future-state flow:

```text
FUTURE STATE — dưới 5 phút để có lịch trình sạc ban đầu

[1. Chủ xe nhập điểm đến / chọn lịch trình]
    ↓
[2. App lấy % pin, loại xe và dữ liệu tuyến đường]
    ↓
[3. Rule tính ngưỡng pin an toàn, trạm khả thi, buffer]
    ↓
[4. LLM Step: diễn giải 1-3 phương án lịch trình]
    - Nhanh nhất
    - An toàn pin nhất
    - Ít điểm dừng nhất
    ↓
[5. Human Step: tài xế chọn phương án cuối cùng]
    ↓
[6. App theo dõi pin thực tế và nhắc khi cần điều chỉnh]
    ↓
[Fallback]
    - Nếu pin < 5%: dispatch_mobile_charger
    - Nếu dữ liệu trạm không chắc: chọn trạm gần hơn, buffer pin cao hơn
    - Nếu LLM không tự tin: hiển thị rule-based route và yêu cầu tài xế kiểm tra lại
```

So sánh mức giải pháp:

| Mức | Phương án | Khi nào đủ | Rủi ro | Chọn? |
|---|---|---|---|---|
| No AI | Checklist trước chuyến đi, danh sách trạm sạc | Đủ cho người đi xa ít và đã quen | Vẫn bắt người dùng tự ghép dữ liệu | Không |
| Rule | Tính quãng đường, buffer pin, trạm gần tuyến | Đủ cho case đơn giản | Khó giải thích/cá nhân hóa preference | Dùng làm nền |
| LLM Feature | Diễn giải phương án, hỏi preference, trình bày lịch trình dễ hiểu | Phù hợp vì output là tư vấn hỗ trợ quyết định | Có thể nói quá chắc nếu prompt yếu | Chọn |
| Agentic Loop | Tự đổi route, tự chọn trạm, tự ra quyết định trong chuyến đi | Chỉ phù hợp khi có API realtime rất tin cậy và quyền rõ | Rủi ro an toàn, trách nhiệm pháp lý | Chưa chọn |

---

## Phase 5 — Evaluate

### AI Readiness Checklist

| Câu hỏi | Trạng thái | Ghi chú |
|---|---|---|
| Có sẵn dữ liệu mẫu/log sạch để test? | Not Yet | Cần dữ liệu tuyến đường, trạm sạc, % pin, loại xe. |
| Rủi ro khi AI sai có kiểm soát được không? | Yes, nếu giới hạn scope | AI chỉ đề xuất; tài xế quyết định; có fallback rule. |
| Stakeholder sẵn sàng đổi workflow cũ? | Likely | Nếu giảm được thời gian lập kế hoạch và tăng tự tin trước chuyến đi. |
| Có metric baseline chưa? | Not Yet | Cần phỏng vấn/mô phỏng ít nhất 3-5 chuyến đi. |
| Có non-AI alternative không? | Yes | Rule route planner là nền bắt buộc. |

### Quyết định cuối cùng

```text
NOT YET -> GO pilot nhỏ.
```

Justification:

```text
Bài toán rõ, workflow rõ và phù hợp với Workflow/LLM Feature. Tuy nhiên chưa nên Go production vì nhóm chưa có dữ liệu realtime về trạm sạc, traffic và mức tiêu hao thực tế. Pilot nhỏ có thể bắt đầu với 2-3 tuyến đường phổ biến, dữ liệu mẫu và human review.
```

Pilot nhỏ nhất:

1. Chọn 2-3 tuyến phổ biến, ví dụ Hà Nội - Hạ Long, Hà Nội - Ninh Bình, TP.HCM - Vũng Tàu.
2. Thu input mẫu: loại xe, % pin xuất phát, điểm đi, điểm đến, mức pin an toàn mong muốn.
3. Rule tính trạm khả thi và buffer pin.
4. LLM diễn giải 1-3 phương án: nhanh nhất, an toàn nhất, ít dừng nhất.
5. 3-5 chủ xe/xe điện đánh giá phương án.
6. Đo: thời gian lập kế hoạch, số nguồn phải kiểm tra lại, tỷ lệ phương án được chấp nhận.

Ước lượng chi phí pilot:

- 1 kỹ sư backend/prompt prototype: 1-2 ngày.
- 1 product/ops researcher phỏng vấn và đo baseline: 1 ngày.
- Dữ liệu ban đầu: có thể dùng tuyến/trạm mẫu đã ẩn thông tin realtime.
- Chi phí API LLM ở pilot thấp vì chỉ test vài chục case.
