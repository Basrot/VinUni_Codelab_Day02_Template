# Nhật ký sử dụng AI & Phản ánh cá nhân (AI Log & Reflection)

* **Họ và tên:** Đào Ngọc Hân (`2A202603779`)
* **Đề tài nhóm:** Vinpearl RoomFlow AI (Hỗ trợ phân công nhân viên dọn phòng giờ cao điểm)

---

## 1. Cách mình phối hợp với AI trong buổi Lab

Ở Phase 1 và Phase 2, vì mình chưa có nhiều trải nghiệm thực tế bên trong các công ty của Vingroup (như quy trình nội bộ của Vinmec, Vinhomes hay Vinpearl), nếu nhờ AI liệt kê sẵn 5 bài toán ngay từ đầu thì mình sẽ chỉ chép lại mà không hiểu bản chất. Vì vậy, mình yêu cầu AI đóng vai người hỏi gợi mở (theo kiểu Socratic): mỗi lần chỉ đặt đúng 1 câu hỏi ngắn, không đưa đáp án trước, đợi mình tự trả lời theo suy nghĩ cá nhân rồi mới góp ý và bổ sung số liệu.

Cách làm này hơi mất thời gian hơn ở đoạn đầu nhưng giúp mình tự nhìn ra nguyên nhân gốc của từng vấn đề. Ví dụ như ở bài toán VinUni, ban đầu mình chỉ thấy phòng Giáo vụ tốn thời gian trả lời câu hỏi lặp lại; khi bị hỏi ngược lại là *"tại sao trường đã có Sổ tay sinh viên mà sinh viên vẫn hỏi?"*, mình mới nhận ra vấn đề nằm ở việc file quy chế dài và phải qua nhiều bước mới tìm thấy nên sinh viên ngại đọc. Hay ở bài toán Vinhomes, mình tự lần ra được việc cư dân mô tả sai ngay từ bước đầu dẫn đến CSKH phân loại nhầm đội thợ ở bước sau.

---

## 2. Những điểm AI đã hỗ trợ hiệu quả

1. **Giúp nhìn ra điểm yếu nếu lạm dụng AI cho bài toán của nhóm:**
   Khi nhóm thống nhất chuyển sang làm đề tài **Vinpearl RoomFlow AI** (phân công nhân viên dọn phòng đúng phòng, đúng người, đúng thời điểm), AI đã giúp phản biện một câu hỏi rất thực tế: *"Nếu chỉ chia phòng theo khoảng cách tầng và số lượng phòng đã làm thì viết thuật toán Rule-based bình thường sẽ nhanh và chuẩn hơn, tại sao lại cần LLM?"*. Nhờ điểm này, bọn mình không dùng AI ôm đồm toàn bộ việc chia ca hay dùng Agent tự động đổi lịch liên tục, mà tách rõ: dùng Rule lọc nhân viên đang rảnh và gần phòng trước, còn LLM chỉ dùng để đọc các ghi chú phát sinh bằng tiếng Việt từ Lễ tân/bộ đàm (như khách VIP cần nôi em bé, dị ứng mùi tinh dầu, hoặc phòng bẩn đặc biệt) rồi tạo bản nháp `[DRAFT_ONLY]` cho Giám sát bấm duyệt.
2. **Hỗ trợ viết code kiểm thử ranh giới an toàn (Phase 4):**
   AI giúp mình cụ thể hóa các quy định nghiệp vụ thành cấu trúc JSON rõ ràng trong `SYSTEM_PROMPT` và viết script Python kiểm tra tự động cả 3 tình huống gài lỗi (ép mở phòng chưa kiểm tra, ép nhân viên sắp hết ca/hết pin xe đi xử lý kính vỡ và rò điện, gài lệnh Prompt Injection để lấy số hộ chiếu và số điện thoại khách).

---

## 3. Những chỗ AI hoặc công cụ bị sai / gặp lỗi và cách mình sửa lại

Trong quá trình làm, có 4 điểm thực tế không giống như gợi ý ban đầu của AI hoặc code mẫu mà mình đã phải điều chỉnh lại:

1. **Chỉnh lại giả định chưa sát thực tế ở bài toán Xanh SM (Phase 1):**
   Lúc đầu AI tóm tắt theo hướng tài xế gọi điện cho khách chủ yếu khi định vị GPS bị lệch hoặc khuất tầm nhìn. Mình đã phản hồi lại ngay là ngoài đời thực, kể cả khi GPS chuẩn thì tài xế vẫn phải gọi ở hầu hết các cuốc xe, vì khách đặt xe xong thường cất điện thoại làm việc khác chứ không nhìn màn hình app; nếu tài xế đến nơi mà không gọi đổ chuông thì khách vẫn ngồi trong nhà đợi. Từ đó phương án ở thẻ số 1 mới bổ sung bước cuộc gọi nhắc tự động khi xe sắp tới thay vì chỉ xử lý lệch bản đồ.
2. **Lỗi `404 NOT_FOUND` khi chạy model mặc định `gemini-2.5-flash`:**
   Trong hướng dẫn và file mẫu `prompt_prototype.py` để mặc định tên model là `gemini-2.5-flash`. Khi mình nạp API key mới vào `.env` và chạy thử thì Google API trả về lỗi `404` báo model này không còn mở cho người dùng mới nữa và gợi ý đổi sang `gemini-3.8-flash`.
3. **Sửa tiếp lỗi `400` và lỗi quá thời gian chạy (`Timeout > 30s`) khi đổi model:**
   Khi đổi sang `gemini-3.8-flash` và thử đặt cấu hình `ThinkingLevel.MINIMAL` để chạy cho nhanh thì API báo lỗi `400 INVALID_ARGUMENT` (do model không nhận mức `MINIMAL`). Khi đổi sang mức `LOW`, cả 3 test đều ra kết quả JSON đúng quy tắc an toàn, nhưng tổng thời gian chạy mất hơn 30 giây (do model tốn thời gian suy luận ngầm cộng với kết nối mạng trên máy Windows của mình thử IPv6 trước rồi bị reset kết nối `WinError 10054`), làm script chấm tự động bị báo fail timeout.
   *Cách xử lý:* Mình kiểm tra lại danh sách các model `flash` đang mở trên key, đo thử tốc độ thực tế và chuyển sang dùng `gemini-3.5-flash` kèm cấu hình `thinking_budget=0`, ép kết nối qua IPv4 (`local_address="0.0.0.0"`) và cho 3 câu test chạy song song bằng `ThreadPoolExecutor`. Nhờ vậy tổng thời gian chạy toàn bộ file giảm xuống còn khoảng 10 giây và vượt qua hết các bài kiểm tra.
4. **Sửa lại cách trình bày báo cáo và sơ đồ quy trình:**
   Bản nháp văn bản và sơ đồ `04-workflow-diagram.png` đầu tiên do AI sinh ra dùng hơi nhiều từ ngữ bóng bẩy, nhiều icon và màu sắc giống giao diện quảng cáo hơn là sơ đồ kỹ thuật (thậm chí lần xuất ảnh đầu còn bị tràn chữ ở tiêu đề và ô chuyển giao). Mình đã yêu cầu lược bỏ các cách diễn đạt màu mè, sửa lỗi lặp dòng do thao tác gộp diff trong lúc sửa file, và vẽ lại sơ đồ theo chuẩn lưu đồ phân làn (Swimlane) tối giản, rõ các bước chuyển giao và điểm nghẽn.

---

## 4. Bài học rút ra

* Dùng AI hiệu quả nhất là để nó đặt câu hỏi phản biện lại ý tưởng của mình (như việc hỏi vặn tại sao không dùng code Rule-based thông thường), chứ không phải nhờ nó viết hộ càng dài càng tốt.
* Ranh giới an toàn cho AI không thể chỉ ghi trên tài liệu mà phải khóa bằng định dạng đầu ra cố định (`[DRAFT_ONLY]` + trường `action` rõ ràng trong JSON) và có test kiểm tra các trường hợp người dùng cố tình ép bỏ quy trình (như lấy lý do khách VIP đang giục ở sảnh).
* Mọi thiết kế prompt hay cấu hình model trên lý thuyết đều phải chạy thử trực tiếp bằng code thật mới phát hiện được các vấn đề thực tế như model ngừng hỗ trợ hay độ trễ vượt quá giới hạn cho phép.
