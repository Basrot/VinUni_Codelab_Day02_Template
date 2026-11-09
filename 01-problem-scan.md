# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:

1. **Lặp lại (Repetitive):** Công việc được thực hiện thường xuyên, theo quy trình cố định và tiêu tốn nhân lực do phải thao tác nhiều lần.
2. **Tốn thời gian (Time-consuming):** Công việc mất nhiều thời gian xử lý thủ công, đặc biệt khi phải đọc, tìm kiếm, tổng hợp hoặc phân tích lượng lớn thông tin.
3. **AI có thể tốt hơn (AI-upgrade):** Quy trình hoặc dịch vụ hiện tại còn hạn chế về tốc độ, khả năng hiểu ngữ cảnh hoặc mức độ cá nhân hóa; AI có thể giúp cải thiện chất lượng và trải nghiệm.
4. **Pain từ người khác (Stakeholder Pain):** Những khó khăn, điểm nghẽn hoặc bất cập được khách hàng, nhân viên hay đối tác phản ánh trong quá trình sử dụng dịch vụ và vận hành.

### 📝 List bài toán của tôi:

| #   | Subsidiary (VinFast/Xanh SM...) | Lens             | Mô tả ngắn bài toán                                                                                                             |
| --- | ------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Xanh SM                         | Tốn thời gian    | Phân tích nội dung phản ánh và lý do khách hàng hủy chuyến để xác định các nguyên nhân phổ biến, hỗ trợ bộ phận vận hành xử lý. |
| 2   | VinFast                         | Lặp lại          | Phân loại nội dung cảnh báo lỗi xe từ mô tả của kỹ thuật viên, đề xuất nhóm lỗi và hướng kiểm tra ban đầu.                      |
| 3   | Vinhomes                        | AI-upgrade       | Phân loại phản ánh của cư dân và tự động đề xuất bộ phận tiếp nhận phù hợp.                                                     |
| 4   | Vinmec                          | Tốn thời gian    | Hỗ trợ trích xuất và tóm tắt thông tin từ hồ sơ bệnh án để chuẩn bị bản nháp tóm tắt xuất viện cho bác sĩ kiểm tra.             |
| 5   | VinWonders                      | Pain from others | Phân tích phản hồi của khách tham quan để phát hiện các vấn đề thường gặp về dịch vụ, trò chơi và tiện ích.                     |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn top 3 từ danh sách SCAN: **#1 (Phân tích phản ánh và lý do khách hàng hủy chuyến), #2 (Phân loại cảnh báo lỗi xe từ mô tả kỹ thuật viên), #4 (Trích xuất và tóm tắt hồ sơ bệnh án thành bản nháp tóm tắt xuất viện).**

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Nhân viên CSKH phải đọc và phân loại lượng lớn    │
│ phản ánh, lý do khách hàng hủy chuyến để xác định nguyên   │
│ nhân phổ biến và hỗ trợ bộ phận vận hành xử lý.             │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Nhân viên CSKH (mất thời gian đọc và phân     │
│ loại). Bộ phận vận hành (khó tổng hợp nguyên nhân phổ     │
│ biến).                                                     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                       │
│   1. Tiếp nhận phản ánh và thông tin hủy chuyến            │
│   → 2. Đọc nội dung phản ánh từ khách hàng                 │
│   → 3. Phân loại nguyên nhân theo từng nhóm                │
│   → 4. Tổng hợp số lượng và tần suất từng nguyên nhân      │
│   → 5. Chuyển báo cáo cho bộ phận vận hành xử lý           │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ Giả định: 5-10 phút/tin)   │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4             │
│ (Đọc phản ánh -> Phân loại nguyên nhân -> Tổng hợp thống  │
│ kê.)                                                       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian phân loại một phản ánh từ 5–10 phút        │
│ → còn dưới 2 phút.                                         │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
│ (Gemini API phân loại phản ánh thành JSON -> Python tổng   │
│ hợp thống kê và tạo báo cáo nguyên nhân phổ biến.)        │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Kỹ thuật viên phải đọc và phân loại các mô tả     │
│ cảnh báo lỗi xe để xác định bộ phận liên quan, nhóm lỗi    │
│ và hỗ trợ bước kiểm tra ban đầu.                            │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau? Kỹ thuật viên (mất thời gian phân loại),       │
│ bộ phận hỗ trợ kỹ thuật (cần tiếp nhận thông tin rõ ràng). │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                       │
│   1. Kỹ thuật viên ghi nhận hiện tượng hoặc cảnh báo lỗi  │
│   → 2. Đọc mô tả và xác định bộ phận liên quan             │
│   → 3. Đối chiếu với các nhóm lỗi đã có                    │
│   → 4. Phân loại và chuyển thông tin đến nhóm kỹ thuật      │
│   → 5. Thực hiện kiểm tra theo quy trình chuyên môn       │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ Giả định: 5-10 phút/lượt) │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4             │
│ (Đọc mô tả -> Trích xuất bộ phận/triệu chứng -> Đề xuất    │
│ nhóm lỗi và thông tin cần kiểm tra bổ sung.)               │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Tự động hóa ít nhất 80% thao tác phân loại báo cáo lỗi     │
│ và giảm số báo cáo phải phân loại thủ công từ 100%         │
│ → còn tối đa 20%.                                           │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
│ (Gemini API trích xuất thông tin và phân loại JSON ->      │
│ Kỹ thuật viên kiểm tra, xác nhận trước khi xử lý.)          │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán: Bác sĩ cần đọc, chọn lọc và tổng hợp thông tin   │
│ từ nhiều phần của hồ sơ bệnh án để chuẩn bị bản nháp       │
│ tóm tắt xuất viện cho bệnh nhân.                            │
│ Công ty thành viên: [x] Vinmec                             │
│                                                             │
│ Ai đang đau? Bác sĩ điều trị (mất thời gian tổng hợp),     │
│ nhân viên y tế (hỗ trợ hoàn thiện hồ sơ).                  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                       │
│   1. Truy cập và thu thập hồ sơ bệnh án trong đợt điều trị │
│   → 2. Đọc thông tin nhập viện, chẩn đoán và diễn biến bệnh│
│   → 3. Kiểm tra kết quả xét nghiệm, thuốc và điều trị      │
│   → 4. Chọn lọc và tổng hợp thông tin thành bản nháp        │
│   → 5. Bác sĩ kiểm tra, chỉnh sửa và hoàn thiện bản cuối  │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ Giả định: 15-20 phút/hồ sơ)│
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4             │
│ (Đọc hồ sơ -> Trích xuất thông tin -> Tạo bản nháp         │
│ tóm tắt xuất viện theo cấu trúc định sẵn)                  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian chuẩn bị bản nháp tóm tắt bệnh án từ        │
│ 15–20 phút → còn dưới 10 phút.                             │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Human-in-the-loop     │
│ (Gemini API trích xuất và tóm tắt -> Bác sĩ kiểm tra,      │
│ chỉnh sửa và phê duyệt trước khi sử dụng.)                │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn của nhóm:

Nhóm quyết định chọn bài toán **"Vinpearl RoomFlow AI"** để thực hiện Deep-Dive.

---
