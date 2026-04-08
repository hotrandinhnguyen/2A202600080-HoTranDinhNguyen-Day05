# NEO Vietnam Airlines

## 1. Khám phá

**Marketing:** Hỗ trợ khách hàng tìm kiếm thông tin, đặt vé, kiểm tra chuyến bay, giải đáp thắc mắc hành lý.  
Nguồn tham khảo: https://spirit.vietnamairlines.com/chuyen-dong-vna/chatbot-neo-va-hanh-trinh-nang-tam-trai-nghiem-khach-hang.html

### Dùng thử app

**a) Tìm kiếm thông tin trong khâu tự lên kế hoạch**

- Hỏi: `cho tôi thông tin chuyến bay từ Đà Nẵng đến Hà Nội hôm nay`
- Bot trả lời: đề nghị tra cứu theo `Mã đặt chỗ / Số vé` hoặc `Số hiệu chuyến bay`
- Nhận xét: người dùng đang ở giai đoạn tìm chuyến bay, tức là chưa thể biết mã đặt chỗ hay số hiệu chuyến bay. Câu trả lời này lệch với nhu cầu thật nên trải nghiệm chưa tốt.

**b) Khâu đặt vé**

- Chatbot chủ yếu trả lời theo kiểu hướng dẫn người dùng sang web hoặc trang đặt vé để tự thao tác.
- Vai trò hiện tại giống một kênh FAQ hoặc điều hướng hơn là một trợ lý thực sự làm hộ tác vụ.

**c) Khâu giải đáp thắc mắc hành lý**

- Phần này làm khá ổn.
- Người dùng hỏi chính sách hành lý thì bot có thể trả lời dựa trên rule tương đối rõ.

## 2. Phân tích 4 path cho NEO

### Path 1: Đúng

**Khi nào xảy ra**

- Câu hỏi rõ, thuộc nhóm FAQ hoặc tra cứu có cấu trúc.
- Ví dụ: `Hành lý xách tay được bao nhiêu kg?`

**User thấy gì**

- Bot trả lời đúng trọng tâm.
- Người dùng cảm thấy chatbot hữu ích vì tiết kiệm thời gian hơn việc tự tìm trong web.

**Ý nghĩa**

- Phù hợp với các tác vụ có luật rõ như hành lý, giấy tờ cần mang, tiêu chuẩn dịch vụ.

### Path 2: Không chắc

**Khi nào xảy ra**

- Ý người dùng hợp lệ nhưng câu hỏi còn mơ hồ hoặc thiếu dữ kiện.
- Ví dụ: `Tôi muốn kiểm tra chuyến bay`, `Tôi cần đổi vé`, `Chuyến đi hôm nay thế nào?`

**Vấn đề**

- Đây là chỗ dễ làm hội thoại bị gãy.
- Hiện tại NEO gần như chỉ xử lý một lượt hỏi rồi một lượt đáp, nên nếu câu đầu vào chưa rõ thì bot không dẫn dắt được user đi tiếp.
- Bot chưa thể hiện rõ khả năng hỏi lại để làm rõ ý, mà dễ trả về menu hoặc yêu cầu thông tin kỹ thuật quá sớm.

**Nên xử lý thế nào**

- Bot phải hỏi lại để làm rõ.
- Ví dụ:
  - `Anh/chị muốn tìm chuyến bay mới hay tra cứu vé đã đặt?`
  - `Anh/chị muốn tra cứu theo số hiệu chuyến bay hay theo mã đặt chỗ?`
- Sau câu hỏi làm rõ, hệ thống cần giữ được ngữ cảnh ở lượt sau để tiếp tục flow thay vì quay lại từ đầu.

**Ý nghĩa**

- NEO cần có bước disambiguation.
- Không nên đẩy user sang flow kỹ thuật khi user mới chỉ mô tả nhu cầu tự nhiên.
- Nếu không xử lý được hội thoại nhiều bước, chatbot sẽ chỉ hoạt động tốt với câu hỏi thật rõ và đúng mẫu.

### Path 3: Sai

**Khi nào xảy ra**

- Bot hiểu sai intent hoặc đẩy user vào sai flow.
- Ví dụ điển hình: user hỏi `cho tôi thông tin chuyến bay từ Đà Nẵng đến Hà Nội hôm nay` nhưng bot lại yêu cầu `Mã đặt chỗ / Số vé / Số hiệu chuyến bay`.

**Hậu quả**

- User cảm thấy bot nghe nhưng không hiểu.
- Tăng số bước thao tác.
- Khả năng rời chatbot rất cao.

**Cần sửa thế nào**

- Tách rõ 2 intent:
  - `Tìm chuyến bay mới`
  - `Tra cứu chuyến bay đã có booking`
- Nếu câu hỏi chứa `từ đâu đến đâu`, `hôm nay`, `ngày mai`, `giờ bay`, thì nên ưu tiên hiểu là nhu cầu tìm lịch bay hoặc tìm chuyến bay, không phải tra cứu booking.
- Nếu bot trả lời sai, cần cho user một cách sửa nhanh mà không phải nhập lại từ đầu.

### Path 4: Mất tin

**Khi nào xảy ra**

- Bot trả lời lạc đề nhiều lần.
- Bot chỉ dẫn link hoặc menu thay vì giải quyết việc.
- Bot phản hồi lâu.
- Bot không có streaming nên user phải chờ nguyên cụm phản hồi.
- Bot gần như chỉ có một phiên hỏi đáp duy nhất, không tạo được cảm giác hội thoại liên tục.

**Biểu hiện**

- User ngừng chat.
- User quay lại web, app khác hoặc gọi tổng đài.
- User xem chatbot chỉ là lớp chặn đầu hành trình.
- User có cảm giác hệ thống bị đơ hoặc không thật sự hiểu ngữ cảnh.

**Các lỗi hiện có**

- Phản hồi lâu: user không biết bot đang xử lý hay đang treo.
- Không có streaming: thiếu cảm giác `đang trả lời`, nên thời gian chờ khó chịu hơn.
- Chỉ có một phiên hỏi đáp duy nhất: user phải diễn đạt lại, bot không giữ được mạch hội thoại.
- Khi fail, bot thường đẩy user sang menu hoặc trang khác thay vì dẫn tiếp trong cùng flow.

**Cần có exit rõ**

- Mở đúng trang chức năng liên quan.
- Đưa nút thao tác nhanh.
- Chuyển sang hotline hoặc nhân viên.
- Gợi ý cách tự làm tiếp theo bằng ngôn ngữ thật cụ thể.
- Có trạng thái loading hoặc streaming để user biết hệ thống vẫn đang phản hồi.
- Hỗ trợ hội thoại nhiều bước và giữ ngữ cảnh ít nhất trong một task.

**Ý nghĩa**

- Trong ngành hàng không, chatbot không chỉ cần trả lời được mà còn phải giúp user hoàn thành việc hoặc thoát flow một cách an toàn.
- Một chatbot phản hồi chậm, không có streaming và không nhớ ngữ cảnh sẽ rất dễ bị đánh giá là kém thông minh dù nội dung có thể đúng.

## 3. Kết luận nhanh

- NEO hiện phù hợp hơn với vai trò FAQ và điều hướng hơn là trợ lý ảo làm hộ tác vụ.
- Điểm yếu nằm ở các tình huống user hỏi bằng ngôn ngữ tự nhiên trong giai đoạn đầu hành trình, đặc biệt là tìm chuyến bay và thao tác giao dịch.
- Ngoài lỗi hiểu sai intent, trải nghiệm hiện tại còn yếu ở chỗ phản hồi lâu, không có streaming và chưa hỗ trợ hội thoại nhiều bước.
- Muốn nâng NEO thành trợ lý ảo tốt hơn, cần tối ưu đủ 4 path:
  - Đúng: trả lời gọn và hữu ích
  - Không chắc: hỏi lại đúng chỗ và giữ ngữ cảnh
  - Sai: cho sửa nhanh
  - Mất tin: có exit rõ ràng, phản hồi nhanh hơn và hỗ trợ hội thoại liên tục
