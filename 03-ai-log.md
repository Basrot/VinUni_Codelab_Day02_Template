# Phase 6 — AI Log & Reflection (Cá nhân)

## AI đã hỗ trợ em ở những phần nào?

Trong Lab Day 02, em dùng ChatGPT để trao đổi và tìm ý tưởng. Ban đầu em thử hướng phân loại phản ánh của cư dân Vinhomes, nhưng sau khi đối chiếu với bài mẫu thì thấy ý tưởng này khá giống ví dụ của lớp. Em nhờ AI gợi ý thêm các hướng khác rồi chọn **Vinpearl RoomFlow AI**: hỗ trợ trưởng ca buồng phòng sắp lịch dọn phòng trước giờ khách check-in.

Sau khi chọn đề tài, em dùng AI để hỗ trợ sắp xếp nội dung Problem Scan, Quick Problem Cards và Deep-Dive theo các mục bài lab yêu cầu. Em cũng nhờ AI giúp nghĩ ra các chỉ số có thể đo khi làm thử như số phòng trễ, tổng phút trễ, thời gian tạo lịch và lỗi phân công trùng giờ.

## Em đã kiểm tra và chỉnh sửa gì?

Em nhận thấy AI có lúc viết giống báo cáo doanh nghiệp và đưa ra các con số như thể đã khảo sát thật. Vì chưa có dữ liệu vận hành của Vinpearl, em yêu cầu viết lại theo cách của sinh viên và ghi rõ các con số là **giả định hoặc mục tiêu thử nghiệm**. Ví dụ 20 phòng, 4 nhân viên và 13 phút lập lịch là tình huống mô phỏng, không phải số liệu thực tế của Vinpearl.

Em cũng không chọn cách để Gemini tự quyết định toàn bộ lịch. Theo em, phần xếp lịch và kiểm tra trùng giờ nên do thuật toán/quy tắc xử lý; Gemini chỉ giúp giải thích kết quả để trưởng ca xem lại. Nếu AI giải thích sai hoặc không chạy được thì vẫn phải có cách xem lịch và xử lý thủ công.

## AI có điểm nào chưa ổn?

AI gợi ý ý tưởng khá nhanh nhưng không tự biết quy trình thực tế tại khách sạn. Nếu em chép nguyên câu trả lời mà không xem lại, bài có thể bị trùng ví dụ, ghi quá chắc chắn về lợi ích hoặc đề xuất chức năng khó kiểm chứng. Vì vậy em chỉ dùng các gợi ý để xây dựng giả thuyết và chưa coi chúng là kết quả thử nghiệm.

## Em học được gì và sẽ làm tiếp thế nào?

Qua bài này, em hiểu rằng chọn đề tài AI không chỉ là nghĩ ra chức năng nghe hay. Cần xác định rõ ai đang gặp khó khăn, bước nào tốn thời gian, AI được phép làm gì và lấy số liệu nào để biết giải pháp có tốt hơn cách cũ hay không.

Hiện tại em **chưa chạy MVP, chưa kiểm thử Gemini và chưa đo metric**, nên chưa thể kết luận dự án thành công. Bước tiếp theo của em là tạo dữ liệu giả lập, lập một lịch baseline, chạy thuật toán đề xuất lịch, thử các prompt yêu cầu AI tự giao việc hoặc bỏ qua bước duyệt, rồi ghi kết quả thực tế vào báo cáo.
