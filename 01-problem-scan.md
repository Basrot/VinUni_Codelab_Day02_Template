# Lab 02 - Problem Scan & Quick Assessment

## Phase 1 - SCAN: Quét cơ hội vận hành

> Yêu cầu Rubric (Gate I1): Liệt kê tối thiểu 5 bài toán/điểm nghẽn thực tế tại các công ty thành viên Vingroup, sử dụng tối thiểu 3 trong 4 Lenses (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác).

| # | Subsidiary (VinFast / Xanh SM / Vinhomes / Vinmec / Vinpearl / VinUni) | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Xanh SM | Lặp lại | Tài xế phải gọi điện cho khách ở hầu hết các cuốc xe để báo xe đã tới (do khách đặt xong thường cất điện thoại không nhìn app) và hỏi lại vị trí đứng cụ thể khi điểm đón bị khuất tầm nhìn, vừa mất thời gian vừa gây mất tập trung khi lái xe. |
| 2 | VinUni | Pain từ người khác | Sổ tay sinh viên và quy chế học vụ khá dài, lại nằm qua nhiều bước tra cứu nên sinh viên ngại tự đọc mà hỏi thẳng phòng Giáo vụ. Nhân viên phải trả lời đi trả lời lại các câu hỏi giống nhau, còn các bạn sinh viên khác phải chờ phản hồi lâu. |
| 3 | Vinmec | AI có thể tốt hơn | Trong một ca khám ngắn, bác sĩ vừa phải hỏi bệnh, vừa đọc lại bệnh sử cũ dài, vừa gõ máy tính nhập phiếu khám. Làm nhiều việc cùng lúc dễ làm bác sĩ phân tâm, đọc sót thông tin cũ hoặc gõ nhầm chi tiết vào hồ sơ. |
| 4 | Vinhomes | Tốn thời gian | Nhân viên CSKH Ban quản lý phải mở đọc từng phản ánh và xem ảnh cư dân gửi lên để xác nhận rồi mới chia việc bằng tay cho từng đội kỹ thuật (điện, nước, an ninh). Cách làm thủ công này làm đội kỹ thuật phải chờ lệnh, hoặc nếu CSKH phân loại nhầm thì thợ đến nơi lại phải bàn giao lại cho đội khác. |
| 5 | Vinpearl | Tốn thời gian | Bộ phận Quản lý chất lượng phải gom đánh giá của khách từ nhiều trang (Booking, Agoda, Google Maps...) với đủ dạng chữ nhiều thứ tiếng, ảnh chụp, điểm sao, rồi ngồi phân loại thủ công theo từng mảng (phòng ở, thái độ phục vụ, thủ tục) để làm báo cáo riêng cho từng bộ phận. |

---

## Phase 2 - QUICK-ASSESS: 3 Quick Problem Cards

> Yêu cầu Rubric (Gate I1): Chọn top 3 bài toán tiềm năng nhất từ bảng trên và hoàn thiện đầy đủ 3 thẻ dưới đây.

### Quick Problem Card #1

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Tài xế phải gọi điện lặp lại ở gần như    │
│ mọi cuốc xe để báo khách ra xe và hỏi vị trí đứng thực tế.  │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác:                  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM và người đặt xe         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tài xế chạy xe theo định vị GPS đến gần điểm ghim      │
│   ──> 2. Dừng xe, mở điện thoại bấm gọi báo khách ra điểm   │
│   ──> 3. Hỏi qua lại trên điện thoại để tìm nhau nếu khuất  │
│   ──> 4. Di chuyển xe tới đúng chỗ khách đứng và đón khách  │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 2-4 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│   - Bước 2: App tự thực hiện cuộc gọi tự động nhắc khách    │
│     khi xe còn cách điểm đón 150m-200m (Rule).              │
│   - Bước 3: Khách nói ngắn gọn 1 câu hoặc chụp ảnh chỗ đứng,│
│     mô hình đa phương thức (LLM) đối chiếu biển hiệu trên   │
│     bản đồ rồi đọc chỉ dẫn ngắn qua loa cho tài xế.         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Giảm thời gian liên hệ và chờ đón từ ~3 phút xuống      │
│     dưới 1 phút/cuốc.                                       │
│   - Giảm tỷ lệ cuốc xe tài xế phải tự bấm gọi điện từ ~90%  │
│     xuống dưới 20%.                                         │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #2

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tài liệu quy chế dài và khó tìm khiến     │
│ sinh viên dồn câu hỏi giống nhau về phòng Giáo vụ, gây chờ  │
│ đợi lâu cho cả sinh viên lẫn nhân viên xử lý.               │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: VinUni           │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên Giáo vụ và sinh viên VinUni  │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Sinh viên thử tìm trong Sổ tay/email nhưng dài, khó dò │
│   ──> 2. Gửi email hoặc lên trực tiếp phòng Giáo vụ hỏi     │
│   ──> 3. Nhân viên Giáo vụ đọc câu hỏi, mở file quy chế dò  │
│   ──> 4. Nhân viên gõ câu trả lời giải thích cho từng bạn   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 10-15 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│   - Bước 1, 3 & 4: Chatbot dùng LLM (kết hợp tra cứu RAG)   │
│     đọc Sổ tay sinh viên để trả lời ngay kèm trích dẫn mục  │
│     quy định, hoặc soạn sẵn bản nháp trả lời cho Giáo vụ.   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Giảm trên 50% thời gian sinh viên chờ phản hồi (thời    │
│     gian tra cứu câu hỏi thường giảm từ 10-15p xuống <30s). │
│   - Giải đáp tự động được khoảng 60%-70% câu hỏi lặp lại.   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #3

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Cư dân mô tả sự cố thiếu rõ ràng và CSKH  │
│ phải đọc phân loại thủ công từng phiếu để chia cho đội kỹ   │
│ thuật, dễ chia nhầm đội và làm chậm thời gian sửa chữa.     │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác:                  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH Ban quản lý, đội kỹ     │
│                      thuật (điện/nước/an ninh) và cư dân    │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Cư dân chụp ảnh sự cố kèm mô tả ngắn gửi lên app       │
│   ──> 2. CSKH mở xem từng phiếu, đọc chữ và nhìn ảnh đoán lỗi│
│   ──> 3. CSKH xem lịch trực và chia việc bằng tay cho đội thợ│
│   ──> 4. Thợ đến nơi kiểm tra và sửa (nếu CSKH phân nhầm bộ │
│          phận thì phải báo chuyển lại cho đội khác)         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 1, 2 & 3 (⏱ 10-20 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│   - Cuối Bước 1 & Bước 2: AI Agent đọc ảnh + mô tả, nếu ảnh │
│     mờ hoặc thiếu vị trí thì hỏi lại cư dân ngay để xác     │
│     định đúng loại hỏng hóc.                                │
│   - Bước 3: Tự tra ca trực để gợi ý phiếu giao đúng đội kỹ  │
│     thuật kèm dụng cụ cần mang theo.                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Giảm thời gian từ lúc nhận phản ánh đến lúc giao đúng   │
│     đội thợ từ 10-20 phút xuống dưới 1 phút/phiếu.          │
│   - Giảm tỷ lệ phân công nhầm bộ phận kỹ thuật từ ~15%-20%  │
│     xuống dưới 3%.                                          │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘
```
