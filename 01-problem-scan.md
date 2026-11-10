# 01 — Problem Scan: Tìm kiếm & Đánh giá nhanh bài toán (Vin Smart Future)

> **Thông tin sinh viên:**
> * Họ và tên: **Trần Trọng Đức Tài**
> * MSSV: **2A202603732**
> * Nhóm: **Vin Smart Future Team**
> * Branch Git cá nhân: `2A202603732_TranTrongDucTai`

---

## 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Sử dụng **4 Lenses** (*Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác*) để quét qua các hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **5 bài toán thực tế** hoàn toàn mới (không trùng lặp ví dụ mẫu):

### 📝 Bảng quét cơ hội (SCAN Table):

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinhomes** | Lặp lại | Ban quản lý (BQL) tòa nhà nhận hàng trăm phản ánh/khiếu nại mỗi ngày qua App Vinhomes Resident (mất nước, rò rỉ ống dẫn, hỏng đèn hành lang, tiếng ồn, đỗ xe sai vị trí); nhân viên trực ban phải đọc từng tin nhắn, gán nhãn thủ công và tạo phiếu giao việc (ticket dispatch) cho tổ kỹ thuật hoặc tổ an ninh từng cụm tòa (mất 8-10 phút/ticket). |
| 2 | **VinFast** | Tốn thời gian | Kỹ thuật viên tại xưởng dịch vụ VinFast (3S) mất 20-30 phút/xe để tra cứu thủ công cẩm nang sửa chữa kỹ thuật điện (Service Manual) và sơ đồ mạch khi xe VF8/VF9 xuất hiện chuỗi mã lỗi chẩn đoán phức tạp (DTC code) kết hợp với mô tả hiện tượng gián đoạn từ chủ xe. |
| 3 | **Xanh SM** | Pain từ người khác | Tại các điểm đón đông đúc và phức tạp (cổng trung tâm thương mại Vincom, sảnh chung cư lớn, ngõ sâu), định vị GPS bị trôi khiến tài xế và hành khách phải gọi điện cho nhau 3-4 cuộc chỉ để tìm điểm hẹn; hệ thống gợi ý điểm đón chưa thông minh dẫn đến tỷ lệ hủy chuyến tăng cao (~15%) và tài xế bị áp lực dừng đỗ sai quy định. |
| 4 | **Vinpearl** | Tốn thời gian | Nhân viên kinh doanh Vinpearl mất 30-40 phút cho mỗi email đặt phòng theo đoàn (B2B Group Booking) từ các công ty lữ hành do email chứa nhiều yêu cầu phi cấu trúc (loại phòng hỗn hợp, ngày check-in/out lệch nhau, suất ăn kèm vé VinWonders), phải đối chiếu thủ công trên hệ thống quản lý khách sạn PMS Opera. |
| 5 | **Vinmec** | AI-upgrade | Bác sĩ điều trị tại Vinmec mất 25-35 phút cho mỗi ca xuất viện để đọc lại toàn bộ bệnh án điện tử (kết quả xét nghiệm, chẩn đoán hình ảnh, đơn thuốc) và soạn thảo bản "Tóm tắt hồ sơ xuất viện" (Discharge Summary) bằng ngôn ngữ y khoa kết hợp diễn giải dễ hiểu cho bệnh nhân tuân thủ điều trị tại nhà. |

---

## 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **Top 3 bài toán tiềm năng nhất** từ danh sách trên để hoàn thiện 3 thẻ bài toán:

---

### 🎴 Quick Problem Card #1 — Vinhomes: Tự động phân loại & Điều phối phản ánh cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tự động đọc hiểu, trích xuất thông tin phản ánh   │
│ của cư dân trên App Vinhomes Resident để phân loại và tạo   │
│ phiếu giao việc (ticket) đến đúng tổ kỹ thuật/dịch vụ tòa.  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: ________________ │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên trực ban Ban Quản lý (BQL)   │
│ tòa nhà (quá tải) & Cư dân (chờ xử lý sự cố quá lâu).       │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tiếp nhận ticket phản ánh của cư dân từ Resident App   │
│   ──> 2. Đọc nội dung tiếng Việt, tra cứu số căn hộ & tòa nhà│
│   ──> 3. Phân loại thủ công (Điện, Nước, PCCC, An ninh, Môi trường) │
│   ──> 4. Tạo lệnh và gọi điện/nhắn tin giao việc cho kỹ thuật│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 8-10 phút)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3: Tự động   │
│ phân tích ngôn ngữ tự nhiên, trích xuất mức độ khẩn cấp và  │
│ gán nhãn chuyên môn để tự động định tuyến ticket.           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   - Rút ngắn thời gian từ lúc nhận phản ánh đến khi bàn giao│
│     cho kỹ thuật viên từ 10 phút ──> dưới 1 phút.           │
│   - Tỷ lệ phân loại đúng tổ phụ trách đạt trên 95%.         │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

### 🎴 Quick Problem Card #2 — VinFast: Trợ lý tra cứu cẩm nang sửa chữa & chẩn đoán mã lỗi OBD

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Hỗ trợ kỹ thuật viên xưởng dịch vụ VinFast tra cứu│
│ nhanh sơ đồ mạch điện và quy trình khắc phục sự cố dựa trên │
│ tổ hợp mã lỗi OBD (DTC) và triệu chứng thực tế của xe điện. │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: ________________ │
│                                                             │
│ Ai đang đau (Actor)? Kỹ thuật viên xưởng dịch vụ 3S VinFast │
│ (mất nhiều giờ tra tài liệu dày cộp) & Khách hàng chờ xe.   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Cắm máy chẩn đoán đọc danh sách mã lỗi DTC             │
│   ──> 2. Mở file PDF tài liệu kỹ thuật Service Manual hàng trăm trang │
│   ──> 3. Tìm kiếm từng mã lỗi và đối chiếu sơ đồ mạch điện  │
│   ──> 4. Tổng hợp các nguyên nhân trùng lặp giữa các mã     │
│   ──> 5. Viết phiếu quy trình kiểm tra các bước đo điện áp/điện trở │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 25 phút/ca)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 & 4: RAG / LLM │
│ đọc hiểu tài liệu kỹ thuật, mapping tổ hợp mã lỗi và gợi ý  │
│ danh sách 3 điểm kiểm tra ưu tiên nhất kèm vị trí giắc cắm. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   - Rút ngắn thời gian tra cứu kỹ thuật từ 25 min ──> under 3 min.│
│   - Giảm 40% thời gian xe phải lưu tại xưởng để chẩn đoán.  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

### 🎴 Quick Problem Card #3 — Xanh SM: Gợi ý điểm đón thông minh (Smart Pick-up Point)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Tự động phân tích vị trí GPS và lịch sử giao thông│
│ tại các điểm đón phức tạp để gợi ý cho hành khách & tài xế  │
│ điểm hẹn đón xe thuận tiện nhất, tránh tắc đường và cấm dừng│
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: ________________ │
│                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM (loay hoay tìm khách, bị│
│ phạt dừng đỗ) & Hành khách (chờ lâu, phải đi bộ tìm xe).    │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách đặt xe tại vị trí GPS tự động (thường bị lệch)   │
│   ──> 2. Tài xế nhận cuốc, lái xe đến toạ độ định vị trên app│
│   ──> 3. Đến nơi không thấy khách, tài xế gọi điện thoại hỏi vị trí│
│   ──> 4. Hai bên gọi đi gọi lại mô tả đặc điểm xung quanh để tìm nhau │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 5-8 phút/cuốc)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1: Khi khách đặt │
│ xe ở toạ độ phức tạp, AI nhận diện khu vực và gợi ý ngay:   │
│ "Vui lòng đứng tại Cổng số 2 Vincom (điểm đón Xanh SM thuận tiện)" │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   - Giảm thời gian kết nối tìm thấy nhau từ 6 phút ──> dưới 2 phút.│
│   - Giảm tỷ lệ hủy cuốc do không tìm thấy khách từ 15% ──> dưới 4%.│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```
