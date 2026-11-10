# 02 — Deep Dive Report: Báo cáo Phân tích sâu (Vin Smart Future)

> **Thông tin nhóm & cá nhân:**
> * Tên dự án: **Vinhomes AI Resident Copilot — Trợ lý AI Phân loại & Điều phối Phản ánh Cư dân**
> * Đơn vị công nghệ: **Vin Smart Future (Vingroup)**
> * Công ty thành viên mục tiêu: **Vinhomes (Quản lý vận hành đô thị thông minh)**
> * Sinh viên thực hiện: **Trần Trọng Đức Tài**
> * MSSV: **2A202603732**
> * Branch Git cá nhân: `2A202603732_TranTrongDucTai`

---

## 🏗️ Phase 3 — DEEP-DIVE

### 3.1. Current-State Workflow Mapping (Quy trình vận hành hiện tại)

*(Sơ đồ trực quan hoá chi tiết được lưu tại file đính kèm: `04-workflow-diagram.png`)*

* **Bối cảnh thực tế tại các khu đô thị Vinhomes:**
  Hằng ngày, Ban Quản lý (BQL) các đại đô thị (Vinhomes Ocean Park, Smart City, Grand Park...) tiếp nhận số lượng lớn phản ánh từ cư dân thông qua ứng dụng *Vinhomes Resident* (mất nước, rò rỉ ống kỹ thuật, hỏng đèn hành lang, tiếng ồn, đỗ xe sai quy định, kẹt thang máy...).

* **Mô tả tuần tự 5 bước trong quy trình thủ công hiện tại:**
  * **Bước 1 (Tiếp nhận phản ánh):** Cư dân tạo yêu cầu trên app với tiêu đề và mô tả tự do bằng tiếng Việt. Yêu cầu đổ về hộp thư đến trung tâm của BQL. *(Thời gian: ~1 phút)*
  * **Bước 2 (Đọc hiểu & Trích xuất nội dung — 🔴 Bottleneck 1):** Nhân viên trực ban phải đọc từng đoạn văn bản tiếng Việt tự do, nhiều trường hợp cư dân viết tắt, không dấu, hoặc cảm xúc bức xúc để tìm ra cốt lõi vấn đề và số căn hộ/tòa nhà. *(Thời gian: ~3–4 phút)*
  * **Bước 3 (Phân loại & Gán nhãn chuyên môn — 🔴 Bottleneck 2):** Trực ban phải tự đánh giá sự cố thuộc phân hệ nào (Điện, Nước sinh hoạt, PCCC, An ninh trật tự, Cây xanh/Môi trường) và đánh giá độ khẩn cấp bằng cảm tính. Nếu phân loại sai, yêu cầu sẽ bị các tổ kỹ thuật trả ngược lại, gây trễ nải. *(Thời gian: ~4–5 phút)*
  * **Bước 4 (Tra cứu & Điều phối nhân sự):** Trực ban mở danh bạ ca trực của tòa nhà tương ứng để chọn kỹ thuật viên hoặc nhân viên an ninh đang phụ trách ca trực. *(Thời gian: ~2 phút)*
  * **Bước 5 (Tạo phiếu giao việc & Gửi thông báo):** Nhập thông tin vào hệ thống quản lý nội bộ và gửi tin nhắn/gọi điện giao việc cho nhân sự thực địa, đồng thời gửi thông báo tiếp nhận ban đầu cho cư dân. *(Thời gian: ~2 phút)*

* **Điểm chuyển giao (🔄 Handoffs):**
  * *Handoff 1:* Cư dân ➔ Trực ban BQL (qua Resident App).
  * *Handoff 2:* Trực ban BQL ➔ Tổ kỹ thuật/An ninh tòa nhà (qua phần mềm nội bộ/Zalo/điện thoại).
  * *Handoff 3:* Nhân sự thực địa ➔ Trực ban BQL (báo cáo hoàn thành để đóng ticket).
* **Điểm nghẽn cổ chai (🔴 Bottlenecks):**
  * **Bước 2 & Bước 3 chiếm tới 7–9 phút/ticket:** Đọc hiểu văn bản phi cấu trúc và phân loại thủ công dễ gây quá tải nghiêm trọng vào giờ cao điểm (sáng sớm trước khi đi làm và tối sau 18h).
* **Tổng thời gian xử lý thủ công trung bình:** **12–15 phút / ticket**.

---

### 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Trường thông tin (Field) | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên trực ban tiếp nhận phản ánh thuộc Ban Quản lý (BQL) tòa nhà Vinhomes. |
| **2. Current Workflow** | Khi cư dân gửi phản ánh qua Resident App, trực ban phải đọc thủ công từng tin nhắn mô tả, tra cứu căn hộ, tự phán đoán gán nhãn chuyên môn (Điện/Nước/Thang máy/An ninh), tra danh bạ ca trực và tạo ticket chuyển giao cho đội kỹ thuật. Toàn bộ qua 5 bước thủ công, mất 12–15 phút/ticket. |
| **3. Bottleneck** | **Bước 2 & 3 (mất 7–9 phút):** Đọc hiểu ngôn ngữ tự nhiên tiếng Việt đời thường, bóc tách thông tin cốt lõi giữa các câu chữ bức xúc và phân loại đúng đội chuyên môn có thẩm quyền xử lý. |
| **4. Business Impact** | Giả định một cụm đô thị tiếp nhận trung bình ~120 phản ánh/ngày. Khâu đọc và phân loại thủ công tiêu tốn **16–20 giờ lao động/ngày** của đội ngũ trực ban. Vào giờ cao điểm, tình trạng nghẽn ticket khiến thời gian tiếp nhận kéo dài, vi phạm cam kết SLA (Service Level Agreement) phản hồi dưới 15 phút của Vinhomes và làm suy giảm chỉ số CSAT của cư dân. |
| **5. Success Metric** | 1. **Tốc độ (Efficiency):** Giảm thời gian đọc hiểu & phân loại từ 8 phút xuống **dưới 1 phút/ticket** (giảm ~85%).<br>2. **Độ chính xác (Accuracy):** Tỷ lệ phân loại đúng đội chuyên môn đạt **trên 95%** trong tập thử nghiệm.<br>3. **An toàn khẩn cấp (Safety):** **100% các sự cố nguy hiểm** (báo cháy, kẹt thang máy, rò rỉ khí gas, ngập nước nghiêm trọng) được AI phát hiện ngay trong vòng **3 giây** để kích hoạt chuông báo động khẩn cấp tới trực ban. |
| **6. Operational Boundary** | • **AI ĐƯỢC PHÉP:** Đọc nội dung phản ánh, trích xuất thực thể (tòa nhà, số căn, hiện tượng), phân loại nhóm vấn đề (Điện/Nước/Thang/An ninh), đánh giá cờ khẩn cấp (`is_emergency: true/false`), và soạn thảo bản nháp phản hồi gửi cư dân có gắn thẻ bắt buộc `[DRAFT_ONLY]`.<br>• **AI TUYỆT ĐỐI CẤM (Hard Constraints):**<br>  - CẤM tự ý hứa hẹn bồi thường tài chính hoặc miễn giảm phí dịch vụ cho cư dân.<br>  - CẤM tự ý đóng ticket hoặc từ chối phản ánh của cư dân.<br>  - CẤM tự ý ra quyết định kỹ thuật đối với các sự cố an toàn tính mạng mà không có người phê duyệt (Bắt buộc Human-in-the-loop). |

---

### 3.3. Future-State Flow & AI Fit

#### Phân loại AI Fit:
* [x] **LLM Feature** (Feature tích hợp mô hình ngôn ngữ lớn)
* *Lý giải lựa chọn:*
  * *Vì sao không dùng Rule-based thuần túy?* Cư dân diễn đạt bằng hàng trăm cách khác nhau ("nhà tôi nước yếu", "vòi sen rỉ rỉ cả đêm", "nước trên trần nhỏ giọt"), từ khóa cố định sẽ bỏ sót hoặc phân loại sai khi gặp từ lóng, viết tắt hoặc lỗi chính tả.
  * *Vì sao không dùng Autonomous Agent (AI tự trị)?* Tác vụ này có luồng vận hành cố định, rủi ro pháp lý và an toàn cao. Nếu để AI tự động giao việc hoặc tự trả lời cư dân mà không có con người kiểm duyệt (HITL), nguy cơ AI cam kết sai chính sách hoặc hiểu nhầm tình huống khẩn cấp sẽ gây khủng hoảng truyền thông cho Vinhomes.
  * *Do đó:* Kiến trúc **LLM Feature (Gemini 2.5 Flash làm Co-pilot)** kết hợp kiểm tra từ khóa an toàn là lựa chọn tối ưu, cân bằng giữa chi phí, tốc độ và độ an toàn.

#### Quy trình tương lai tích hợp AI (Future-State Workflow):
* 🔵 **AI Step (Tác vụ AI xử lý):** Khi cư dân gửi phản ánh, Gemini API ngay lập tức phân tích ngữ nghĩa, trích xuất JSON có cấu trúc gồm: `category`, `sub_issue`, `urgency_level`, `emergency_flag`, và một đoạn văn bản nháp hướng dẫn/xác nhận mở đầu bằng `[DRAFT_ONLY]`.
* 🟢 **Human Step (HITL - Human-in-the-loop):** Màn hình trực ban hiện pop-up gợi ý của AI. Trực ban chỉ mất 10–15 giây để quét mắt kiểm tra, bấm nút **"Xác nhận & Giao việc"** hoặc chỉnh sửa lại nhãn nếu cần.
* ↩️ **Fallback Plan (Phương án dự phòng):** 
  * Nếu Gemini API bị lỗi kết nối hoặc thời gian phản hồi > 5 giây: Hệ thống tự động chuyển ticket vào hàng đợi thủ công như quy trình cũ.
  * Nếu phát hiện từ khóa nguy hiểm sống còn (cháy, nổ, kẹt thang, khói): Hệ thống kích hoạt ngay luồng Rule-based khẩn cấp, rung chuông báo động đỏ trên màn hình trực ban mà không cần đợi AI xử lý.

#### Sơ đồ luồng tương lai:
```text
┌────────────────┐     ┌────────────────────────────┐     ┌────────────────────────┐     ┌───────────────────────┐
│ 1. Cư dân gửi  │     │ 2. 🔵 AI Engine (Gemini)   │     │ 3. 🟢 Trực ban BQL     │     │ 4. Chuyển ticket đến  │
│ phản ánh qua   │ ──> │ Trích xuất thực thể, gán   │ ──> │ Review nhãn & draft    │ ──> │ kỹ thuật viên & gửi   │
│ Resident App   │     │ nhãn, draft tin [DRAFT_ONLY]│    │ Bấm "Duyệt & Giao việc"│     │ thông báo (Dưới 1 min)│
└────────────────┘     └────────────────────────────┘     └────────────────────────┘     └───────────────────────┘
                                                                       │ (Khi AI lỗi / Không tự tin)
                                                                       ▼
                                                          ┌────────────────────────┐
                                                          │ ↩️ Fallback Plan:       │
                                                          │ Chuyển hàng đợi thủ    │
                                                          │ công / Còi báo khẩn cấp│
                                                          └────────────────────────┘
```

---

## 🏁 Phase 5 — EVALUATE: Đánh giá độ sẵn sàng & Quyết định

### AI Readiness Checklist:
- [x] **1. Dữ liệu sẵn sàng:** Có sẵn lịch sử hàng chục ngàn phản ánh ẩn danh của cư dân trên Resident App để làm dữ liệu đánh giá và tinh chỉnh prompt (Few-shot learning).
- [x] **2. Rủi ro trong tầm kiểm soát:** Rủi ro sai sót được triệt tiêu nhờ cơ chế bắt buộc duyệt (HITL) qua thẻ `[DRAFT_ONLY]` và bộ lọc Rule-based bypass cho các sự cố nguy hiểm.
- [x] **3. Stakeholders sẵn sàng:** Khối Quản lý Đô thị Vinhomes đang tìm kiếm giải pháp chuyển đổi số để tối ưu hóa chi phí nhân sự và nâng cao chất lượng dịch vụ cư dân.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
- [x] **GO (Bắt đầu xây dựng Prototype):** Dự án thỏa mãn đầy đủ các tiêu chí về tính khả thi kỹ thuật, thời gian hoàn vốn nhanh và rủi ro được kiểm soát an toàn.

### Justification (Lý giải quyết định):
> **Dự án được đánh giá đạt mức độ GO vì 3 lý do cốt lõi:**
> 1. **Hiệu quả đầu tư (ROI) vượt trội:** Giảm 85% thời gian phân loại ticket giúp tiết kiệm hàng trăm giờ công trực ban mỗi tháng, cho phép nhân sự tập trung vào chăm sóc cư dân thực tế thay vì gõ máy tính.
> 2. **Chi phí vận hành cực thấp:** Sử dụng Gemini 2.5 Flash với chi phí token rất nhỏ (vài chục đồng/ticket), rẻ hơn hàng trăm lần so với chi phí nhân sự đọc thủ công.
> 3. **Lộ trình an toàn vững chắc:** Áp dụng mô hình Co-pilot có người duyệt (HITL) giúp Vinhomes hưởng trọn lợi ích tốc độ của AI mà không phải gánh chịu rủi ro pháp lý hay an toàn vận hành.
