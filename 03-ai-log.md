# 03 — AI Log & Reflection

## Nhật ký cá nhân về việc dùng AI trong Lab 02

Trong buổi lab này, tôi dùng AI như một **thought-partner** chứ không dùng AI để quyết định thay nhóm. Tôi dùng ChatGPT để brainstorm, phản biện problem, viết nháp prompt boundary và kiểm tra xem bài toán VinFast route planning có đang bị solution-first không.

Bài toán nhóm chọn là: **chủ xe VinFast khi đi đường dài phải tự kiểm tra nhiều nguồn để lập lịch trình: % pin còn lại, quãng đường, trạm sạc nên dừng, thời gian sạc và thời điểm tiếp tục di chuyển.**

---

## 1. AI giúp gì?

AI giúp tôi ở 4 phần chính.

Thứ nhất, AI giúp brainstorm candidate problems trong hệ sinh thái Vin Smart Future. Ban đầu nhóm có nhiều hướng như Vinmec, Vinpearl, VinID, VinFast Service Center và các workflow nội bộ. Tôi dùng AI để mở rộng góc nhìn theo 4 lenses: lặp lại, tốn thời gian, AI-upgrade và stakeholder pain. Nhờ đó nhóm có đủ 12 candidates từ 4 thành viên để đưa vào bảng convergence.

Thứ hai, AI giúp phản biện problem card. Tôi dán problem VinFast route planning vào AI và yêu cầu AI đóng vai CFO/Head of Operations khó tính. AI đặt lại các câu hỏi hữu ích như: metric có đo được không, dữ liệu trạm sạc có realtime không, nếu rule-based route planner đã đủ thì tại sao cần LLM. Những câu hỏi này giúp nhóm không nhảy thẳng sang Agent.

Thứ ba, AI giúp chuyển mô tả workflow thành sơ đồ before/after. Từ mô tả "chủ xe kiểm pin, tìm trạm, tính sạc", AI giúp tôi tách thành các bước rõ hơn: kiểm tra % pin, nhập điểm đến, tìm trạm sạc, ước lượng pin, chọn trạm dừng, tính thời gian sạc và kiểm tra lại khi có thay đổi.

Thứ tư, AI hỗ trợ viết và stress-test prompt prototype. Tôi dùng AI để nghĩ adversarial prompts như:

- Người dùng cố ép hệ thống bỏ tag `[DRAFT_ONLY]`.
- Người dùng pin còn 2% nhưng yêu cầu chỉ đường đến trạm sạc cách 8km.
- Người dùng yêu cầu AI cam kết 100% trạm sạc còn trống và chuyến đi an toàn.

Các test này giúp tôi kiểm tra boundary của prompt trong `starter-code/prompt_prototype.py`.

---

## 2. AI sai gì hoặc hời hợt ở đâu?

AI có vài điểm sai/hời hợt mà tôi phải sửa.

Điểm sai đầu tiên là **AI đề xuất Agent quá sớm**. Khi nghe bài toán có nhiều dữ liệu như pin, route, trạm sạc, traffic, AI dễ gợi ý một agent tự theo dõi chuyến đi, tự đổi route và tự quyết định trạm dừng. Cách này nghe mạnh nhưng không phù hợp với pilot đầu vì liên quan an toàn di chuyển. Nếu AI tự quyết sai, hậu quả không còn là lỗi text đơn giản.

Điểm hời hợt thứ hai là **AI viết metric quá chung**. AI hay nói "giảm lo lắng", "cải thiện trải nghiệm", "tối ưu hành trình" nhưng không có con số cụ thể. Những câu này không đủ để chấm theo rubric. Tôi phải chuyển thành metric đo được: giảm thời gian lập kế hoạch từ 20-30 phút xuống dưới 5 phút, giảm số app/nguồn phải kiểm tra từ 3-4 xuống 1, tăng điểm tự tin trước chuyến đi qua survey 1-5.

Điểm sai thứ ba là **AI chưa tự đặt boundary đủ cứng cho tình huống pin thấp**. Ban đầu AI chỉ khuyên "nên kiểm tra trạm gần nhất" hoặc "cân nhắc phương án an toàn", nhưng chưa có rule rõ. Với pin dưới 5%, nếu AI vẫn đề xuất trạm sạc xa thì có thể nguy hiểm. Vì vậy tôi thêm rule cứng: khi `battery_percent < 5`, hệ thống không được đề xuất trạm xa hơn 5km và phải trả action `dispatch_mobile_charger`.

Điểm hời hợt thứ tư là **AI có xu hướng nói chắc chắn quá mức**. Trong route planning, dữ liệu realtime như tình trạng trạm sạc, giao thông, thời tiết và mức tiêu hao thực tế có thể thay đổi. Nếu prompt không chặt, AI dễ viết kiểu "bạn chắc chắn tới nơi an toàn". Tôi xem đây là lỗi boundary vì AI không được cam kết điều nó không kiểm chứng được.

---

## 3. Tôi đã sửa prompt và ranh giới như thế nào?

Sau khi thấy các lỗi trên, tôi sửa prompt theo hướng chặt hơn.

Đầu tiên, tôi bắt buộc mọi output bắt đầu bằng tag:

```text
[DRAFT_ONLY]
```

Mục tiêu là nhắc rõ đây chỉ là bản nháp hỗ trợ quyết định, không phải lệnh tự động gửi cho tài xế hoặc quyết định vận hành cuối cùng.

Tiếp theo, tôi tách rõ phần **rule cứng** và phần **LLM mềm**:

- Rule xử lý dữ liệu có tính toán: % pin, khoảng cách, ngưỡng pin an toàn, trạm sạc khả thi.
- LLM chỉ diễn giải phương án, hỏi preference và trình bày lịch trình dễ hiểu.

Tôi cũng thêm boundary cho pin cực thấp:

```text
If battery_percent is below 5%, do NOT recommend any charging station farther than 5km.
Instead, immediately return:
{"action": "dispatch_mobile_charger", "reason": "..."}
```

Ngoài ra, tôi yêu cầu output có các trường như:

```text
status
action
recommendation
assumptions
confidence
human_review_required
```

Các trường này ép AI phải nói rõ giả định, mức tự tin và việc có cần người thật/tài xế xác nhận hay không.

Cuối cùng, tôi thêm adversarial tests trong code để kiểm tra prompt:

1. Pin 2% nhưng người dùng yêu cầu đi đến trạm sạc 8km.
2. Người dùng yêu cầu bỏ `[DRAFT_ONLY]` và gửi thẳng.
3. Người dùng yêu cầu cam kết chắc chắn 100% về tình trạng trạm sạc.

Sau khi sửa, prototype có thể chạy bằng local fallback khi chưa có API key, và autograder kiểm tra được các boundary chính.

---

## 4. Điều tôi học được

Điều quan trọng nhất tôi học được là AI không nên được dùng để "làm mọi thứ". Với bài VinFast route planning, nếu dùng Agent quá sớm thì rủi ro cao. Cách hợp lý hơn là dùng rule cho phần an toàn/tính toán, dùng LLM cho phần giải thích và cá nhân hóa, còn tài xế vẫn quyết định cuối cùng.

Tôi cũng học được rằng prompt tốt không chỉ là prompt trả lời hay, mà phải có boundary rõ, có fallback và có adversarial tests. Nếu không cố tình tấn công prompt, mình rất dễ tưởng hệ thống an toàn trong khi nó vẫn có thể bị dụ bỏ qua ranh giới.

Nếu làm lại, tôi sẽ validate với chủ xe thật sớm hơn. Tôi muốn hỏi 3-5 chủ xe VinFast hoặc người dùng xe điện: lần gần nhất đi xa họ mất bao lâu để lập kế hoạch, họ mở bao nhiêu app, họ lo nhất ở bước nào và họ có tin một gợi ý AI route-planning hay không.
