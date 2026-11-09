# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Em sử dụng 4 lenses để tìm các vấn đề có thể xảy ra trong vận hành của một số công ty thành viên Vingroup. Các tình huống dưới đây là **giả thuyết để làm bài Lab**, chưa phải kết quả khảo sát trực tiếp tại doanh nghiệp.

### 📝 List bài toán của tôi:

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Vinpearl | Tốn thời gian (Time-consuming) | Trưởng ca buồng phòng phải sắp lịch dọn cho nhiều phòng có giờ nhận khách gần nhau và cập nhật lại khi có thay đổi. |
| 2 | VinFast | AI có thể tốt hơn (AI-upgrade) | Kỹ thuật viên cần rà soát nhiều thông số pin, nhiệt độ và lịch sử vận hành để tìm dấu hiệu bất thường cần kiểm tra thêm. |
| 3 | Vinhomes | Lặp lại (Repetitive) | Nhân viên kỹ thuật phải xem dữ liệu đồng hồ nước định kỳ để phát hiện những căn hộ có mức sử dụng bất thường. |
| 4 | Xanh SM | Pain từ người khác (Stakeholder Pain) | Khi xe tập trung ở một khu vực nhưng nhu cầu đón khách ở khu vực khác, tài xế có thể phải chờ cuốc lâu và khách chờ xe. |
| 5 | Vinmec | Tốn thời gian (Time-consuming) | Nhân viên quản lý thiết bị cần đối chiếu nhật ký sử dụng và lịch bảo trì để quyết định thiết bị nào cần kiểm tra trước. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

**Người thực hiện:** Nguyễn Gia Nam — phần scan và quick cards là bài cá nhân. Nhóm đã thống nhất chọn Vinpearl RoomFlow AI cho Phase 3–5.

Từ danh sách 5 bài toán ở Phase 1, em chọn **#1 Vinpearl RoomFlow AI, #4 Xanh SM DemandPulse AI và #2 VinFast Battery Forensics AI**. Em hoàn thiện 3 Quick Problem Cards theo đúng các trường trong worksheet. Quy trình, thời gian và chỉ tiêu dưới đây là **giả định để thiết kế MVP**, chưa được khảo sát hay đo tại doanh nghiệp.

## QUICK PROBLEM CARD #1 — Vinpearl RoomFlow AI — hỗ trợ lập lịch dọn phòng

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
└─────────────────────────────────────────────────────────────┘
Bài toán (1 câu): Vinpearl RoomFlow AI — hỗ trợ lập lịch dọn phòng.
Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [x] Khác
Khác (ghi rõ): Vinpearl
Ai đang đau (Actor)? Trưởng ca buồng phòng; nhân viên dọn phòng; lễ tân.

Workflow thủ công hiện tại (3–5 bước):
1. Lễ tân chuyển danh sách phòng và giờ nhận khách.
2. Trưởng ca sắp mức ưu tiên.
3. Trưởng ca phân công nhân viên.
4. Nhân viên nhận việc, dọn phòng.
5. Trưởng ca nhận tiến độ và điều chỉnh lịch.

Bước nào tốn thời gian/lỗi nhất? Bước 3, khoảng 5 phút/lượt lập lịch (giả định).
AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3: thuật toán Rule/Optimization đề xuất lịch; LLM chỉ giải thích nháp khi cần.
Đo thành công bằng gì (Metric có số)? MVP 20 phòng/4 nhân viên; lập lịch dưới 30 giây; 0 phân công trùng giờ; mục tiêu giảm >=20% phòng trễ so với baseline khi baseline có phòng trễ.
Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent
```

**Lý do em đưa vào Top 3:** Có người dùng và luồng công việc rõ, dễ dựng dữ liệu thử và đo được thời gian lập lịch, số phòng trễ. Lợi ích kinh tế có thể đến từ giảm công điều phối và hạn chế phòng giao trễ, nhưng chưa có số liệu chứng minh doanh thu tăng.

## QUICK PROBLEM CARD #2 — Xanh SM DemandPulse AI — dự báo nhu cầu đặt xe

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
└─────────────────────────────────────────────────────────────┘
Bài toán (1 câu): Xanh SM DemandPulse AI — dự báo nhu cầu đặt xe.
Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác

Ai đang đau (Actor)? Điều phối viên; tài xế; khách chờ xe.

Workflow thủ công hiện tại (3–5 bước):
1. Thu thập số cuốc theo khu vực/giờ.
2. Điều phối viên theo dõi nhu cầu hiện tại.
3. Ước lượng khu vực sắp thiếu xe.
4. Đề xuất tài xế chuyển khu vực.

Bước nào tốn thời gian/lỗi nhất? Bước 3, thời gian xử lý thực tế chưa có; tạm giả định 10 phút mỗi lượt rà soát.
AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3: mô hình dự báo nhu cầu 30 phút tiếp theo; rule tạo gợi ý, con người quyết định.
Đo thành công bằng gì (Metric có số)? Thử trên >=7 ngày dữ liệu mô phỏng; mục tiêu MAE thấp hơn >=15% so với baseline trung bình lịch sử; không tự điều chuyển xe.
Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent
```

**Lưu ý:** Dự báo nhu cầu bằng mô hình ML là hướng nâng cấp sau; ô Rule ở đây chỉ mô tả MVP baseline.

**Lý do em đưa vào Top 3:** Có thể giúp tăng số chuyến phục vụ và giảm thời gian xe chờ, liên quan trực tiếp tới doanh thu đội xe. Tuy nhiên dữ liệu đặt xe theo vị trí/giờ khó có đủ để kiểm chứng hiệu quả thật.

## QUICK PROBLEM CARD #3 — VinFast Battery Forensics AI — phát hiện log pin bất thường

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
└─────────────────────────────────────────────────────────────┘
Bài toán (1 câu): VinFast Battery Forensics AI — phát hiện log pin bất thường.
Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác

Ai đang đau (Actor)? Kỹ thuật viên kiểm tra pin; bộ phận bảo trì.

Workflow thủ công hiện tại (3–5 bước):
1. Hệ thống xuất log pin.
2. Kỹ thuật viên xem nhiệt độ, điện áp, dòng điện.
3. Đối chiếu biến động để phát hiện điểm bất thường.
4. Ghi nhận trường hợp cần kiểm tra chuyên môn.

Bước nào tốn thời gian/lỗi nhất? Bước 2–3, khoảng 10 phút/log (giả định).
AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: mô hình phát hiện bất thường đánh dấu đoạn log; không tự kết luận pin an toàn/hỏng.
Đo thành công bằng gì (Metric có số)? Tối thiểu 100 chuỗi dữ liệu mô phỏng có nhãn; mục tiêu recall >=90%; báo cáo precision và false-positive rate; 0 lệnh điều khiển xe tự động.
Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent
```

**Lưu ý:** Phát hiện bất thường bằng ML là hướng mở rộng; Rule ở đây là baseline ngưỡng để so sánh.

**Lý do em đưa vào Top 3:** Có thể giảm công rà soát và hỗ trợ bảo trì, giá trị tài chính tiềm năng lớn; nhưng dữ liệu chuyên môn, độ tin cậy và rủi ro an toàn khiến MVP khó hơn.

---

## 🗳️ 1 ý tưởng em tâm đắc nhất (đề xuất cá nhân)

**Em chọn: Card #1 — Vinpearl RoomFlow AI.**

Em chọn ý tưởng này vì trong ba phương án, đây là bài toán dễ xác định **ai dùng**, **đang vướng ở bước nào**, **MVP phải làm gì** và **đo kết quả ra sao**. Em có thể tạo bộ dữ liệu 20 phòng/4 nhân viên, so sánh lịch thủ công (baseline) với lịch thuật toán đề xuất, kiểm tra xung đột phân công và số phòng hoàn thành trễ. Trưởng ca vẫn phải duyệt lịch; Gemini chỉ hỗ trợ giải thích, không tự phân công.

**Khả năng tạo doanh thu/giá trị tài chính:** Nếu giải pháp thực sự giảm thời gian điều phối hoặc giảm số phòng giao trễ, nó có thể giúp khách sạn tiết kiệm chi phí vận hành và là cơ sở phát triển phần mềm thu phí theo cơ sở. Đây mới là giả thuyết thương mại, không phải doanh thu đã đạt được. Muốn chứng minh phải đo baseline, chi phí triển khai, mức tiết kiệm thực tế và hỏi người vận hành có sẵn sàng dùng/trả tiền hay không.

**Vì sao chưa ưu tiên 2 ý tưởng còn lại?** Xanh SM có tiềm năng tài chính hấp dẫn nhưng phụ thuộc dữ liệu nhu cầu đặt xe thực tế; VinFast cần dữ liệu pin có nhãn và kiểm định chuyên môn vì liên quan an toàn. Hai ý tưởng này không kém giá trị, chỉ khó kiểm chứng trong phạm vi Lab hơn.

**Kết quả thảo luận:** Sau khi các thành viên trình bày, nhóm đã thống nhất chọn **Vinpearl RoomFlow AI** để thực hiện Phase 3–5. Đây là lựa chọn cá nhân sau khi so sánh khả năng làm MVP, dữ liệu và rủi ro; không phải kết quả kiểm thử.
