# 03 — AI Log & Reflection: Nhật ký tương tác và phản tư khi dùng AI

> **Thông tin sinh viên:**
> * Họ và tên: **Trần Trọng Đức Tài**
> * MSSV: **2A202603732**
> * Nhóm: **Vin Smart Future Team**
> * Branch Git cá nhân: `2A202603732_TranTrongDucTai`
> * Công cụ AI sử dụng làm Trợ lý đồng hành (Thought-Partner): [x] Google Gemini  [ ] ChatGPT  [ ] Claude

---

## 💡 1. Bối cảnh và Mục đích sử dụng AI

Trong quá trình thực hiện **Phase 1 (SCAN)** và **Phase 2 (QUICK-ASSESS)**, tôi sử dụng AI với vai trò là một **Thought-Partner (Bạn đồng hành tư duy)** và **Chuyên gia phản biện (Challenger)**:
1. **Brainstorm theo 4 Lenses:** Khảo sát các quy trình nghiệp vụ thực tế của các công ty thuộc hệ sinh thái Vingroup (*Vinhomes, VinFast, Xanh SM, Vinpearl, Vinmec*) nhằm phát hiện các điểm nghẽn (bottlenecks) tốn thời gian hoặc gây ức chế cho người vận hành.
2. **Stress-Test các Quick Problem Cards:** Yêu cầu AI đóng vai Trưởng ban Quản lý Vinhomes hoặc Giám đốc Xưởng VinFast để chỉ ra lỗ hổng trong luồng xử lý thủ công, đặt nghi vấn về tính khả thi của giải pháp AI so với các thuật toán Rule-based truyền thống.

---

## 🌟 2. AI đã hỗ trợ hiệu quả những phần nào?

* **Làm rõ ranh giới Actor & Bottleneck:** AI giúp phân tách rõ giữa bước "đọc hiểu thông tin" (bước AI làm tốt) và bước "ra quyết định phê duyệt / hành động vật lý" (bước con người phải kiểm soát).
* **Định lượng Success Metrics:** Khi tôi mô tả bài toán phân loại phản ánh cư dân Vinhomes, AI ban đầu gợi ý một metric rất chung chung là *"cải thiện độ hài lòng của cư dân"*. Tôi đã ép AI cụ thể hóa thành các chỉ số vận hành đo lường được: *"Rút ngắn thời gian chuyển giao ticket từ 10 phút xuống dưới 1 phút; Tỷ lệ phân loại đúng tổ phụ trách đạt > 95%"*.
* **Ví dụ Prompt & Phản hồi chất lượng:**
  * *Prompt tôi dùng:* `"Tôi đang đề xuất bài toán dùng AI gợi ý điểm đón thông minh cho Xanh SM tại các cổng trung tâm thương mại Vincom. Hãy chỉ ra 2 lý do vì sao GPS thuần túy thất bại và AI phân tích ngôn ngữ/lịch sử đón có thể giải quyết được."`
  * *Kết quả:* AI phân tích hiện tượng "hẻm vực đô thị" (urban canyon effect) làm tín hiệu GPS nhảy loạn giữa các tầng và các cổng, đồng thời gợi ý cơ chế clustering các điểm đón thực tế mà tài xế Xanh SM thường xuyên dừng thành công để làm dữ liệu huấn luyện gợi ý.

---

## ⚠️ 3. AI trả lời sai / Ảo giác (Hallucination) / Ranh giới bị vi phạm ở đâu?

* **Ảo giác về quy trình thực tế:** Khi tôi hỏi về việc tự động hóa đặt phòng khách sạn tại Vinpearl, AI đã ảo tưởng rằng các công ty lữ hành đều gửi dữ liệu qua API chuẩn hóa, trong khi thực tế tại Việt Nam phần lớn các đại lý du lịch (B2B) vẫn gửi email bằng văn bản tự do, bảng biểu Excel không chuẩn format và trao đổi qua Zalo.
* **Xu hướng "thần thánh hóa AI":** Ở bài toán mã lỗi kỹ thuật xe VinFast, AI từng đề xuất để LLM "tự động ra lệnh xóa mã lỗi trên xe từ xa qua mạng". Đây là một rủi ro an toàn kỹ thuật cực kỳ nguy hiểm, vi phạm nghiêm trọng quy chuẩn an toàn ô tô (ISO 26262), bởi việc xóa mã lỗi mà chưa kiểm tra vật lý có thể dẫn đến tai nạn giao thông.

---

## 🛡️ 4. Bạn đã can thiệp, tinh chỉnh Prompt và thiết lập Ranh giới (Boundaries) ra sao?

* **Thiết lập Ranh giới an toàn nghiêm ngặt (Hard Operational Boundaries):**
  * Với bài toán xe điện VinFast: Bắt buộc AI chỉ đóng vai trò **Tra cứu tài liệu và Gợi ý sơ bộ (Advisory Co-pilot)**, tuyệt đối CẤM can thiệp vào ECU/hệ thống chấp hành của xe và luôn yêu cầu kỹ thuật viên xưởng xác nhận bằng đồng hồ đo điện trước khi sửa chữa.
  * Với bài toán phản ánh Vinhomes: Các phản ánh liên quan đến sự cố an ninh nghiêm trọng, rò rỉ khí gas hoặc báo cháy (PCCC) BẮT BUỘC bỏ qua bước xếp hàng của AI và kích hoạt ngay cảnh báo khẩn cấp trực tiếp tới trực ban an ninh bằng cơ chế Rule-based Fallback.
* **Kỹ thuật Prompting đã áp dụng:**
  * *Role-playing khắt khe:* Yêu cầu AI đóng vai trò kỹ sư an toàn hệ thống để tự phản biện các đề xuất thiếu an toàn.
  * *Negative constraints:* Ghi rõ các điều cấm trong prompt để hạn chế tối đa ảo giác.

---

## 🎯 5. Bài học rút ra (Key Takeaways)

1. **"Problem First, AI Second":** Đừng tìm cách nhét AI vào mọi ngóc ngách. Một bài toán phân loại ticket hay tra cứu tài liệu chỉ thực sự cần LLM ở bước xử lý ngôn ngữ phi cấu trúc; các khâu định tuyến dữ liệu cố định nên để các hệ thống Rule/Database truyền thống xử lý để đảm bảo tốc độ và tiết kiệm chi phí.
2. **Giá trị của Human-in-the-loop (HITL):** Bất kể mô hình AI có thông minh đến đâu, việc giữ con người ở vị trí phê duyệt cuối cùng là chốt chặn quan trọng nhất để bảo vệ uy tín thương hiệu và an toàn vận hành của tập đoàn.
