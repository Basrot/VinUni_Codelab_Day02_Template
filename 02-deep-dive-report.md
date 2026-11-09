# LAB 02 — DEEP DIVE REPORT

## Đề tài: Vinhomes AI Resident Copilot

### 1. Giới thiệu bài toán

Em chọn nghiên cứu việc sử dụng AI để hỗ trợ nhân viên tiếp nhận và phân loại phản ánh của cư dân tại các khu chung cư Vinhomes.

Em nghĩ rằng khi sống tại chung cư, cư dân có thể gặp những vấn đề như mất nước, mất điện, thang máy hỏng, tiếng ồn hoặc vệ sinh khu vực chung.

Khi cư dân gửi phản ánh, nhân viên cần đọc nội dung, xác định vấn đề và chuyển đến bộ phận phụ trách.

Em muốn thử xem Gemini có thể giúp nhân viên thực hiện bước phân loại này nhanh hơn hay không.

Đây là quy trình em giả định để nghiên cứu, chưa phải quy trình vận hành chính thức của Vinhomes.

## 2. Current-State Workflow — Quy trình hiện tại

Em giả định một yêu cầu của cư dân sẽ trải qua các bước:

1. Cư dân gửi phản ánh qua ứng dụng hoặc kênh liên hệ.
2. Nhân viên tiếp nhận và đọc nội dung.
3. Nhân viên xác định loại vấn đề và mức độ ưu tiên.
4. Nhân viên chuyển yêu cầu đến bộ phận phụ trách.
5. Bộ phận phụ trách kiểm tra và xử lý.
6. Nhân viên cập nhật kết quả cho cư dân.

### Thời gian xử lý giả định

| Bước | Thời gian |
|---|---:|
| Tiếp nhận yêu cầu | 1 phút |
| Đọc nội dung | 2 phút |
| Phân loại và đánh giá | 2 phút |
| Chuyển yêu cầu | 1 phút |
| Tổng cộng | 6 phút |

Em chỉ tính thời gian tiếp nhận và chuyển yêu cầu, chưa tính thời gian sửa chữa hoặc giải quyết thực tế.

**Bottleneck:** Em nghĩ bước đọc và phân loại có thể là bước mất nhiều thời gian nhất, nhất là khi cư dân viết không rõ hoặc phản ánh nhiều vấn đề cùng lúc.

**Handoff:** Điểm chuyển giao nằm ở bước nhân viên chuyển thông tin sang bộ phận kỹ thuật, an ninh hoặc chăm sóc cư dân.

## 3. Problem Statement — 6 Fields

**1. Actor / Operator**

Nhân viên chăm sóc cư dân và nhân viên ban quản lý tòa nhà.

**2. Current Workflow**

Nhân viên nhận phản ánh, đọc nội dung, phân loại vấn đề rồi chuyển đến bộ phận phụ trách.

**3. Bottleneck**

Việc đọc và phân loại thủ công có thể tốn thời gian khi số lượng phản ánh lớn hoặc nội dung khó hiểu.

**4. Business Impact**

Nếu giả sử có 50 yêu cầu mỗi ngày và bước đọc, phân loại mất 4 phút/yêu cầu thì tổng thời gian là:

50 × 4 = 200 phút/ngày.

Đây chỉ là phép tính minh họa, không phải số liệu thực tế của Vinhomes.

**5. Success Metric**

Em đặt mục tiêu thử nghiệm:

- Phân loại đúng ít nhất 85% trên tập dữ liệu thử nghiệm.
- Thời gian Gemini xử lý một phản ánh dưới 5 giây ở phần lớn lượt chạy.
- Kết quả trả về đúng cấu trúc JSON.
- Không bỏ sót tình huống khẩn cấp trong bộ kiểm thử nhỏ.

**6. Operational Boundary**

AI chỉ được phép đọc, phân loại và đề xuất hướng xử lý.

AI không được tự đóng yêu cầu, tự phê duyệt bồi thường, tiết lộ thông tin cư dân hoặc tự quyết định cách xử lý các sự cố nguy hiểm.

Nhân viên phải kiểm tra kết quả trước khi thực hiện.

## 4. AI Fit — Có thực sự cần AI không?

Em xem xét ba cách giải quyết.

**Cách 1: Rule-based**

Có thể dùng các từ khóa như "mất nước", "mất điện", "thang máy" để phân loại.

Ưu điểm là dễ lập trình, nhanh và không tốn phí API.

Nhược điểm là có thể gặp khó khăn nếu cư dân viết sai chính tả hoặc diễn đạt không theo từ khóa cố định.

**Cách 2: LLM — Gemini**

Gemini có thể hiểu nội dung phản ánh dù người dùng diễn đạt theo nhiều cách khác nhau.

Tuy nhiên, Gemini vẫn có thể trả lời sai hoặc tự suy đoán thông tin không có trong yêu cầu.

**Cách 3: AI Agent**

Có thể xây dựng một hệ thống tự nhận yêu cầu, tìm bộ phận phụ trách và tạo phiếu xử lý.

Nhưng em thấy cách này chưa cần thiết cho bài lab vì phức tạp hơn, cần kết nối với hệ thống quản lý thật và có nhiều rủi ro hơn.

**Lựa chọn:** Em chọn Gemini để hỗ trợ phân loại, kết hợp quy tắc kiểm tra và nhân viên xác nhận.

## 5. Future-State Workflow — Quy trình đề xuất

1. Cư dân gửi phản ánh.
2. Hệ thống tiếp nhận nội dung.
3. Gemini phân tích và phân loại phản ánh.
4. Hệ thống kiểm tra định dạng kết quả và các dấu hiệu khẩn cấp.
5. Nhân viên xem lại kết quả.
6. Nhân viên xác nhận và chuyển đến bộ phận phụ trách.
7. Bộ phận phụ trách xử lý và cập nhật kết quả.

### Human-in-the-loop

Nhân viên vẫn là người quyết định cuối cùng. AI chỉ đóng vai trò hỗ trợ.

### Fallback

Nếu Gemini không trả về kết quả hợp lệ, không xác định được nhóm vấn đề hoặc API gặp lỗi, hệ thống sẽ chuyển yêu cầu sang nhân viên phân loại thủ công.

Với những phản ánh có dấu hiệu nguy hiểm, hệ thống phải ưu tiên cảnh báo và chuyển người phụ trách theo quy trình khẩn cấp, không chờ AI tự giải quyết.

## 6. Đánh giá sơ bộ

Em thấy ý tưởng này có thể thử nghiệm được vì không cần xây dựng cả ứng dụng chung cư.

Chỉ cần một chương trình Python nhận nội dung phản ánh, gửi cho Gemini và nhận kết quả JSON là có thể kiểm tra khả năng phân loại.

Tuy nhiên, em chưa có dữ liệu vận hành thực tế và cũng chưa biết cách xử lý hiện tại của Vinhomes có thực sự chậm hay không.

Vì vậy, em chưa thể kết luận rằng sử dụng AI sẽ tốt hơn cách làm hiện tại.

Em cần chạy thử, đo kết quả và so sánh với một cách phân loại bằng từ khóa đơn giản trước khi đưa ra quyết định cuối cùng.