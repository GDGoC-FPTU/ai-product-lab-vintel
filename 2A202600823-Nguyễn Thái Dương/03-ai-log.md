# 03 — AI Log & Reflection

**Họ và tên:** Nguyễn Thái Dương  
**MSSV:** 2A202600823

---

## AI giúp gì trong buổi lab?

**Scan và brainstorm candidate:**  
Tôi dùng AI để mở rộng danh sách bài toán từ góc nhìn người dùng hệ sinh thái Vin. Ban đầu tôi chỉ nghĩ đến bài Vinmec vì đã trải qua pain đó thật. AI giúp gợi ý thêm các pattern tương tự ở Vinpearl (lên kế hoạch từ nhiều nguồn) và VinID (loyalty không cá nhân hóa), từ đó tôi có đủ 3 candidate để pitch.

**Viết và phản biện Problem Card:**  
Tôi dán nội dung Problem Card #1 (Vinmec) vào AI và yêu cầu AI đóng vai CFO/trưởng vận hành khó tính, chỉ ra điểm yếu. AI đặt câu hỏi: metric "dưới 3 phút" có baseline chưa, và tại sao rule-based glossary file kèm PDF không đủ? Những câu hỏi này buộc tôi bổ sung Non-AI alternative và làm rõ lý do cần LLM (cá nhân hóa theo từng kết quả, không phải glossary chung).

**Challenge bài của bạn khác:**  
Tôi dùng AI gợi ý câu hỏi phản biện cho bài VinFast route planning của Quang: dữ liệu trạm sạc có realtime không, nếu AI gợi ý sai trạm sạc thì fallback là gì. Nhóm sau đó bổ sung boundary rõ hơn cho bài VinFast.

**So sánh mức giải pháp (Rule / Workflow / Agent):**  
Khi nhóm thảo luận kiến trúc cho bài VinFast, tôi hỏi AI: "Với quy trình có cấu trúc cố định và rủi ro khi AI sai cao, tại sao Workflow đủ dùng mà không cần Agent?" AI giải thích rõ sự khác biệt và nhóm thống nhất chọn Workflow.

---

## AI sai / hời hợt ở đâu?

**AI viết metric quá chung:**  
Khi tôi hỏi AI metric nào phù hợp cho bài Vinmec, AI trả lời "cải thiện trải nghiệm người dùng" và "tăng sự hài lòng" — không có con số. Tôi phải tự chuyển thành metric đo được: giảm từ 20-30 phút xuống dưới 3 phút; giảm tần suất bác sĩ phải giải thích lại từng chỉ số thông thường.

**AI đề xuất scope quá rộng cho bài Vinmec:**  
AI ban đầu gợi ý tính năng "AI tư vấn sức khỏe tổng thể dựa trên lịch sử xét nghiệm nhiều năm". Đây là scope Agent, vượt ranh giới an toàn trong lab. Tôi thu hẹp lại: AI chỉ giải thích kết quả hiện tại, không lưu lịch sử, không chẩn đoán, không khuyên điều trị.

**AI đôi khi chọn bài "ngầu" hơn thay vì bài có thể làm được:**  
Khi tôi hỏi AI so sánh bài Vinmec với bài VinFast để nhóm chọn, AI có xu hướng thiên về Vinmec vì "AI giải thích y tế nghe thú vị hơn". Tôi phải tự đặt lại tiêu chí: bài nào có thể pilot trong lab, đo được metric trong thời gian ngắn, và ít rủi ro chuyên môn hơn — kết quả là VinFast phù hợp hơn cho lab.

**AI không tự nhận ra nguồn không đủ để validate:**  
Khi tôi hỏi AI về pain của người dùng Vinmec với kết quả xét nghiệm, AI đưa ra số liệu chung về "80% bệnh nhân không hiểu kết quả xét nghiệm". Tôi không dùng số này trong báo cáo vì không có nguồn xác thực — chỉ dùng làm bối cảnh tham khảo.

---

## Sửa lại như thế nào?

Với bài Vinmec, tôi giữ scope hẹp: AI chỉ giải thích thuật ngữ trong file kết quả hiện tại, không chẩn đoán, không lưu lịch sử, bác sĩ là người đưa ra kết luận cuối cùng. Boundary này rõ hơn nhiều so với scope AI đề xuất ban đầu.

Với metric, tôi đặt câu hỏi lại cho AI: "Nếu phải đo bằng 1 con số duy nhất sau 2 tuần pilot, bạn sẽ đo gì?" Cách hỏi này ép AI ra số cụ thể thay vì câu định tính.

Với quyết định chọn bài nhóm, tôi không dùng AI để quyết định mà dùng scorecard tự điền với tiêu chí rõ: workflow rõ, metric đo được trong lab, ít rủi ro boundary, có thể pilot được. AI chỉ làm input brainstorm, quyết định cuối là của nhóm.

---

## Điều học được

Dùng AI như thought-partner hiệu quả nhất khi mình biết mình cần gì. AI giỏi mở rộng ý tưởng và đặt câu hỏi phản biện, nhưng không đáng tin với metric cụ thể hay số liệu về hệ sinh thái Vin. Câu hỏi "Nếu rule-based đã đủ, tại sao cần LLM?" là câu hỏi quan trọng nhất trong buổi lab — AI trả lời câu này tốt và giúp nhóm tránh dùng LLM cho bài toán thực ra chỉ cần filter/sort.
