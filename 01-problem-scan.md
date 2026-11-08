# Lab 02 — Quét cơ hội và Quick Problem Cards

## Phạm vi và độ tin cậy

Bài làm theo tình huống Vin Smart Future trong đề bài. Chưa có phỏng vấn, log nội bộ hay khảo sát thực địa. Các thời gian, sản lượng và ngưỡng mục tiêu dưới đây là **giả định để thiết kế thử nghiệm**, không phải số liệu vận hành đã xác minh của doanh nghiệp. Không sử dụng thông tin khách hàng thật.

## Phase 1 — SCAN

| # | Đơn vị theo tình huống đề bài | Lens | Bài toán cụ thể | Dữ liệu cần xác minh |
|---|---|---|---|---|
| 1 | Xanh SM | Tốn thời gian; stakeholder pain | Điều phối viên phải đọc báo cáo pin thấp, xác nhận vị trí và soạn hướng dẫn cho tài xế. | Log thời gian từng bước, pin, vị trí, kết quả xử lý |
| 2 | VinFast | Lặp lại | Đối soát hóa đơn sạc với giao dịch để tìm bản ghi thiếu hoặc trùng. | Hóa đơn và giao dịch đã ẩn danh; ưu tiên SQL/rule trước AI |
| 3 | Vinhomes | AI-upgrade; lặp lại | Phân loại phản ánh cư dân viết tự do để chuyển đúng bộ phận và dự thảo xác nhận tiếp nhận. | Ticket, nhãn bộ phận, danh mục dịch vụ được duyệt |
| 4 | Vinpearl / VinWonders | AI-upgrade; tốn thời gian | Nhân viên phải tra nhiều mục FAQ khi trả lời câu hỏi nhiều ý về dịch vụ. | FAQ có phiên bản, câu hỏi mẫu; không cho AI tự tạo giá |
| 5 | Vinmec | Stakeholder pain; tốn thời gian | Nhân viên hành chính đọc yêu cầu đặt lịch tự do để xác định thông tin còn thiếu. | Yêu cầu đã ẩn danh, danh mục chuyên khoa, quy tắc chuyển người |
| 6 | Xanh SM | Lặp lại; tốn thời gian | Tổng hợp ghi chú hủy chuyến thành nhóm nguyên nhân cho báo cáo tuần. | Ghi chú ẩn danh, nhãn nguyên nhân và tỷ lệ bất đồng giữa người gán nhãn |

## Phase 2 — QUICK-ASSESS

### Card 1 — Trợ lý điều phối sự cố pin thấp (Xanh SM)

- **Bài toán:** Rút ngắn thời gian từ lúc nhận báo cáo pin thấp đến khi điều phối viên duyệt phương án hỗ trợ.
- **Actor:** Điều phối viên là người dùng trực tiếp; tài xế là người chịu thời gian chờ.
- **Workflow hiện tại:** (1) Nhận báo cáo → (2) xác minh pin/vị trí → (3) tra phương án sạc hoặc hỗ trợ → (4) soạn và kiểm tra hướng dẫn → (5) liên hệ tài xế/đội hỗ trợ.
- **Bottleneck giả định:** Bước 3 mất 5 phút, bước 4 mất 4 phút; tổng toàn quy trình 15 phút/lượt, chưa tính di chuyển.
- **AI hỗ trợ:** Chuyển thông tin ngôn ngữ tự nhiên thành bản nháp ngắn có cấu trúc; không tự tìm trạm, không tự điều xe.
- **Metric:** Thử nghiệm giảm trung vị thời gian đến bản nháp được duyệt từ baseline giả định 15 xuống ≤5 phút; 100% đầu ra cần duyệt, không chấp nhận vi phạm ranh giới trong bộ test.
- **Quick Architecture:** Rule cho ngưỡng pin và kiểm tra dữ liệu + LLM Feature cho soạn nháp; không dùng Agent.
- **Giả định/rủi ro:** Chưa có nguồn vị trí/trạm sạc hay cam kết đội hỗ trợ. Khi pin <5%, chỉ dự thảo yêu cầu hỗ trợ di động; người phụ trách xác nhận khả năng phục vụ hoặc chuyển cứu hộ theo quy trình được duyệt.

### Card 2 — Phân loại phản ánh cư dân (Vinhomes)

- **Bài toán:** Giảm thao tác đọc và chuyển ticket sai bộ phận.
- **Actor:** Nhân viên chăm sóc cư dân, kỹ thuật và cư dân gửi phản ánh.
- **Workflow hiện tại:** (1) Đọc phản ánh → (2) hỏi thông tin thiếu → (3) chọn bộ phận → (4) soạn xác nhận → (5) chuyển ticket.
- **Bottleneck giả định:** Phân loại và soạn xác nhận mất 6/10 phút xử lý chủ động mỗi ticket; không bao gồm chờ bộ phận tiếp nhận.
- **AI hỗ trợ:** Gợi ý nhãn, thông tin thiếu và câu xác nhận từ danh mục dịch vụ đã duyệt.
- **Metric:** Mục tiêu thời gian xử lý chủ động ≤4 phút/ticket; macro-F1 phân loại ≥0,90 trên 100 ticket ẩn danh được hai nhân viên gán nhãn; người duyệt mọi phản hồi.
- **Quick Architecture:** Rule định tuyến trường hợp rõ ràng + LLM cho văn bản mơ hồ; không Agent.
- **Ranh giới:** Không quyết định phí, bồi thường, trách nhiệm pháp lý; nội dung khẩn cấp chuyển trực tiếp người phụ trách. Cần xác minh danh mục và quyền truy cập dữ liệu.

### Card 3 — Tổng hợp nguyên nhân hủy chuyến (Xanh SM)

- **Bài toán:** Giảm thời gian tổng hợp ghi chú hủy chuyến mà vẫn truy nguyên được kết luận.
- **Actor:** Chuyên viên vận hành lập báo cáo tuần.
- **Workflow hiện tại:** (1) Xuất ghi chú → (2) ẩn danh/lọc trùng → (3) đọc và gán nhóm → (4) đếm theo nhóm → (5) viết nhận xét và kiểm tra.
- **Bottleneck giả định:** Đọc, gán nhóm và viết nhận xét mất 90/120 phút cho một lô 100 ghi chú.
- **AI hỗ trợ:** Đề xuất nhãn và tóm tắt kèm mã bản ghi; tính số lượng bằng code, không để LLM tự đếm.
- **Metric:** Mục tiêu ≤45 phút/lô 100 bản ghi; macro-F1 ≥0,85 với bộ nhãn chuẩn; 100% nhận xét có mã bằng chứng; không quy trách nhiệm cá nhân từ suy đoán.
- **Quick Architecture:** Rule/SQL cho lọc và đếm + LLM Feature cho phân nhóm văn bản, có người kiểm tra.
- **Rủi ro:** Ghi chú thiên lệch hoặc thiếu nguyên nhân; cho phép nhãn “không đủ thông tin”, không suy diễn động cơ tài xế.

## Lựa chọn để phân tích sâu

Chọn **Card 1** vì phù hợp prototype và ranh giới pin của starter code, có thể kiểm tra bằng dữ liệu tổng hợp mà không kết nối hệ thống điều xe thật. Card 2 cần taxonomy và quy trình chuyển ticket đã duyệt; Card 3 phù hợp phân tích offline nhưng chưa có bộ nhãn chuẩn. Đây là lựa chọn cho bài lab, chưa phải kết luận về lợi ích kinh doanh thực tế. Báo cáo chi tiết: [02-deep-dive-report.md](02-deep-dive-report.md).
