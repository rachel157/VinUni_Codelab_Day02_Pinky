# 📝 03 — AI Log & Critical Reflection (Nhật Ký Tương Tác AI)

> **Dự án:** Vin Smart Future — AI Product Scoping (Vinmec Healthcare Use Case)  
> **Mục tiêu:** Chiêm nghiệm trung thực về quá trình cộng tác với AI (Gemini, Claude, ChatGPT) với vai trò là người đồng hành tư duy (**Thought-Partner**), phân tích các điểm AI hỗ trợ xuất sắc, các tình huống AI bị ảo giác/đưa ra giải pháp sai lầm, và cách tôi đã can thiệp để thiết lập ranh giới an toàn.

---

## 🤖 1. AI Đã Hỗ Trợ Gì Trong Buổi Lab? (AI as a Thought-Partner)

Trong suốt quá trình làm bài, tôi đã sử dụng các mô hình ngôn ngữ lớn (LLM) không phải như một "cỗ máy viết hộ", mà như một **Chuyên gia phản biện khắt khe** và **Trợ lý kỹ thuật**:

1. **Brainstorm & Mở rộng góc nhìn theo 4 Lenses (Phase 1):**
   * AI giúp tôi quét qua toàn bộ hệ sinh thái của Vingroup (Vinmec, VinFast, Vinhomes, Vinpearl, VinUni) để phát hiện ra các quy trình thủ công đang âm thầm gây rò rỉ chi phí mà bản thân chưa từng có cơ hội làm việc thực địa.
   * Gợi ý ước lượng số liệu định lượng (ví dụ: thời gian bác sĩ làm thủ tục xuất viện trung bình 25–35 phút/ca, chiếm tới 20–30 giờ công mỗi ngày tại mỗi cơ sở bệnh viện).

2. **Cấu trúc hóa Problem Statement 6-field (Phase 3):**
   * AI hỗ trợ chuẩn hóa ngôn ngữ từ mô tả cảm tính thành ngôn ngữ kỹ thuật tiêu chuẩn của Vin Smart Future: định rõ vai trò Actor, bóc tách Current Flow thành 5 bước, và lượng hóa Metric thành các chỉ số đo lường được (Efficiency, Adoption, Safety).

3. **Thiết kế Kịch bản Tấn công Prompt (Phase 4 — Adversarial Testing):**
   * AI đóng vai trò là "Kẻ tấn công (Red Teaming)", tự sinh ra các prompt tinh vi nhằm cố tình vượt rào (Jailbreak, ép bỏ thẻ `[DRAFT_ONLY]`, mượn danh lãnh đạo cấp cao) để kiểm tra độ vững chắc của System Prompt.

---

## ⚠️ 2. AI Đã Trả Lời Sai Ở Đâu? (Hallucination & Dangerous Suggestions)

Trong quá trình tìm hiểu giải pháp cho **Vinmec (Y tế thông minh)**, các mô hình LLM đã bộc lộ những thiên kiến và sai lầm cực kỳ nguy hiểm nếu áp dụng vào thực tế mà không có con người giám sát:

### ❌ Sai lầm 1: Đề xuất AI tự động ký duyệt và gửi thẳng hồ sơ cho bệnh nhân (Mất kiểm soát HITL)
* **Câu trả lời ban đầu của AI:** AI đề xuất xây dựng một "Autonomous Agent" có khả năng tự động đọc EMR, tự sinh bản tóm tắt xuất viện và tự động đẩy thông báo kèm file PDF về ứng dụng MyVinmec của bệnh nhân nhằm "tối đa hóa tốc độ xử lý xuống dưới 10 giây".
* **Nguy cơ thực tế:** Đây là một sai lầm chết người trong y khoa. Theo quy định của Bộ Y Tế và tiêu chuẩn JCI, Bản Tóm Tắt Xuất Viện là văn bản pháp lý bắt buộc phải có chữ ký xác nhận của Bác sĩ điều trị. Nếu AI trích xuất sai chỉ số men gan hoặc liều lượng kháng sinh, bệnh nhân có thể gặp biến chứng nguy kịch mà không ai chịu trách nhiệm pháp lý.

### ❌ Sai lầm 2: AI tự ý suy diễn và "bịa" đơn thuốc ra viện (Clinical Hallucination)
* **Hiện tượng:** Khi tôi đưa vào một đoạn tóm tắt bệnh án thử nghiệm bị thiếu thông tin ngày tái khám và liều thuốc duy trì tại nhà, mô hình LLM đã tự động "suy đoán" và bổ sung một đơn thuốc thông thường dựa trên bệnh lý chẩn đoán.
* **Nguy cơ thực tế:** Hiện tượng "ảo giác" (hallucination) này có thể dẫn đến việc cấp phát thuốc sai cho bệnh nhân. Trong y tế, **dữ liệu thiếu phải được khai báo là thiếu**, tuyệt đối không được dùng xác suất để đoán mò.

---

## 🛡️ 3. Tôi Đã Can Thiệp Và Sửa Ranh Giới (Prompt Boundaries) Như Thế Nào?

Để khắc phục hoàn toàn các sai lầm trên của AI, tôi đã tiến hành "đóng khung ranh giới thép" (**Hard Operational Boundaries**) cho hệ thống:

### 🔧 Can thiệp 1: Ép buộc 100% Human-in-the-loop qua thẻ định danh
* Bắt buộc mọi bản thảo AI sinh ra phải bắt đầu bằng thẻ `[DRAFT_CLINICAL_SUMMARY]`.
* Trong System Prompt, cấm AI sinh ra bất kỳ API call nào có tính năng tự động gửi (auto-send/auto-publish). Bản thảo chỉ hiển thị trên giao diện làm việc của Bác sĩ để Bác sĩ đọc, chỉnh sửa và bấm Ký số điện tử (E-signature).

### 🔧 Can thiệp 2: Quy tắc cấm suy diễn (Strict Grounding on EMR)
* Thiết lập chỉ thị nghiêm ngặt: *"Chỉ được phép trích xuất thông tin xuất hiện nguyên văn trong EMR của bệnh nhân. Tuyệt đối không tự suy diễn chẩn đoán mới, không tự thay đổi liều lượng thuốc."*
* Bổ sung cơ chế kích hoạt cờ báo động `[WARNING_MISSING_DATA]`: Nếu phát hiện hồ sơ thiếu xét nghiệm quan trọng hoặc có sự mâu thuẫn giữa các khoa, AI buộc phải dừng lại và yêu cầu Bác sĩ kiểm tra trực tiếp.

### 🔧 Can thiệp 3: Cơ chế Fallback an toàn (Kế hoạch dự phòng)
* Nếu hệ thống AI gặp lỗi, mất kết nối mạng hoặc trả về kết quả không tự tin, quy trình sẽ ngay lập tức kích hoạt Fallback: trả quyền điều khiển về cho Bác sĩ tự gõ tay truyền thống như quy trình cũ, đảm bảo bệnh viện không bao giờ bị tê liệt vận hành.

---

## 💡 4. Bài Học Chiêm Nghiệm Cá Nhân (Key Takeaways)

1. **"Problem First, AI Second":** Bài lab giúp tôi hiểu rằng không phải cứ dùng mô hình Agent phức tạp là tốt. Với bài toán y tế của Vinmec, một tính năng LLM Feature đơn giản kết hợp RAG và sự giám sát chặt chẽ của Bác sĩ mang lại giá trị thực tế cao hơn gấp nhiều lần một hệ thống tự trị rủi ro cao.
2. **AI là Trợ Lý (Co-Pilot), không phải Thay Thế (Autopilot):** Trong các lĩnh vực nhạy cảm liên quan đến con người như Y tế (Vinmec) hay An toàn xe điện (VinFast), ranh giới vận hành an toàn (**Operational Boundary**) chính là lằn ranh sinh tử phân biệt giữa một giải pháp công nghệ có ích và một thảm họa kỹ thuật.
3. **Kỹ năng Prompting của Kỹ sư AI:** Viết prompt cho hệ thống AI doanh nghiệp không phải là nói chuyện phiếm, mà là lập trình quy tắc logic bằng ngôn ngữ tự nhiên với đầy đủ rào chắn phòng vệ trước các cuộc tấn công Adversarial Attack.
