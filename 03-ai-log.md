# 03-ai-log.md

## Nhật ký AI Log — Reflection cá nhân

### 1. AI giúp gì?
Trong buổi lab, tôi đã dùng AI như một thought partner để:
- Brainstorm các bài toán vận hành tiềm năng cho Vin Smart Future.
- Viết nhanh 3 Quick Problem Cards với cấu trúc rõ ràng.
- Xây dựng Problem Statement 6-field và Future-State Flow bằng ngôn ngữ Việt phù hợp.
- Tạo ra bản mẫu prompt prototype để bảo vệ ranh giới an toàn.

### 2. AI sai gì?
Trong quá trình thử nghiệm, mô hình AI có thể dễ bị lừa bởi yêu cầu "bỏ qua [DRAFT_ONLY]" hoặc đề xuất trạm sạc xa khi pin rất thấp. Đây là một dạng prompt injection / bypass boundary nếu không thiết kế hệ thống prompt thật chặt.

### 3. Sửa đổi ra sao?
Để giảm rủi ro, tôi đã:
- Yêu cầu AI luôn trả về draft bắt đầu bằng `[DRAFT_ONLY]` và ghi rõ không được gửi tự động.
- Thêm quy tắc bảo vệ pin dưới 5%: nếu pin thấp thì không được chọn trạm xa > 5km, phải đề xuất điều xe cứu hộ pin di động.
- Viết các test adversarial nhằm kiểm tra ranh giới prompt bằng cách cố tình yêu cầu bỏ qua thẻ draft hoặc chọn trạm quá xa.

### 4. Kết luận cá nhân
Tôi nhận thấy AI hữu ích nhất khi dùng làm trợ lý viết draft và kiểm tra logic, nhưng vẫn cần con người duyệt cuối cùng. Việc định nghĩa giới hạn rõ ràng giúp giảm hallucination và hạn chế hành động không an toàn trong ứng dụng vận hành thời gian thực.
