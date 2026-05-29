# 01 — Problem Scan & Quick Cards

**Họ và tên:** Nguyễn Thái Dương  
**MSSV:** 2A202600823

---

## Phase 1 — Bảng quét cơ hội

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinmec** | Tốn thời gian | Nhận kết quả xét nghiệm từ Vinmec, các chỉ số dùng thuật ngữ y tế khó hiểu, phải tự tra Google từng chỉ số nhưng vẫn không chắc hiểu đúng. 20-30 phút/lần, vẫn lo lắng dù kết quả bình thường. |
| 2 | **Vinmec** | Tốn thời gian | Đặt lịch khám Vinmec phải tự chọn đúng chuyên khoa và bác sĩ dù không biết triệu chứng của mình thuộc chuyên khoa nào. 10-15 phút/lần, hay chọn nhầm chuyên khoa. |
| 3 | **Vinpearl** | Tốn thời gian | Lên kế hoạch đi Vinpearl phải tra giá phòng, vé VinWonders, nhà hàng, di chuyển từ 4-5 trang/app riêng lẻ rồi tự tổng hợp. 45-60 phút/lần, hay bỏ sót gói combo tiết kiệm hơn đặt lẻ. |
| 4 | **VinID** | Lặp lại | Điểm VinID tích lũy từ Xanh SM, WinMart, Vinmec,… nhưng không biết tổng điểm là bao nhiêu và có thể đổi gì có giá trị nhất. Điểm hay hết hạn không dùng. |
| 5 | **Xanh SM** | Lặp lại | Đặt xe Xanh SM xong phải nhìn vào app liên tục theo dõi tài xế vì ước tính thời gian đến hay sai thực tế. "3 phút" có khi thành 10 phút, phải xem màn hình liên tục khi chờ. |
| 6 | **Vinhomes** | AI có thể tốt hơn | Cư dân Vinhomes muốn báo sự cố (thang máy, điện, nước) phải gọi hotline, chờ máy, nhắc lại vấn đề, không theo dõi được tiến độ xử lý. Hotline bận giờ cao điểm, không biết sự cố đã được nhận chưa. |
| 7 | **VinFast** | Tốn thời gian | Người dùng xe VinFast muốn tìm trạm sạc trống gần nhất khi pin gần hết nhưng app không hiển thị realtime tình trạng trạm. Đến nơi rồi mới biết đầy, range anxiety khi đi đường dài. |
| 8 | **VinUni / VinSchool** | Pain từ người khác | Phụ huynh cần theo dõi thông báo từ trường nhưng thông báo đến từ nhiều kênh (app, email, Zalo, bảng tin) không tổng hợp vào một nơi. Hay bỏ sót thông báo quan trọng, phải check 3-4 nơi mỗi ngày. |
| 9 | **Vinpearl** | AI có thể tốt hơn | Sau chuyến nghỉ Vinpearl không có tóm tắt trải nghiệm và gợi ý cá nhân hóa cho lần đi tiếp dựa trên lịch sử phòng đã ở, hoạt động đã làm. Mỗi lần đặt lại từ đầu như người mới. |
| 10 | **WinMart** | Lặp lại | Mua sắm ở WinMart không biết trước sản phẩm nào đang giảm giá hôm nay, phải đi loanh quanh hoặc tra từng sản phẩm trong app. Hay bỏ sót ưu đãi ngay hôm đó. |

---

## Phase 2 — Top 3 Quick Problem Cards

**Tiêu chí chọn top 3:**

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Kết quả xét nghiệm Vinmec khó hiểu (#1) | Workflow rõ nhất; metric thời gian đo được; AI intervention point rõ (giải thích ngôn ngữ y tế, không chẩn đoán); boundary an toàn | Ranh giới "giải thích" vs "chẩn đoán" cần thiết kế rất cẩn thận |
| 2 | Lên kế hoạch đi Vinpearl (#3) | Workflow lặp lại mỗi lần đặt; metric thời gian rõ; đã từng trải qua pain này thật | Dữ liệu giá/phòng/vé thay đổi realtime, cần API sống chứ không phải dữ liệu tĩnh |
| 3 | Điểm VinID rải rác (#4) | Lặp lại thường xuyên; ảnh hưởng trực tiếp vì dùng nhiều dịch vụ Vin; metric (tỷ lệ điểm hết hạn) đo được | Cần truy cập dữ liệu giao dịch cá nhân — privacy/permission phức tạp |

---

### Quick Problem Card #1 — Kết quả xét nghiệm Vinmec khó hiểu

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Bệnh nhân nhận kết quả xét nghiệm Vinmec phải    │
│ tra Google 20-30 phút vì thuật ngữ y tế khó hiểu mà vẫn    │
│ không dám chắc mình hiểu đúng.                              │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Bệnh nhân / thân nhân nhận file kết quả xét nghiệm         │
│ từ Vinmec (qua app MyVinmec hoặc quầy lấy kết quả).        │
│                                                             │
│ Workflow thủ công hiện tại (6 bước):                        │
│   1. Nhận PDF kết quả                                       │
│   → 2. Đọc danh sách chỉ số (HbA1c, WBC, ALT,...)          │
│   → 3. Thấy chỉ số ↑↓ → lo lắng                            │
│   → 4. Tra Google từng chỉ số   ← bottleneck               │
│   → 5. Thông tin rời rạc, không nhất quán                   │
│   → 6. Vẫn không chắc → chờ gặp bác sĩ hỏi lại            │
│                                                             │
│ Bước nào tốn nhất? Bước 4-5 (⏱ 20-30 phút/lượt)           │
│ AI có thể hỗ trợ ở đâu? Bước 4-5: AI đọc file kết quả,     │
│ giải thích từng chỉ số bất thường bằng ngôn ngữ thông       │
│ thường, tạo danh sách câu hỏi nên hỏi bác sĩ.              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian "nhận kết quả → hiểu ý nghĩa cơ bản"        │
│ từ 20-30 phút ──> dưới 3 phút.                              │
│                                                             │
│ Quick Architecture: [x] Workflow (Rule + LLM Feature)       │
│ Boundary: AI không được chẩn đoán bệnh, không kết luận      │
│ tình trạng sức khỏe. Chỉ giải thích thuật ngữ + câu hỏi.   │
│ Fallback: AI không đọc được PDF → link đặt lịch tư vấn BS. │
└─────────────────────────────────────────────────────────────┘
```

---

### Quick Problem Card #2 — Lên kế hoạch đi Vinpearl

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Người muốn đi Vinpearl phải tra giá phòng, vé    │
│ VinWonders, nhà hàng và di chuyển từ 4-5 trang riêng lẻ    │
│ rồi tự tổng hợp, mất 45-60 phút và hay bỏ sót gói combo   │
│ rẻ hơn đặt lẻ.                                             │
│ Công ty thành viên: [x] Vinpearl                            │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Người dùng cá nhân / nhóm bạn muốn lên kế hoạch nghỉ       │
│ dưỡng Vinpearl Resort hoặc tham quan VinWonders.            │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Vào vinpearl.com tìm giá phòng, so sánh loại phòng    │
│   → 2. Sang vinwonders.com tìm giá vé                      │
│   → 3. Google nhà hàng + kiểm tra vé di chuyển             │
│   → 4. Tự cộng tổng chi phí thủ công   ← bottleneck       │
│   → 5. Quay lại đặt từng dịch vụ trên từng trang riêng lẻ │
│                                                             │
│ Bước nào tốn nhất? Bước 1-4 (⏱ 45-60 phút/lượt)           │
│ AI có thể hỗ trợ ở đâu? Bước 1-4: AI gom thông tin phòng,  │
│ vé, ưu đãi theo ngày, ước tính di chuyển → tổng hợp        │
│ thành 2-3 plan kèm ước tính chi phí.                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm từ 45-60 phút ──> dưới 10 phút có plan + chi phí.    │
│                                                             │
│ Quick Architecture: [x] Workflow (Rule + LLM Feature)       │
│ Boundary: Người dùng review và confirm trước khi đặt.       │
│ Fallback: Thông tin hết hạn/hết phòng → báo rõ và          │
│ chuyển đến trang đặt chính thức.                            │
└─────────────────────────────────────────────────────────────┘
```

---

### Quick Problem Card #3 — Điểm VinID rải rác không biết dùng gì

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Điểm VinID tích lũy từ Xanh SM, WinMart,        │
│ Vinmec,… nhưng người dùng không biết tổng điểm là bao       │
│ nhiêu và nên đổi thành gì phù hợp nhất với thói quen mình, │
│ dẫn đến điểm hết hạn lãng phí.                             │
│ Công ty thành viên: [x] VinID                               │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Người dùng VinID đã dùng ít nhất 2-3 dịch vụ trong hệ     │
│ sinh thái Vin và tích lũy điểm thưởng.                      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Mở app VinID                                           │
│   → 2. Kiểm tra số điểm — không rõ breakdown               │
│   → 3. Browse danh sách đổi điểm dài, không cá nhân hóa   │
│         ← bottleneck (8-10 phút)                            │
│   → 4. Không chắc chọn gì → bỏ qua hoặc chọn đại          │
│                                                             │
│ Bước nào tốn nhất? Bước 3 (⏱ 8-10 phút/lượt)              │
│ AI có thể hỗ trợ ở đâu? Bước 3: AI phân tích lịch sử dùng  │
│ dịch vụ → gợi ý top 3 cách dùng điểm phù hợp nhất          │
│ với thói quen (hay đi Xanh SM → voucher Xanh SM).           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Tăng tần suất đổi điểm từ <1 lần/quý ──> ≥1 lần/tháng.   │
│                                                             │
│ Quick Architecture: [x] Workflow (Rule + LLM Feature)       │
│ Boundary: Người dùng chọn và confirm trước khi đổi điểm.   │
│ Fallback: Không có gợi ý phù hợp → hiển thị danh sách      │
│ toàn bộ như hiện tại.                                       │
└─────────────────────────────────────────────────────────────┘
```
