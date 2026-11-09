# 🏗️ Phase 3 — DEEP-DIVE: Vinpearl RoomFlow AI

> **Đề tài theo sơ đồ nhóm:** Hỗ trợ lập và phân công lịch dọn phòng tại Vinpearl. Đầu vào là danh sách phòng cần dọn, thời hạn/phòng ưu tiên và danh sách nhân viên; bộ lập lịch theo quy tắc đề xuất phân công. Gemini chỉ tạo ghi chú/gợi ý ở dạng **DRAFT_ONLY** để trưởng ca xem xét, không tự duyệt hoặc thay đổi lịch.
>
> **Phạm vi prototype:** Dữ liệu giả lập, bộ lập lịch rule-based chạy cục bộ và lời gọi Gemini tùy chọn để tạo ghi chú cho trưởng ca. Chưa kết nối PMS/CSV production, chưa phát lịch cho nhân viên và chưa cập nhật trạng thái phòng thật.
>
> **Cơ sở và giới hạn:** Quy trình hiện tại và quy trình đề xuất dưới đây bám theo sơ đồ workflow do nhóm cung cấp. Thời gian xử lý, khối lượng phòng, năng lực nhân viên và hiệu quả chưa có dữ liệu thực tế; không xem các mục tiêu đề xuất là kết quả đã đo.

## 3.1. Current-State Workflow Mapping

Quy trình hiện tại theo sơ đồ (giả định, cần xác nhận với bộ phận buồng phòng):

```text
① Lễ tân xuất danh sách phòng cần dọn
        │ 🔄 Handoff danh sách phòng cho trưởng ca
        ▼
② Trưởng ca kiểm tra mức ưu tiên và phân công thủ công
  🔴 BOTTLENECK: khó cân bằng tải; có thể trùng lịch hoặc bỏ sót phòng
        │ 🔄 Handoff nhiệm vụ cho nhân viên buồng phòng
        ▼
③ Nhân viên nhận việc và dọn phòng
        │ 🔄 Handoff trạng thái hoàn thành cho hệ thống/đầu mối cập nhật
        ▼
④ Nhân viên/trưởng ca cập nhật báo hoàn thành và trạng thái phòng
```

**Thời gian hiện tại:** Chưa được đo trong tài liệu/sơ đồ. Cần đo riêng thời gian chuẩn bị danh sách, phân công, chờ/di chuyển và cập nhật trạng thái; không tự gán số phút hay tỷ lệ sai sót.

**Vấn đề cần kiểm chứng:** Phân công thủ công có thể mất thời gian, phân bổ không đều, trùng lịch hoặc bỏ sót phòng. Cần xác nhận nguyên nhân, tần suất và tác động với trưởng ca và nhân viên; đồng thời tìm hiểu các ràng buộc thực tế như thời lượng dọn, kỹ năng, khu vực, ca làm và tình trạng phòng.

## 3.2. Problem Statement (6-field) & Metrics

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Lễ tân xuất danh sách phòng; trưởng ca buồng phòng kiểm tra ưu tiên và phân công; nhân viên buồng phòng thực hiện nhiệm vụ và cập nhật trạng thái phòng. |
| **2. Current Workflow** | Lễ tân xuất danh sách phòng cần dọn; trưởng ca xem ưu tiên rồi phân công nhân viên thủ công; nhân viên nhận việc và dọn phòng; sau khi hoàn thành, trạng thái/báo cáo được cập nhật. Nguồn dữ liệu trong sơ đồ là CSV/PMS cho quy trình đề xuất; cách làm và hệ thống hiện tại cần xác nhận. |
| **3. Bottleneck** | Bước trưởng ca phân công thủ công: khó cân bằng tải và theo dõi đồng thời phòng ưu tiên, hạn hoàn thành, sức chứa của nhân viên; có nguy cơ trùng lịch hoặc bỏ sót phòng. |
| **4. Business Impact** | Chưa có baseline về thời gian lập lịch, số phòng/ca, tỷ lệ phân công lại, phòng bị bỏ sót hoặc tác động đến thời điểm phòng sẵn sàng. Đo các chỉ số này theo ca trước khi triển khai để xác định giá trị vận hành; không quy đổi thành doanh thu khi chưa có chứng cứ. |
| **5. Success Metric** | Mục tiêu thí điểm đề xuất, cần trưởng ca xác nhận: (a) **0 phân công vượt sức chứa** đã cấu hình; (b) **100% phòng được phân công hoặc được liệt kê rõ là chưa phân công** để trưởng ca xử lý; (c) **0 phòng bị lặp** trong lịch đầu ra; (d) **100% lịch do con người duyệt** trước khi phát cho nhân viên; (e) đo thời gian lập lịch và so với baseline, sau đó thống nhất ngưỡng cải thiện mục tiêu. |
| **6. Operational Boundary** | Rule-based Scheduler là nguồn lịch phân công chính thức trong prototype; quy tắc ưu tiên và giới hạn tải phải minh bạch, cấu hình/được trưởng ca xác nhận. Gemini chỉ được soạn ghi chú nháp hoặc nêu điểm cần kiểm tra dựa trên lịch đã có; **không được tự duyệt, thay đổi phòng/nhân viên/thời hạn/ưu tiên, cập nhật CSV/PMS, giao việc hoặc nhắn nhân viên**. Trưởng ca kiểm tra và phê duyệt; nhân viên nhận nhiệm vụ sau khi lịch được duyệt và tự cập nhật hoàn thành qua quy trình được phép. Nếu Gemini lỗi/đầu ra không hợp lệ, giữ nguyên lịch rule-based và chuyển trưởng ca xử lý. |

### Cách đo và kiểm chứng

- **Dữ liệu đầu vào tối thiểu:** mã phòng, hạn hoàn thành/giờ ưu tiên, mức ưu tiên, thời lượng ước tính; danh sách nhân viên và giới hạn tải trong ca. Chỉ đưa thêm kỹ năng/khu vực nếu vận hành xác nhận quy tắc và dữ liệu nguồn đáng tin cậy.
- **Không giao cho LLM việc tối ưu có ràng buộc:** phân công và kiểm tra sức chứa là xử lý xác định bằng quy tắc; Gemini không phải nguồn dữ liệu hoặc nguồn chân lý của lịch.
- **Giới hạn prototype hiện tại:** lịch mẫu sắp phòng ưu tiên trước, rồi theo deadline và phân công nhân viên có tổng tải thấp nhất trong giới hạn phút/ca. Chưa mô hình hóa thời điểm bắt đầu, thời gian di chuyển, khu vực hoặc kỹ năng; do đó không chứng minh nhân viên chắc chắn hoàn thành trước deadline. Trưởng ca phải kiểm tra các ràng buộc này trước khi duyệt.
- **Đánh giá lịch:** kiểm tra tính duy nhất của mã phòng, mọi tải nhân viên không vượt giới hạn, và phòng không thể phân công được xuất hiện trong danh sách chờ xử lý.
- **So sánh vận hành:** ghi thời gian lập lịch và số lần chỉnh sửa/phân công lại theo ca trước/sau; so sánh trên cùng loại ca và khối lượng tương đương.

## 3.3. Future-State Flow & AI Fit

### AI Fit

- [x] **Rule / State-Machine — lập lịch và phân công**
- [ ] LLM Feature — quyết định/phân công lịch
- [ ] Agentic Loop

**Vai trò Gemini giới hạn:** LLM Feature chỉ tạo ghi chú **DRAFT_ONLY** cho trưởng ca (ví dụ tóm tắt tải, nêu phòng chưa phân công hoặc điểm cần kiểm tra từ lịch rule-based). Gemini không tạo hay chỉnh sửa lịch. Vì vậy, lõi điều phối là rule-based; LLM chỉ là lớp hỗ trợ tùy chọn, có thể bỏ qua mà quy trình vẫn chạy được.

### Future-State Flow theo sơ đồ nhóm

```text
① CSV/PMS đã được phép sử dụng:
   danh sách phòng, hạn/ưu tiên và nhân viên
        │
        ▼
② Rule-based Scheduler:
   sắp thứ tự theo quy tắc đã duyệt; phân công trong giới hạn tải;
   phòng không phân công được được đưa vào danh sách chờ
        │
        ├── Dữ liệu thiếu/sai hoặc không đủ công suất
        │       └── Đánh dấu rõ, không tự bịa dữ liệu; trưởng ca xử lý
        ▼
③ 🔵 Gemini tạo ghi chú lịch dạng DRAFT_ONLY (tùy chọn)
   Không thay đổi lịch hoặc giao việc
        │
        ├── Gemini lỗi / quá tải / JSON sai
        │       └── ↩️ Fallback: giữ lịch Rule-based; chuyển trưởng ca xử lý
        ▼
④ 🟢 Trưởng ca kiểm tra lịch rule-based và ghi chú nháp;
   sửa nếu cần và phê duyệt lịch
        │
        ├── Chưa đồng ý → chỉnh quy tắc/dữ liệu và chạy lại, sau đó duyệt
        ▼
⑤ Nhân viên nhận lịch đã duyệt, thực hiện dọn phòng,
   cập nhật hoàn thành/trạng thái theo quy trình được phép
```

**Bảo vệ vận hành:** Gemini nhận bản sao tối thiểu của lịch đã được chuẩn hóa, không có quyền ghi vào PMS/CSV hay gọi công cụ giao việc. Lịch chuẩn được giữ tách biệt khỏi ghi chú LLM. Không phát lịch trước khi trưởng ca duyệt. Nếu nguồn PMS/CSV lỗi, dừng tạo lịch mới và dùng quy trình hiện hành thay vì coi dữ liệu cũ là mới nhất.

## 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist

1. [ ] Có dữ liệu CSV/PMS và danh sách nhân viên mẫu, sạch, đại diện, được phép dùng. Sơ đồ nêu nguồn dự kiến nhưng chưa xác nhận quyền truy cập hoặc chất lượng dữ liệu.
2. [x] Có thể kiểm soát rủi ro bằng lịch rule-based, bước duyệt của trưởng ca và fallback. Gemini không có quyền sửa lịch hoặc giao việc.
3. [ ] Trưởng ca và nhân viên đã xác nhận quy tắc phân công, giới hạn tải và quy trình nhận/cập nhật nhiệm vụ. Chưa có bằng chứng xác nhận.

### Quyết định đề xuất: **NOT YET cho triển khai thực tế; tiếp tục prototype bằng dữ liệu giả lập**

Sơ đồ thể hiện rõ điểm đau và ranh giới phù hợp: quy tắc quyết định lịch, Gemini chỉ hỗ trợ bản nháp, người phụ trách duyệt trước khi nhân viên nhận việc. Tuy nhiên, chưa có baseline, dữ liệu PMS/CSV được phê duyệt, quy tắc vận hành/giới hạn tải đã xác nhận hoặc phản hồi người dùng. Do đó chưa thể kết luận mức cải thiện hay triển khai production.

**Điều kiện để chuyển bước:**

1. Trưởng ca xác nhận định nghĩa ưu tiên, hạn phòng, thời lượng dọn, giới hạn tải và trường hợp phòng phải để chờ.
2. Chủ hệ thống/bảo mật phê duyệt schema và dữ liệu đầu vào; ban đầu chỉ dùng dữ liệu giả lập hoặc bản sao đã được phép.
3. Đo baseline lập lịch trên các ca đại diện.
4. Kiểm thử lịch rule-based với phòng ưu tiên, nhân viên quá tải, dữ liệu thiếu/sai và tình huống không đủ nhân lực.
5. Chạy shadow mode; trưởng ca đối chiếu lịch đề xuất với quy trình hiện tại. Chỉ phát lịch cho nhân viên sau khi các chỉ số và quy trình duyệt được xác nhận.

Nếu Gemini không khả dụng, lịch Rule-based vẫn phải đầy đủ, được hiển thị rõ là chờ duyệt và chuyển trưởng ca xử lý; không phụ thuộc LLM để hoàn thành phân công.
