### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|---------------------------------|------|---------------------|
| 1 | GSM | AI có thể tốt hơn | Phân loại tự động đánh giá 1-5 sao: Tổng hợp hàng nghìn đánh giá trên ứng dụng Xanh SM để phân tách nguyên nhân gốc rễ (thái độ tài xế, mùi xe, điều hòa, giá cước) giúp cải thiện chất lượng dịch vụ từng vùng, từng quốc gia có văn hóa riêng. |
| 2 | GSM | Lặp lại | Tối ưu hóa ghép đơn đa phương thức (Multi-modal Matching): AI tự động phân tích và ghép cuốc giao đồ ăn/hàng hóa nhẹ (Xanh Express) cùng tuyến đường với cuốc chở khách của tài xế xe máy điện để tăng doanh thu. |
| 3 | GSM | Pain từ người khác | Định tuyến tránh ngập úng mùa mưa tại Hà Nội/TP.HCM: Tích hợp dữ liệu cảnh báo ngập tự động để tính toán lại lộ trình cho tài xế Xanh SM, tránh các tuyến đường ngập sâu có nguy cơ hỏng động cơ xe điện. |
| 4 | GSM | Tốn thời gian | Dự báo điểm nóng nhu cầu thời gian thực: Phân tích dữ liệu thời tiết, giao thông và sự kiện để dự báo trước 30 phút các khu vực có khách gọi xe đột biến, tự động gợi ý tài xế di chuyển đón đầu. |
| 5 | GSM | Tốn thời gian | Trợ lý ảo giải đáp chính sách thưởng/phạt cho tài xế 24/7: Chatbot nội bộ giúp tài xế tra cứu nhanh quy định thưởng doanh thu, chiết khấu ca trực, bảo hiểm mà không cần gọi tổng đài. |



**3 Quick Problem Cards**
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Phân loại tự động đánh giá 1-5 sao của khách │
│ hàng trên ứng dụng để tìm ra nguyên nhân gốc rễ theo vùng.  │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Đội ngũ Vận hành & CSKH khu vực        │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Khách gửi đánh giá/feedback trên App                   │
│   ──> 2. Nhân viên CSKH xuất dữ liệu ra file Excel hằng tuần│
│   ──> 3. Đọc thủ công từng phản hồi để gom nhóm lỗi         │
│   ──> 4. Lập báo cáo tổng hợp gửi cho Quản lý các vùng      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 300 phút/tuần)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Tự động NLP text      │
│ classification gom nhóm nguyên nhân (thái độ, mùi, giá...)   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   VD: "Giảm thời gian xử lý báo cáo tuần từ 5 tiếng ──> 15 phút"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tối ưu hóa ghép đơn giao hàng nhẹ (Xanh   │
│ Express) chung tuyến đường với cuốc chở khách xe máy điện.  │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế xe máy điện Xanh SM             │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tài xế nhận cuốc chở khách                             │
│   ──> 2. Hoàn thành chuyến chở khách                        │
│   ──> 3. Bật ứng dụng tìm đơn giao hàng thủ công            │
│   ──> 4. Nhận đơn hàng mới đôi khi ngược đường về           │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ 10 phút/lượt)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Auto-matching đơn hàng │
│ ngay trước khi kết thúc chuyến chở khách hiện tại           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   VD: "Tăng doanh thu trung bình mỗi ca trực của tài xế 20%"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Tự động định tuyến tránh ngập úng mùa mưa   │
│ cho tài xế Xanh SM để bảo vệ động cơ xe điện.               │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM & Đội cứu hộ kỹ thuật   │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Mưa lớn xảy ra tại các tuyến phố                       │
│   ──> 2. Tài xế tự cập nhật thông tin qua mạng xã hội/tin đồn │
│   ──> 3. Dò dẫm lái xe vào điểm ngập sâu gây hỏng xe         │
│   ──> 4. Gọi tổng đài báo cứu hộ xe ngập nước               │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 20 phút/sự cố)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Tích hợp dữ liệu cảnh │
│ báo ngập tự động để route lại đường đi ngay lập tức         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   VD: "Giảm 90% số lượng xe điện chết máy do ngập nước"     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```