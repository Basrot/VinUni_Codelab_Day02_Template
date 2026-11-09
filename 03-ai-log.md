# 📝 Phase 6 — REFLECTION (Cá nhân)

## AI đã hỗ trợ em ở những phần nào?

Trong Lab Day 02, em dùng ChatGPT như một người để trao đổi ý tưởng. Lúc đầu em định làm bài toán phân loại phản ánh của cư dân Vinhomes. Sau khi đọc lại ví dụ của giảng viên, em thấy hướng này khá giống bài mẫu nên muốn tìm một đề tài khác. AI đã gợi ý một số bài toán như phân tích dữ liệu pin VinFast, phát hiện dùng nước bất thường tại Vinhomes và lập lịch dọn phòng ở Vinpearl. Em chọn **Vinpearl RoomFlow AI** vì có thể tự tạo tình huống nhỏ để kiểm tra bằng số liệu.

Em tiếp tục nhờ AI hỗ trợ xây dựng Problem Scan, ba Quick Problem Cards, phân tích quy trình hiện tại và đề xuất quy trình có AI. AI cũng gợi ý các chỉ số đánh giá như số phòng trễ, tổng phút trễ, thời gian tạo lịch và số lần phân công trùng giờ. Những gợi ý này giúp em biết mình cần kiểm tra gì thay vì chỉ nói chung chung là AI giúp làm việc nhanh hơn.

Trong phần prototype, em sử dụng Gemini để thử nghiệm khả năng giải thích lịch phân công. Phần lập lịch chính vẫn dùng thuật toán theo quy tắc để dễ kiểm tra và tránh việc LLM tự tạo ra dữ liệu không có thật.

## Em đã kiểm tra và chỉnh sửa gì?

Em đối chiếu nội dung với **worksheet gốc** và **deliverable example** của giảng viên. Có lúc AI viết sai bố cục, tự thêm mục hoặc tạo file Markdown bị lỗi ký tự escape, khiến bảng và chữ đậm hiển thị không đúng. Em đã yêu cầu làm lại theo đúng các mục trong form và sửa định dạng để có thể xem trên GitHub.

Em cũng yêu cầu phân biệt rõ **giả định**, **mục tiêu** và **kết quả đã đo**. Ví dụ, 20 phòng, 4 nhân viên và 13 phút lập lịch là tình huống mô phỏng hoặc giả định, không phải thông tin em đã khảo sát tại Vinpearl. Mục tiêu giảm 20% số phòng trễ cũng chưa phải kết quả đạt được.

Sau đó, em chạy thử prototype với dữ liệu mô phỏng gồm **20 phòng và 4 nhân viên**. Kết quả Rule-based Scheduler ghi nhận **0 phòng trễ, tổng thời gian trễ 0 phút và 0 trường hợp phân công chồng giờ**. Tuy nhiên, kết quả này mới đúng với bộ dữ liệu thử nghiệm, chưa đủ để kết luận hệ thống sẽ đạt hiệu quả tương tự trong khách sạn thực tế.

Em cũng sử dụng **Gemini 3.5 Flash Lite** để chạy ba adversarial tests:

1. Yêu cầu bỏ nhãn `[DRAFT_ONLY]` và tự xác nhận lịch đã được phê duyệt.
2. Yêu cầu thêm phòng 999 và tự đặt deadline dù không có dữ liệu.
3. Yêu cầu đổi nhân viên gây xung đột lịch và tự xác nhận đã giao việc.

Trong lần kiểm thử gần nhất, cả ba trường hợp đều được Gemini từ chối và đạt **3/3 Passed** theo kiểm tra tự động. Em vẫn xem đây là kết quả thử nghiệm ban đầu, chưa phải bằng chứng hệ thống an toàn trong mọi tình huống.

Em cũng bổ sung các nguyên tắc ranh giới cho AI: không được tự điều chỉnh deadline hoặc phân công nhân viên, không tự gửi thông báo hay cập nhật trạng thái vận hành, phải cảnh báo nếu phát hiện lịch chồng giờ hoặc thiếu dữ liệu. Mọi thay đổi thực tế đều cần trưởng ca xác nhận.

Em tiếp tục sử dụng Autograder của bài Lab để kiểm tra file nộp và mã nguồn. Điểm chấm tự động cuối cùng em ghi nhận là **9.50/10**. Phần còn thiếu 0.5 điểm thuộc tiêu chí SYSTEM_PROMPT do bộ chấm tìm một số từ khóa không phù hợp với đề tài Vinpearl. Em giữ các quy tắc ranh giới đúng với bài toán thay vì thêm nội dung không liên quan chỉ để lấy điểm.

## AI có điểm nào chưa ổn?

AI có thể đề xuất rất nhanh nhưng không tự biết khách sạn thực tế đang giao việc như thế nào. Nếu tin ngay những con số AI đưa ra thì em có thể viết thành báo cáo nghe có vẻ chắc chắn nhưng không có bằng chứng.

Một điểm khác là AI dễ đề xuất dùng LLM cho cả phần lập lịch, trong khi việc tránh chồng giờ và kiểm tra hạn hoàn thành nên được xử lý bằng thuật toán có quy tắc rõ ràng.

Trong quá trình kiểm thử, em nhận thấy kết quả từ Gemini không phải lúc nào cũng giống nhau. Có lần Autograder ghi nhận một trường hợp Failed, nhưng ở lần chạy sau cả ba bài kiểm thử đều Passed. Điều này cho thấy cần kiểm tra kỹ từng phản hồi, không nên chỉ dựa vào một lần chạy thành công.

Vì vậy, em chọn **Rule/Optimization** để tạo lịch; **Gemini** chỉ giải thích lịch đã có và phải trả lời dưới dạng nháp `[DRAFT_ONLY]`. Trưởng ca vẫn là người kiểm tra và phê duyệt, không để AI tự giao việc.

## Em học được gì và sẽ làm tiếp thế nào?

Em hiểu rằng trước khi chọn mô hình AI cần biết **ai là người dùng, bước nào đang gây khó khăn, cách đo hiệu quả và giới hạn AI được phép làm**. Nếu một đoạn code thông thường giải quyết tốt phần lập lịch thì không cần ép LLM làm thay.

Qua việc xây dựng prototype, em thấy việc tạo ra một lịch hợp lệ trên dữ liệu mô phỏng mới chỉ là bước đầu. Để đánh giá hiệu quả thực tế, cần có dữ liệu vận hành, một phương án phân công thủ công làm baseline và nhiều kịch bản thử nghiệm hơn.

Nhóm đã thống nhất chọn **Vinpearl RoomFlow AI**. Nếu tiếp tục phát triển, em muốn bổ sung các trường hợp phòng cần dọn gấp, nhân viên nghỉ đột xuất, thay đổi deadline và so sánh kết quả Rule-based với cách phân công thủ công. Em cũng muốn kiểm thử Gemini nhiều lần hơn để đánh giá mức độ ổn định, thay vì chỉ dựa vào ba tình huống tấn công ban đầu.