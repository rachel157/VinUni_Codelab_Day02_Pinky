# 🔍 01 — Problem Scan & Quick Problem Cards

> **Đơn vị:** Vin Smart Future — AI Engineering Division  
> **Dự án:** Scoping Giải pháp AI Vận hành cho Hệ sinh thái Vingroup  
> **Chủ đề chọn Deep-Dive:** **Vinmec — AI Hỗ trợ Soạn thảo Bản Tóm tắt Hồ sơ Bệnh án Xuất viện (Discharge Summary Co-Pilot)**  

---

## 🔍 Phase 1 — SCAN: Bảng Quét 6 Bài Toán Vận Hành Tại Vingroup

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác) để rà soát các điểm nghẽn nghiệp vụ thực tế trong các công ty thành viên:

| # | Subsidiary | Lens | Mô tả ngắn bài toán vận hành & Điểm nghẽn |
|---|------------|------|------------------------------------------|
| 1 | **Vinmec** | **Tốn thời gian & Pain từ người khác** | Bác sĩ điều trị mất 25–35 phút/bệnh nhân để rà soát các kết quả cận lâm sàng, diễn biến điều trị và gõ thủ công Bản tóm tắt hồ sơ bệnh án xuất viện (Discharge Summary). Bác sĩ bị quá tải hành chính, thời gian khám thực tế cho bệnh nhân bị rút ngắn. |
| 2 | **VinFast** | **AI có thể tốt hơn** | Cố vấn dịch vụ tại Xưởng Dịch vụ VinFast mất 15–20 phút tiếp nhận và tra cứu thủ công sổ tay kỹ thuật để map ngôn ngữ đời thường của khách (*"xe kêu cụp cụp ở giảm xóc trước"*) sang mã lỗi chẩn đoán tiêu chuẩn (DTC code) và phụ tùng thay thế. |
| 3 | **Vinhomes** | **Lặp lại** | Nhân viên CSKH/Ban quản lý tòa nhà phải đọc thủ công hàng nghìn phản ánh/khiếu nại mỗi ngày trên App Vinhomes Resident (hỏng đèn, rò rỉ nước, tiếng ồn...), mất 12–24h để phân loại và chuyển tiếp thủ công đến đội kỹ thuật. |
| 4 | **Vinpearl** | **Tốn thời gian** | Đội ngũ đặt phòng phải đọc và xử lý thủ công các email đặt phòng đoàn phức tạp (Group Booking) từ các công ty lữ hành, mất 30–45 phút/đoàn để so khớp quỹ phòng trống và draft xác nhận booking. |
| 5 | **Vinmec** | **AI có thể tốt hơn** | Tổng đài CSKH Vinmec mất nhiều thời gian lắng nghe mô tả triệu chứng ban đầu của khách hàng để tư vấn đúng chuyên khoa (ví dụ: đau ngực do Tim mạch vs Tiêu hóa trào ngược), gây chậm trễ lịch hẹn khám. |
| 6 | **VinUni** | **Lặp lại** | Trợ giảng và giảng viên mất nhiều giờ chấm bài tập lập trình hàng tuần, phản hồi lỗi cú pháp/logic còn mang tính rập khuôn, chưa giải thích sâu nguyên nhân cho từng sinh viên. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ Bài Toán Tiềm Năng (Quick Problem Cards)

Từ 6 bài toán trên, tôi chọn lọc **3 bài toán tiềm năng nhất** để phân tích nhanh:

---

### 📋 QUICK PROBLEM CARD #1: Vinmec — Soạn thảo Bản Tóm tắt Xuất viện (Discharge Summary)

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                   │
│                                                                         │
│ Bài toán (1 câu): Hỗ trợ bác sĩ tự động tổng hợp dữ liệu bệnh án        │
│ điện tử (EMR) để soạn thảo bản nháp tóm tắt xuất viện cho bệnh nhân.     │
│ Công ty thành viên: [x] Vinmec                                          │
│                                                                         │
│ Ai đang đau (Actor)? Bác sĩ điều trị, Bác sĩ nội trú, Bệnh nhân chờ đợi. │
│                                                                         │
│ Workflow thủ công hiện tại (5 bước):                                    │
│   1. Mở EMR tra cứu bệnh án ──> 2. Đọc & nhặt kết quả xét nghiệm        │
│   ──> 3. Tóm tắt diễn tiến điều trị ──> 4. Gõ bản Discharge Summary    │
│   ──> 5. Ký tên & in hồ sơ bàn giao cho bệnh nhân.                      │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 20-25 phút/bệnh nhân)     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3, 4                      │
│ (Trích xuất EMR ──> Tổng hợp dữ liệu lâm sàng ──> Draft bản tóm tắt)    │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                   │
│   - Giảm thời gian soạn thảo từ 30 phút ──> dưới 5 phút/ca.             │
│   - Tỉ lệ bác sĩ đồng ý duyệt nội dung nháp đạt >= 90%.                 │
│                                                                         │
│ Quick Architecture: [x] LLM Feature (RAG trên EMR + Human-in-the-loop)   │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 📋 QUICK PROBLEM CARD #2: VinFast — Trợ lý Chẩn đoán Lỗi Kỹ thuật tại Xưởng Dịch vụ

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                   │
│                                                                         │
│ Bài toán (1 câu): Chuyển hóa mô tả triệu chứng hư hỏng bằng tiếng Việt   │
│ tự nhiên của chủ xe sang mã chẩn đoán kỹ thuật tiêu chuẩn (DTC).        │
│ Công ty thành viên: [x] VinFast                                         │
│                                                                         │
│ Ai đang đau (Actor)? Cố vấn dịch vụ xưởng và Kỹ thuật viên bảo hành.    │
│                                                                         │
│ Workflow thủ công hiện tại (4 bước):                                    │
│   1. Khách hàng mô tả lỗi ──> 2. Cố vấn tra sổ tay bảo hành thủ công   │
│   ──> 3. Đoán mã lỗi DTC sơ bộ ──> 4. Đưa xe lên cầu nâng kiểm tra.     │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 15 phút/xe)              │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3                        │
│ (Map ngôn ngữ tự nhiên ──> Mã lỗi DTC & danh sách phụ tùng gợi ý)       │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                   │
│   - Rút ngắn thời gian tiếp nhận xe ban đầu từ 20 phút ──> 5 phút.      │
│   - Độ chính xác gợi ý mã lỗi đạt >= 85%.                               │
│                                                                         │
│ Quick Architecture: [x] LLM Feature                                     │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 📋 QUICK PROBLEM CARD #3: Vinhomes — AI Triaging Phân loại Sự cố Cư dân

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                   │
│                                                                         │
│ Bài toán (1 câu): Tự động phân loại mức độ khẩn cấp (P1/P2/P3) và điều  │
│ phối ticket phản ánh trên App Vinhomes Resident đến đúng ban quản lý.   │
│ Công ty thành viên: [x] Vinhomes                                        │
│                                                                         │
│ Ai đang đau (Actor)? Đội CSKH Ban Quản lý và Cư dân bức xúc vì chờ lâu. │
│                                                                         │
│ Workflow thủ công hiện tại (4 bước):                                    │
│   1. Cư dân gửi ticket trên App ──> 2. Lễ tân đọc & gắn tag thủ công    │
│   ──> 3. Chuyển tiếp email đến đội Kỹ thuật/An ninh ──> 4. Phản hồi cư dân│
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 4-12 giờ chờ đợi)        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3                        │
│ (Phân tích ngữ nghĩa tiếng Việt ──> Auto-tag mức độ & Điều phối tự động)│
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                   │
│   - Thời gian phân loại & định tuyến ticket giảm từ 4 giờ ──> dưới 30s.  │
│   - Độ chính xác điều hướng đúng bộ phận đạt >= 95%.                    │
│                                                                         │
│ Quick Architecture: [x] LLM Feature + Rule-based Router                 │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định Lựa chọn & Phản biện (Problem Selection)

Sau khi phân tích, tôi quyết định lựa chọn **Card #1: Vinmec — AI Hỗ trợ Soạn thảo Bản Tóm tắt Hồ sơ Bệnh án Xuất viện (Discharge Summary Co-Pilot)** để thực hiện Deep-Dive.

### Lý do lựa chọn:
1. **Giá trị thực tế khổng lồ (High Clinical Value):** Bác sĩ Vinmec là nhân sự chuyên môn chất lượng cao, việc dành 2–3 giờ/ngày chỉ để sao chép dữ liệu hành chính là lãng phí nghiêm trọng nguồn lực y tế.
2. **Dữ liệu đầu vào có cấu trúc cao:** Hồ sơ Bệnh án điện tử (EMR) tại Vinmec đạt chuẩn quốc tế (JCI), đã số hóa đầy đủ các trường xét nghiệm, chẩn đoán ICD-10 và y lệnh. Đây là môi trường lý tưởng để LLM trích xuất và tổng hợp.
3. **Ranh giới an toàn (Operational Boundary) rõ nét:** Lĩnh vực y tế đòi hỏi sự kiểm soát 100% của con người (**Human-in-the-loop**). Bác sĩ điều trị luôn là người chịu trách nhiệm pháp lý cuối cùng, giúp kiểm soát hoàn toàn rủi ro sai lệch (hallucination).

### Lý do loại bỏ các thẻ còn lại:
* **Card #2 (VinFast):** Mô tả lỗi xe bằng tiếng Việt của khách hàng có tính phương ngữ cao, dữ liệu mô tả ban đầu thường thiếu thông số cảm biến OBD/CAN-bus thực tế, độ khả thi kỹ thuật chưa vững bằng dữ liệu EMR của Vinmec.
* **Card #3 (Vinhomes):** Bài toán triaging ticket cư dân phần lớn có thể giải quyết bằng mô hình phân loại Intent Classification truyền thống hoặc Rule-based kết hợp từ khóa, chưa phát huy hết thế mạnh suy luận ngôn ngữ sâu của LLM thế hệ mới.
