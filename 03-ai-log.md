# 📝 AI Log & Reflection (Cá nhân) — Lab 02: AI Product Scoping

**Học viên / Tác giả:** Nguyễn Hoàng Tùng  
**Đề tài lựa chọn:** Tự động định tuyến tránh ngập úng mùa mưa cho tài xế Xanh SM (GSM)  

---

## 1. AI đã giúp gì cho bạn?
* **Brainstorm & Mở rộng scope ý tưởng:** AI đã hỗ trợ tôi nhanh chóng quét qua bức tranh tổng quan và đề xuất từ 20 đến 30 ý tưởng bài toán vận hành khác nhau tại các khối công ty thành viên Vingroup[cite: 1, 3].
* **Thẩm định sơ bộ tính khả thi:** Sau khi chọn lọc, tôi đã đặt các câu hỏi đào sâu (deep-dive) để AI phân tích tính khả thi, đánh giá mức độ tiềm năng và sự phù hợp của công nghệ AI đối với quy trình nghiệp vụ thực tế tại Xanh SM[cite: 1].

## 2. AI đã trả lời sai hoặc gặp lỗi / Hallucination ở đâu?
* **Bịa đặt thông tin (Hallucination về thực thể):** Trong một số lượt phản hồi đầu tiên, AI đã đề xuất các giải pháp liên quan đến các phòng ban hoặc công ty thành viên không có thật trong cơ cấu thực tế của Vingroup.
* **Đề xuất giải pháp rủi ro cao:** AI gợi ý một số luồng xử lý tự động liên quan trực tiếp đến các vấn đề pháp lý và tranh chấp hợp đồng lao động/bồi thường của tài xế — đây là những mảng có rủi ro pháp lý cực kỳ cao, không phù hợp để áp dụng tự động hóa hoàn toàn bằng LLM ở giai đoạn đầu.

## 3. Bạn đã sửa prompt như thế nào để thu được kết quả chính xác?
* **Thắt chặt ngữ cảnh thực tế (Context Grounding):** Tôi đã sửa lại câu lệnh (prompt), yêu cầu mô hình giới hạn chặt chẽ phạm vi vào các công ty thành viên có thật (như Xanh SM, VinFast, Vinhomes, Vinmec) và kiểm chứng lại xem các điểm nghẽn (bottleneck) đó có thực sự diễn ra ngoài đời thực hay không[cite: 1, 3].
* **Thêm ràng buộc về ranh giới an toàn (Operational Boundaries):** Bổ sung các chỉ thị rõ ràng trong prompt để loại bỏ ngay lập tức các bài toán chạm ngưỡng nhạy cảm pháp lý hoặc đòi hỏi tự trị hoàn toàn mà không có sự kiểm soát của con người (Human-in-the-loop)[cite: 1].