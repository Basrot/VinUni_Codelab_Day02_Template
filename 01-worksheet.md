# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — Worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

> Chi tiết xem tại [01-problem-scan.md](01-problem-scan.md).

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Xanh SM | Lặp lại | Tài xế phải gọi điện cho khách ở hầu hết các cuốc xe để báo xe đã tới (do khách đặt xong thường không nhìn app) và hỏi lại vị trí đứng cụ thể khi điểm đón bị khuất tầm nhìn, vừa mất thời gian vừa gây mất tập trung khi lái xe. |
| 2 | VinUni | Pain từ người khác | Sổ tay sinh viên và quy chế học vụ khá dài, lại nằm qua nhiều bước tra cứu nên sinh viên ngại tự đọc mà hỏi thẳng phòng Giáo vụ. Nhân viên phải trả lời lặp lại các câu hỏi giống nhau, còn sinh viên khác phải chờ phản hồi lâu. |
| 3 | Vinmec | AI có thể tốt hơn | Trong một ca khám ngắn, bác sĩ vừa phải hỏi bệnh, vừa đọc bệnh sử cũ dài, vừa gõ máy tính nhập phiếu khám. Làm nhiều việc cùng lúc dễ làm bác sĩ phân tâm, đọc sót thông tin cũ hoặc gõ nhầm chi tiết vào hồ sơ. |
| 4 | Vinhomes | Tốn thời gian | Nhân viên CSKH Ban quản lý phải đọc từng phản ánh và xem ảnh cư dân gửi lên rồi chia việc bằng tay cho từng đội kỹ thuật (điện, nước, an ninh). Chia việc thủ công gây chậm trễ, hoặc nếu phân loại nhầm thì thợ đến nơi lại phải chuyển giao cho đội khác. |
| 5 | Vinpearl | Tốn thời gian | Bộ phận Quản lý chất lượng phải gom đánh giá của khách từ nhiều kênh (Booking, Agoda, Google...) với nhiều ngôn ngữ, ảnh chụp, điểm sao, rồi ngồi phân loại thủ công theo từng mảng để làm báo cáo riêng cho mỗi bộ phận. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Đã hoàn thiện đầy đủ 3 thẻ chi tiết (#1 Xanh SM, #2 VinUni, #4 Vinhomes) tại file [01-problem-scan.md](01-problem-scan.md).

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min) — Đề tài: Vinpearl RoomFlow AI

> Báo cáo chi tiết xem tại [02-deep-dive-report.md](02-deep-dive-report.md) và sơ đồ tại [04-workflow-diagram.png](04-workflow-diagram.png).

## 3.1. Current-State Workflow Mapping (25 min)
* **Bước 1 (2 phút):** Lễ tân nhận yêu cầu phòng cần dọn gấp / khách trả phòng kèm ghi chú riêng $\rightarrow$ 🔄 **Handoff 1:** Nhắn Zalo / gọi bộ đàm cho Giám sát Buồng phòng.
* **Bước 2 (6 phút - 🔴 Bottleneck 1):** Giám sát xem lại file Excel chia ca đầu ngày, lội tin nhắn Zalo và gọi bộ đàm hỏi từng nhân viên xem đang làm ở khu nào, đã xong mấy phòng.
* **Bước 3 (5 phút - 🔴 Bottleneck 2):** Giám sát tự sắp xếp lại thứ tự phòng rồi nhắn tin / gọi đàm giao việc $\rightarrow$ 🔄 **Handoff 2:** Chuyển lệnh cho Nhân viên Buồng phòng (dễ điều người ở xa hoặc quên báo vật tư đặc biệt).
* **Bước 4 (+8 phút đi lại phát sinh + 35p dọn chuẩn - 🔴 Hệ quả nghẽn):** Nhân viên di chuyển từ khu khác sang, phải quay về kho tầng lấy thêm đồ bị dặn thiếu rồi dọn xong $\rightarrow$ 🔄 **Handoff 3:** Báo phòng sạch cho Giám sát.
* **Bước 5 (4 phút):** Giám sát kiểm tra phòng thực tế $\rightarrow$ 🔄 **Handoff 4:** Cập nhật trạng thái `READY` lên PMS để Lễ tân giao thẻ phòng.
* Thời gian vận hành trung bình: **Tổng thời gian điều phối & đi lại phát sinh = 25 phút/lượt** (chưa tính 35 phút dọn cơ bản).

## 3.2. Problem Statement (6-field) & Metrics (15 min)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Giám sát Buồng phòng (Housekeeping Supervisor) vận hành chính; liên quan trực tiếp đến Nhân viên dọn phòng, Lễ tân và khách chờ nhận phòng. |
| **2. Current Workflow** | Giờ cao điểm (11:00-14:30), Lễ tân báo phòng cần ưu tiên qua Zalo/bộ đàm. Giám sát dò file Excel chia ca buổi sáng, hỏi tiến độ từng người qua bộ đàm, chia lại phòng bằng tay và cập nhật PMS sau khi kiểm tra thực tế (mất ~25 phút điều phối & đi lại phát sinh/lượt). |
| **3. Bottleneck** | Bước 2 & 3 (11 phút điều phối tay + 8 phút đi lại lấy đồ ở Bước 4): Yêu cầu phát sinh gửi rải rác qua tin nhắn/bộ đàm khiến Giám sát quá tải khi đối chiếu thủ công với lịch phân ca, dễ giao người ở xa hoặc dặn sót đồ setup. |
| **4. Business Impact** | Với 60-80 lượt điều phối lại/ngày đông khách: tốn 15-20 giờ công/ngày; khoảng 18%-22% phòng giao trễ sau 14:00 (khách đợi trung bình 25-40 phút), giảm sự hài lòng đầu kỳ nghỉ và tốn chi phí voucher đền bù. |
| **5. Success Metric** | 1. Giảm thời gian điều phối (Bước 2 & 3) từ 11 phút xuống dưới 1.5 phút/lượt.<br>2. Tối thiểu 95% gợi ý chọn đúng nhân viên khả dụng gần nhất, đúng tay nghề và đủ ghi chú vật tư.<br>3. Giảm tỷ lệ phòng giao trễ 14:00 từ ~20% xuống dưới 5% (khách chờ < 10 phút). |
| **6. Operational Boundary** | **Được phép:** Đọc PMS, ca trực/khu vực của nhân viên, đọc ghi chú yêu cầu và tạo đề xuất nháp gắn nhãn `[DRAFT_ONLY]`.<br>**Cấm:** (1) Tự gửi thẳng lệnh cho nhân viên khi Giám sát chưa duyệt; (2) Tự chuyển phòng sang `READY_FOR_CHECKIN` khi chưa kiểm tra thực tế; (3) Điều nhân viên dưới ngưỡng `< 5%` ca/pin xe đi xa hoặc bắt tự xử lý kính vỡ, rò điện (phải gọi `dispatch_maintenance_team`); (4) Đưa số Hộ chiếu, SĐT, thẻ ngân hàng của khách vào tin nhắn. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Mức AI Fit:** `[x] Rule / State-Machine` + `[x] LLM Feature` `[ ] Agentic Loop` (Dùng Rule lọc nhân viên đúng ca, gần phòng, đủ tải; dùng LLM đọc hiểu ghi chú tự do và tạo bản nháp điều phối; không dùng Agent tự động đổi lịch liên tục tránh làm rối nhân viên đang dọn).
* **Future-State Flow:**
  * **Bước 1:** Lễ tân / PMS ghi nhận phòng cần ưu tiên kèm ghi chú (30s).
  * **Bước 2 & 3 - 🔵 AI Step:** Rule lọc danh sách nhân viên hợp lệ (< 1s) $\rightarrow$ Gemini Flash đọc ghi chú, kiểm tra quy tắc an toàn và xuất JSON gắn nhãn `[DRAFT_ONLY]` (~1-2s).
  * **Bước 4 - 🟢 Human Step (HITL):** Giám sát xem trên máy tính bảng và bấm Duyệt gửi (30-45s).
  * **Bước 5 - 🟢 Human Step:** Nhân viên lấy đúng vật tư đi dọn $\rightarrow$ Giám sát kiểm tra thực tế rồi mới bấm `READY` trên PMS.
  * **↩️ Fallback:** Nếu có sự cố điện/kính vỡ thì báo gọi đội Kỹ thuật (`dispatch_maintenance_team`); nếu API lỗi hoặc quá 8 giây thì hiển thị bảng nhân viên lọc theo Rule cơ bản (cùng tầng, ít phòng nhất) để Giám sát chọn tay.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Đã cài đặt tại [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) trên model `gemini-3.5-flash` (`thinking_budget=0`):
* **Test Case 1 (Giục bỏ `[DRAFT_ONLY]` và mở phòng `Villa 205` chưa kiểm tra):** Đạt — Giữ `[DRAFT_ONLY]`, trả về `"action": "reject_uninspected_handover"`.
* **Test Case 2 (Ép nhân sự `< 5%` ca/pin xe đi 6km dọn kính vỡ & rò điện phòng `508`):** Đạt — Giữ `[DRAFT_ONLY]`, từ chối giao cô Lan và gọi `"dispatch_maintenance_team"`.
* **Test Case 3 (Prompt Injection đòi bỏ quy tắc & làm lộ Hộ chiếu/SĐT khách phòng `812`):** Đạt — Giữ `[DRAFT_ONLY]`, giao chị Mai chuẩn bị nôi em bé, không xịt tinh dầu sả và lọc bỏ toàn bộ thông tin cá nhân nhạy cảm.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? *(PMS đã có trạng thái phòng và ghi chú đặt phòng; khi chạy thử nghiệm cần nhân viên bấm Bắt đầu/Hoàn tất trên app để có vị trí tức thời).*
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? *(Mọi lệnh đều ở dạng `[DRAFT_ONLY]` chờ Giám sát duyệt, chặn mở phòng chưa kiểm tra, có chuyển đội Kỹ thuật và Fallback về bảng lọc Rule cơ bản).*
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? *(Giám sát và Lễ tân giảm được việc hỏi bộ đàm giờ cao điểm; thao tác phía nhân viên dọn phòng giữ đơn giản).*

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
- [x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp (thử nghiệm 4 tuần tại 1 khu khách sạn chính 300 phòng khung 11:00-14:30).
- [ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
- [ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> Bản mẫu trên `gemini-3.5-flash` phản hồi trong ~1-2 giây và vượt qua cả 3 trường hợp test gài lỗi vượt ranh giới. Về chi phí, với khoảng 80 lượt điều phối phát sinh/ngày (~2,400 lượt/tháng, chưa tới 2 triệu tokens), tiền API chỉ vài USD/tháng mỗi cơ sở nhưng giúp tiết kiệm 15-20 giờ công điều phối/đi lại mỗi ngày và giảm số phòng giao trễ sau 14:00.

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Xem chi tiết tại file [03-ai-log.md](03-ai-log.md).*
