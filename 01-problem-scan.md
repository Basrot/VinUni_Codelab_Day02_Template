# 🔍 Phase 1 — SCAN
### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinFast     | Lặp lại & tốn thời gian | Nhân viên CSKH nhận ticket từ người dùng về các vấn đề lỗi, rồi tốn thời gian đọc thủ công từng mô tả, xác định loại lỗi, và gán (route) cho đúng bộ phận kỹ thuật hoặc trung tâm dịch vụ gần nhất.
| 2 | Xanh SM     | Lặp lại | Đội ngũ vận hành mở từng bộ hồ sơ tài xế tải lên để kiểm tra chéo bằng mắt thường các thông tin trên CCCD, bằng lái xe, và lý lịch tư pháp xem có khớp với form đăng ký và có dấu hiệu chỉnh sửa hay không.
| 3 | Xanh SM     | Stakeholder Pain & Tốn thời gian | Khách báo mất đồ qua tổng đài, nhân viên ghi nhận thành văn bản. Khi tài xế báo nhặt được đồ, nhân viên lại phải đọc/nghe và lục tìm trong hàng trăm ticket để so khớp các đặc điểm giữa hai nguồn thông tin.
| 4 | VinFast     | AI upgrade | Khi khách hàng báo xe tụt pin nhanh bất thường hoặc lỗi màn hình hiển thị, kỹ thuật viên phải xuất file log dữ liệu thô của xe, đọc đối chiếu hàng ngàn dòng tham số để quyết định xem có cần gọi xe đến xưởng hay không.
| 5 | Xanh SM     | AI upgrade & Stakeholder Pain | Khi có mưa lớn bất chợt hoặc sự kiện tan tầm, hệ thống rule-based hiện tại không phản ứng kịp. Điều phối viên phải nhìn bản đồ nhiệt bằng mắt thường và nhắn tin/gọi điện thủ công yêu cầu một nhóm tài xế di chuyển về vùng đang "cháy" xe.
---

Đây là những tình huống em tự đặt ra dựa trên suy nghĩ về cách các dịch vụ sẽ hoạt động, không hề có số liệu thực tế từ các công ty.

# 🃏 Phase 2 — QUICK-ASSESS 


```

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD 1                                        │
│                                                             │
│ Bài toán (1 câu): Tốn thời gian xử lý thủ công ticket       │
│ Công ty thành viên: [X] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH                         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận ticket ──> 2. Đọc thủ công                        | 
|   ──> 3. Xác định lỗi ──> 4. Gán route                      |
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-4 (⏱ 3-5 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              |
| (Đọc hiểu văn bản/giọng về mô tả lỗi của khách,             |
|tự động trích xuất từ khóa, phân loại nhóm và định tuyến)     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?  Giảm từ 3/5 phút     |
| xuống 5 giây, Tỷ lệ phân luồng chính xác (FCR) > 90%        │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘


┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Khớp nối thông tin tìm đồ thất lạc        │
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên xử lý                        │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1.Khách báo mất  ──> 2. Nhân viên ghi nhận ──>            |
|    3. Tài báo nhặt ──> 4. Nhân viên tìm thông tin khớp      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 4 (⏱ 5-10 phút/lượt) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 4             |
| (đề xuất thông tin có có tỷ lệ khớp cao)                    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?  │Giảm thời gian tìm  |
| xuống dưới 2 phút/ca, nâng % chính xác > 75%                 |
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Điều phối xe thủ công khi có biến động cục bộ│
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Điều phối                              │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1.Quan sát bản đồ nhiệt  ──> 2. Gọi thủ công nhóm xế      |
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 1-2 (⏱ 10-15 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-2              |
| (theo dõi thời tiết, mạng xã hội về sự kiện,                |
| tình trạng giao thông, dự đoán trước điểm nóng,...)          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?  │Giảm độ trễ phát hiện|
| và ra lệnh điều phối 15 phút xuống 3 phút                    |
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [] LLM  [X] Agent │
└─────────────────────────────────────────────────────────────┘



