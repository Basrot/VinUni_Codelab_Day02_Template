# LAB 02 — PROBLEM SCAN & QUICK ASSESSMENT

**Đề tài lựa chọn:** Vinhomes AI Resident Copilot

## PHASE 1 — TÌM KIẾM CÁC BÀI TOÁN

### 1. Cách em tìm ý tưởng

Khi tìm hiểu về các công ty thuộc Vingroup, em nghĩ rằng không nhất thiết phải tìm một vấn đề quá lớn mới có thể ứng dụng AI. Có những công việc khá đơn giản nhưng phải làm đi làm lại nhiều lần, nếu có công cụ hỗ trợ thì nhân viên sẽ đỡ mất thời gian hơn.

Em tập trung vào những công việc liên quan đến tiếp nhận thông tin từ khách hàng, vì đây là những bài toán dễ hình dung quy trình và cũng có thể làm thử một sản phẩm nhỏ trong thời gian học.

Em đưa ra 5 vấn đề sau:

| STT | Công ty | Lens | Vấn đề em nhận thấy |
|---|---|---|---|
| 1 | Vinhomes | Repetitive | Khi cư dân báo hỏng thiết bị hoặc phản ánh dịch vụ, nhân viên có thể phải đọc từng yêu cầu rồi chuyển cho bộ phận phụ trách. |
| 2 | VinFast | Time-consuming | Khi khách hàng mô tả xe gặp vấn đề, nhân viên phải tìm hiểu xem lỗi thuộc nhóm nào trước khi chuyển cho kỹ thuật viên. |
| 3 | Xanh SM | Stakeholder Pain | Khách hàng có thể phản ánh về tài xế, điểm đón hoặc giá cước. Nhân viên phải đọc và phân loại các phản ánh này. |
| 4 | Vinpearl | Repetitive | Khách du lịch thường hỏi những câu giống nhau về giờ nhận phòng, dịch vụ hoặc đặt vé. Nhân viên có thể phải trả lời nhiều lần. |
| 5 | Vinhomes | AI-upgrade | Khi nhiều cư dân cùng phản ánh một sự cố, nhân viên có thể phải đọc nhiều tin nhắn để biết có phải cùng một vấn đề hay không. |

Đây là những tình huống em tự đặt ra dựa trên cách các dịch vụ thường hoạt động, chưa có số liệu thực tế từ các công ty.

Sau khi xem xét, em chọn 3 vấn đề để phân tích kỹ hơn là Vinhomes, VinFast và Xanh SM.

---

## PHASE 2 — QUICK PROBLEM CARDS

### QUICK PROBLEM CARD #1 — Vinhomes

**1. Bài toán**

Hỗ trợ nhân viên phân loại các yêu cầu, phản ánh của cư dân bằng AI.

**2. Công ty thành viên**

Vinhomes.

**3. Ai đang gặp vấn đề?**

Theo em, người gặp khó khăn trực tiếp là nhân viên tiếp nhận yêu cầu của cư dân. Nếu có nhiều người gửi phản ánh cùng lúc, nhân viên phải đọc và xử lý từng yêu cầu.

Cư dân cũng bị ảnh hưởng nếu yêu cầu được chuyển chậm hoặc chuyển chưa đúng bộ phận.

**4. Quy trình hiện tại (em giả định)**

1. Cư dân gửi phản ánh về một vấn đề trong chung cư.
2. Nhân viên đọc nội dung phản ánh.
3. Nhân viên xác định vấn đề thuộc nhóm nào.
4. Chuyển yêu cầu cho bộ phận liên quan.
5. Bộ phận phụ trách kiểm tra và xử lý.

**5. Bước nào tốn thời gian nhất?**

Em nghĩ bước đọc và phân loại yêu cầu có thể tốn thời gian, đặc biệt khi cư dân viết dài hoặc không mô tả rõ vấn đề.

Ví dụ cư dân nhắn:

"Nhà tôi ở tầng 15, từ sáng đến giờ nước chảy rất yếu, không biết tòa nhà có đang sửa gì không?"

Nhân viên cần hiểu đây là vấn đề liên quan đến nước, sau đó mới biết nên chuyển cho ai.

Em tạm giả định việc đọc và phân loại mất khoảng 3–5 phút/yêu cầu. Đây chỉ là con số để thử nghiệm, không phải thời gian thực tế của Vinhomes.

**6. AI có thể hỗ trợ ở đâu?**

Em muốn dùng Gemini để đọc nội dung cư dân gửi và trả về một số thông tin:

- Yêu cầu thuộc nhóm nào: điện, nước, thang máy, vệ sinh hoặc vấn đề khác.
- Có dấu hiệu khẩn cấp hay không.
- Nên chuyển đến bộ phận nào.
- Gợi ý một câu phản hồi ngắn cho cư dân.

Nhân viên vẫn là người kiểm tra kết quả và quyết định xử lý.

**7. Đo kết quả như thế nào?**

Em dự định tự tạo khoảng 30–50 phản ánh giả lập, sau đó gán nhãn thủ công để so sánh với kết quả Gemini.

Mục tiêu ban đầu:

- Phân loại đúng ít nhất 85% phản ánh thử nghiệm.
- Không bỏ sót tình huống khẩn cấp trong bộ test nhỏ.
- Thời gian AI xử lý một yêu cầu dưới 5 giây ở phần lớn lượt thử.

Em sẽ đo kết quả thực tế rồi mới kết luận có đạt hay không.

**8. Quick Architecture**

LLM kết hợp một số quy tắc kiểm tra đơn giản.

Em chọn LLM vì cư dân có thể diễn đạt cùng một vấn đề bằng nhiều cách khác nhau. Tuy nhiên, nếu chỉ cần nhận biết vài từ khóa cố định thì code thông thường có thể đơn giản và rẻ hơn.

---

### QUICK PROBLEM CARD #2 — VinFast

**1. Bài toán**

Hỗ trợ phân loại mô tả sự cố xe điện do khách hàng gửi đến.

**2. Công ty thành viên**

VinFast.

**3. Ai đang gặp vấn đề?**

Nhân viên tiếp nhận dịch vụ và khách hàng cần hỗ trợ về xe.

**4. Quy trình hiện tại (em giả định)**

1. Khách hàng liên hệ và mô tả hiện tượng của xe.
2. Nhân viên ghi nhận thông tin.
3. Nhân viên xác định nhóm vấn đề ban đầu.
4. Chuyển thông tin cho bộ phận kỹ thuật.
5. Kỹ thuật viên kiểm tra trực tiếp.

**5. Bước nào tốn thời gian nhất?**

Em nghĩ khó khăn nằm ở việc hiểu mô tả của khách hàng.

Ví dụ: "Xe đang đi thì hiện một biểu tượng lạ, sau đó em thấy xe chạy yếu hơn."

Nếu không có đủ thông tin, nhân viên có thể phải hỏi lại nhiều lần.

Em tạm giả định bước tiếp nhận và phân loại ban đầu mất khoảng 5–7 phút.

**6. AI có thể hỗ trợ ở đâu?**

Gemini có thể đọc mô tả và gợi ý nhóm vấn đề, đồng thời đưa ra những câu hỏi cần bổ sung thông tin.

Tuy nhiên, em không muốn AI tự kết luận xe bị hỏng bộ phận nào vì việc đó cần kỹ thuật viên kiểm tra.

**7. Đo kết quả như thế nào?**

- Thử nghiệm trên 30 mô tả sự cố giả lập.
- Mục tiêu phân loại đúng từ 80% trở lên.
- Kiểm tra AI có đưa ra kết luận kỹ thuật quá chắc chắn hay không.

**8. Quick Architecture**

LLM hỗ trợ tiếp nhận thông tin, kết hợp quy tắc an toàn và kiểm tra của nhân viên.

**Đánh giá của em**

Ý tưởng này khá thú vị, nhưng em chưa có nhiều kiến thức về kỹ thuật xe điện. Nếu làm không cẩn thận, kết quả AI có thể nghe hợp lý nhưng thực tế lại sai. Vì vậy em chưa ưu tiên bài toán này.

---

### QUICK PROBLEM CARD #3 — Xanh SM

**1. Bài toán**

Hỗ trợ phân loại phản ánh của khách hàng sau chuyến xe.

**2. Công ty thành viên**

Xanh SM.

**3. Ai đang gặp vấn đề?**

Nhân viên chăm sóc khách hàng, bộ phận vận hành và khách hàng sử dụng dịch vụ.

**4. Quy trình hiện tại (em giả định)**

1. Khách hàng gửi phản ánh về chuyến đi.
2. Nhân viên đọc nội dung.
3. Xác định vấn đề liên quan đến tài xế, điểm đón, giá cước hay dịch vụ.
4. Chuyển cho bộ phận phù hợp.
5. Kiểm tra thông tin và phản hồi khách hàng.

**5. Bước nào tốn thời gian nhất?**

Em nghĩ việc phân loại sẽ khó hơn nếu khách hàng phản ánh nhiều vấn đề trong cùng một tin nhắn.

Ví dụ:

"Tài xế đến sai điểm đón, tôi phải đi bộ khá xa mà cuối cùng vẫn bị tính thêm phí."

Tin nhắn này vừa có vấn đề về điểm đón, vừa có vấn đề về chi phí.

Em tạm giả định nhân viên cần khoảng 4–6 phút để đọc, xác định và chuyển yêu cầu.

**6. AI có thể hỗ trợ ở đâu?**

AI có thể xác định một hoặc nhiều nhóm vấn đề trong phản ánh, sau đó gợi ý bộ phận tiếp nhận.

**7. Đo kết quả như thế nào?**

- Tạo 30–50 phản ánh giả lập.
- Mục tiêu phân loại đúng ít nhất 85%.
- Kiểm tra khả năng phát hiện nhiều vấn đề trong một phản ánh.
- Kiểm tra AI có tự ý hứa hoàn tiền hay không.

**8. Quick Architecture**

LLM hỗ trợ phân loại nội dung, còn các quyết định hoàn tiền hoặc xử lý tài xế phải do nhân viên thực hiện.

**Đánh giá của em**

Bài toán khá dễ hiểu và có thể thử nghiệm bằng Gemini. Tuy nhiên, nếu muốn xử lý thật thì cần thêm thông tin chuyến đi và quy định nội bộ. Em chưa có những dữ liệu đó.

---

## PHẦN 3 — SO SÁNH VÀ CHỌN ĐỀ TÀI

Sau khi phân tích 3 bài toán, em có bảng so sánh như sau:

| Tiêu chí | Vinhomes | VinFast | Xanh SM |
|---|---|---|---|
| Dễ hiểu quy trình | Dễ | Trung bình | Dễ |
| Có thể tự tạo dữ liệu thử nghiệm | Có | Có, nhưng khó đánh giá đúng sai | Có |
| Phù hợp với Gemini | Có | Có | Có |
| Cần kiến thức chuyên ngành | Không quá nhiều | Khá nhiều | Trung bình |
| Có thể làm prototype trong buổi lab | Có | Khó hơn | Có |

### Đề tài em quyết định lựa chọn

**Vinhomes AI Resident Copilot — Trợ lý AI hỗ trợ phân loại và xử lý phản ánh cư dân.**

### Vì sao em chọn đề tài này?

Em chọn bài toán này vì thấy nó khá gần với cuộc sống hằng ngày. Khi sống trong chung cư, cư dân có thể gặp nhiều vấn đề như mất nước, hỏng thang máy, tiếng ồn hoặc vệ sinh.

Em nghĩ nếu nhân viên có một công cụ giúp đọc và phân loại các phản ánh thì công việc tiếp nhận có thể nhanh hơn. Tuy nhiên, em cũng chưa chắc dùng AI sẽ tốt hơn cách làm hiện tại, vì nếu lượng phản ánh ít thì nhân viên hoàn toàn có thể tự xử lý.

Vì vậy, em muốn làm một prototype nhỏ bằng Python và Gemini API để kiểm tra xem AI có phân loại đúng các phản ánh hay không, có xử lý được những câu diễn đạt khó hiểu không và có mắc lỗi khi gặp yêu cầu bất thường không.

Nếu kết quả tốt, em nghĩ có thể phát triển thêm. Còn nếu AI thường xuyên phân loại sai hoặc chi phí sử dụng cao thì cần xem lại việc có nên áp dụng hay không.

### Phạm vi em dự định làm

Trong Lab 02, em chỉ làm chương trình nhận một nội dung phản ánh và trả về kết quả phân loại dưới dạng JSON.

Em chưa xây dựng ứng dụng cho cư dân, chưa kết nối hệ thống Vinhomes thật và cũng chưa tự động chuyển yêu cầu đến bộ phận kỹ thuật.

Em muốn hoàn thành chức năng nhỏ này trước, kiểm thử được rồi mới nghĩ đến việc mở rộng.