# 📄 02 — Problem Deep-Dive Report: Vinmec Discharge Summary Co-Pilot

> **Đơn vị công tác:** Vin Smart Future (Vingroup)  
> **Khối nghiệp vụ:** Khối Y Tế Thông Minh — Bệnh viện Đa khoa Quốc tế Vinmec  
> **Dự án:** **AI Hỗ trợ Soạn thảo Bản Tóm tắt Hồ sơ Bệnh án Xuất viện (Discharge Summary Co-Pilot)**  

### 👥 Thông tin nhóm

**Tên nhóm:** Pinky

| # | MSSV | Họ và tên | Vai trò |
|---|------|-----------|---------|
| 1 | 2A202603370 | Phạm Việt Hưng | Nhóm trưởng |
| 2 | 2A202603377 | Chu Mai Hồng | Thành viên |
| 3 | 2A202603481 | Nguyễn Hoàng Tùng | Thành viên |
| 4 | 2A202603436 | Phạm Nguyên Vũ | Thành viên |

---

# 🏗️ Phase 3 — DEEP-DIVE: Phân Tích Chuyên Sâu Bài Toán

## 3.1. Sơ Đồ Quy Trình Vận Hành Hiện Tại (Current-State Workflow)

Quy trình xuất viện của bệnh nhân nội trú hiện tại tại Bệnh viện Đa khoa Quốc tế Vinmec bao gồm 5 bước tuần tự hoàn toàn thủ công:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Bác sĩ quyết │     │ Mở EMR, rà   │     │ Tổng hợp     │     │ Gõ thủ công  │
│ định cho     │ ──→ │ soát toàn bộ │ ──→ │ diễn tiến    │ ──→ │ văn bản Bản  │
│ xuất viện    │     │ xét nghiệm   │     │ điều trị     │     │ Tóm Tắt      │
│ Ai: Bác sĩ   │     │ Ai: Bác sĩ   │     │ Ai: Bác sĩ   │     │ Ai: Bác sĩ   │
│ ⏱ 2 phút     │     │ ⏱ 10 phút 🔴 │     │ ⏱ 8 phút     │     │ ⏱ 10 phút 🔴 │
│ In: Tình trạng│    │ In: EMR, PACS│     │ In: Note hằng│     │ In: Dữ liệu  │
│ Out: Y lệnh  │     │ Out: Số liệu │     │ ngày         │     │ Out: Văn bản │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                       │
                                                                       ▼
                                                                ┌──────────────┐
                                                                │ Bước 5       │
                                                                │ In, ký tên   │
                                                                │ & bàn giao   │
                                                                │ Ai: Bác sĩ,  │
                                                                │ Điều dưỡng 🔄│
                                                                │ ⏱ 3 phút     │
                                                                └──────────────┘

🔴 = Bottlenecks (Bước 2 & Bước 4 chiếm tới 20 phút)
🔄 = Handoff (Chuyển giao giữa Bác sĩ điều trị và Điều dưỡng/Quầy viện phí)
⏱ Tổng thời gian xử lý thủ công: ~33 phút / bệnh nhân.
```

* **Điểm nghẽn cổ chai (🔴 Bottlenecks):**
  * **Bước 2 (10 phút):** Tra cứu thủ công các kết quả cận lâm sàng nằm rải rác ở các phân hệ khác nhau: phân hệ Xét nghiệm (LIS), Chẩn đoán hình ảnh (PACS/X-quang, CT, MRI) và Ghi chú điều dưỡng.
  * **Bước 4 (10 phút):** Tự gõ văn bản tóm tắt quá trình điều trị, đối chiếu mã chẩn đoán ICD-10 và hướng dẫn dặn dò dùng thuốc ra viện bằng tiếng Việt chuẩn y khoa.
* **Điểm chuyển giao (🔄 Handoffs):** Bác sĩ ký xong bàn giao bản cứng cho Điều dưỡng hành chính và Quầy viện phí để làm thủ tục thanh toán bảo hiểm và trả giường.

---

## 3.2. Problem Statement (6-Field) — Chuẩn Vin Smart Future

| Trường Thông Tin (Field) | Nội Dung Chi Tiết Nghiệp Vụ Tại Vinmec |
| :--- | :--- |
| **1. Actor / Operator** | Bác sĩ điều trị và Bác sĩ nội trú tại các khoa lâm sàng (Khoa Nội tổng quát, Khoa Ngoại, Khoa Tim mạch) thuộc Bệnh viện Đa khoa Quốc tế Vinmec. |
| **2. Current Workflow** | Khi bệnh nhân đủ điều kiện ra viện, bác sĩ mở hệ thống Bệnh án điện tử (EMR), lần lượt đọc các ghi chú lâm sàng từ ngày nhập viện, truy xuất các kết quả xét nghiệm máu, vi sinh, chẩn đoán hình ảnh, tổng hợp thuốc đã sử dụng, sau đó gõ thủ công từng mục vào biểu mẫu Bản Tóm Tắt Xuất Viện. Quy trình gồm 5 bước thủ công, mất trung bình 33 phút/bệnh nhân. |
| **3. Bottleneck** | Bước 2 và Bước 4 (chiếm 20/33 phút): Bác sĩ mất quá nhiều thời gian đọc lướt hàng chục trang báo cáo cận lâm sàng để nhặt số liệu bất thường, sau đó soạn thảo văn bản tóm tắt diễn tiến bệnh. Đây là tác vụ văn phòng thuần túy, lặp đi lặp lại và dễ gây sai sót do mệt mỏi. |
| **4. Business Impact** | Mỗi cơ sở bệnh viện Vinmec tiếp nhận khoảng 40–60 ca xuất viện mỗi ngày. Với 33 phút/ca, toàn bộ đội ngũ bác sĩ mất tổng cộng 22–33 giờ công lao động/ngày chỉ để làm giấy tờ. Hậu quả: chậm trễ giờ trả phòng/giường bệnh (làm giảm 12% công suất quay vòng giường nội trú), gia tăng thời gian chờ thanh toán của bệnh nhân, và làm tăng nguy cơ kiệt sức (burnout) của bác sĩ. |
| **5. Success Metric** | **1. Hiệu suất (Efficiency):** Giảm thời gian soạn thảo bản tóm tắt xuất viện từ 33 phút xuống **dưới 5 phút/ca** (tiết kiệm > 80% thời gian hành chính).<br>**2. Chất lượng & Chấp nhận (Adoption):** Tỉ lệ bác sĩ đồng ý ký duyệt nội dung do AI soạn thảo nháp đạt **>= 92%**.<br>**3. Độ an toàn (Safety):** **0% sai lệch dữ liệu lâm sàng** (Zero Hallucination đối với chỉ số xét nghiệm và đơn thuốc ra viện). |
| **6. Operational Boundary (Ranh giới vận hành an toàn)** | **ĐƯỢC PHÉP:** AI được phép truy xuất dữ liệu có sẵn trong EMR của bệnh nhân đó, tổng hợp dữ liệu xét nghiệm vào/ra viện, soạn thảo văn bản nháp mang thẻ định danh `[DRAFT_CLINICAL_SUMMARY]`.<br>🛑 **TUYỆT ĐỐI CẤM:**<br>1. AI không được tự ý suy đoán hoặc thêm chẩn đoán bệnh mới chưa có trong EMR.<br>2. AI không được tự ý thay đổi tên thuốc, liều dùng, hoặc hướng dẫn điều trị ra viện.<br>3. AI tuyệt đối **KHÔNG được tự động ký duyệt hoặc phát hành hồ sơ** ra cổng thông tin/app bệnh nhân mà không có chữ ký số của Bác sĩ điều trị (Bắt buộc 100% Human-in-the-loop).<br>4. Nếu phát hiện dữ liệu xét nghiệm bị thiếu hoặc mâu thuẫn, AI phải gắn nhãn cảnh báo `[WARNING_MISSING_DATA]` và chuyển trả cho bác sĩ nhập tay. |

---

## 3.3. Future-State Flow & AI Fit

### Lựa chọn Công nghệ AI (AI-Fit Matrix):
* **Lựa chọn:** **LLM Feature kết hợp RAG (Retrieval-Augmented Generation) & Prompt Safety Boundaries**.
* **Lý do không dùng Rule-based thuần:** Hồ sơ bệnh án chứa rất nhiều ghi chú dạng văn bản tự do không cấu trúc (Unstructured Clinical Notes) của các chuyên khoa khác nhau, rule-based không thể tóm tắt văn phong mạch lạc và súc tích.
* **Lý do không dùng Autonomous Agent (Multi-Agent tự trị):** Trong môi trường Y tế, mọi quyết định đều liên quan đến tính mạng và trách nhiệm pháp lý. Việc trao quyền tự trị (Autonomous loop) cho Agent tự ra quyết định hoặc tự gửi hồ sơ là vi phạm nghiêm trọng tiêu chuẩn an toàn y tế quốc tế (JCI) và pháp luật Việt Nam. Do đó, mô hình LLM Feature đóng vai trò "Trợ lý thư ký lâm sàng (Clinical Scribe Copilot)" có Human-in-the-loop là tối ưu nhất.

### Sơ Đồ Quy Trình Tương Lai (Future-State Flow):

```text
┌────────────────┐     ┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│ Bước 1         │     │ Bước 2         │     │ Bước 3         │     │ Bước 4         │
│ Bác sĩ click   │     │ 🔵 AI RAG      │     │ 🔵 LLM tạo     │     │ 🟢 Bác sĩ      │
│ "Tạo bản tóm   │ ──→ │ tự động trích  │ ──→ │ bản nháp mang  │ ──→ │ kiểm duyệt,    │
│ tắt xuất viện" │     │ xuất dữ liệu   │     │ nhãn [DRAFT]   │     │ chỉnh sửa (nếu │
│ Ai: Bác sĩ     │     │ từ EMR / PACS  │     │ kèm trích dẫn  │     │ cần) & ký số   │
│ ⏱ 30 giây      │     │ ⏱ 10 giây      │     │ ⏱ 15 giây      │     │ ⏱ 3-4 phút     │
└────────────────┘     └────────────────┘     └────────────────┘     └────────────────┘
                                                                              │
                                                       ┌──────────────────────┴──────────────────────┐
                                                       ▼                                             ▼
                                                🟢 HỢP LỆ:                                    ↩️ FALLBACK:
                                                Bác sĩ ký số ──> Bàn giao                     Nếu AI cảnh báo thiếu số liệu
                                                cho Quầy viện phí & App cư dân.               hoặc draft không chuẩn, Bác sĩ
                                                (Tổng thời gian: < 5 phút!)                   chuyển sang gõ tay như cũ.
```

---

# 🏁 Phase 5 — EVALUATE: Đánh Giá Tính Sẵn Sàng & Quyết Định

### 1. Bảng Đánh Giá Mức Độ Sẵn Sàng (AI Readiness Checklist):

| Tiêu Chí Đánh Giá | Hiện Trạng Tại Vinmec | Đánh Giá |
| :--- | :--- | :---: |
| **1. Sẵn sàng về dữ liệu (Data Readiness)** | Hệ thống EMR Vinmec đã chuẩn hóa mã ICD-10, kết quả xét nghiệm đạt chuẩn kết nối HL7/FHIR, dữ liệu bệnh án đã lưu trữ số hóa tập trung. | ✅ **ĐẠT** |
| **2. Kiểm soát rủi ro & An toàn (Risk Control)** | Thiết lập ranh giới vận hành nghiêm ngặt: AI chỉ sinh bản nháp `[DRAFT_CLINICAL_SUMMARY]`, bác sĩ chịu trách nhiệm pháp lý và ký số 100% trước khi phát hành. Có cơ chế Fallback gõ tay. | ✅ **ĐẠT** |
| **3. Mức độ sẵn sàng của Stakeholders** | Đội ngũ bác sĩ Vinmec đang chịu áp lực lớn về thủ tục hành chính, rất hào hứng với công cụ tự động hóa giúp giải phóng thời gian khám chữa bệnh. Ban Giám Đốc bệnh viện ủng hộ chiến lược Y tế Thông minh. | ✅ **ĐẠT** |

---

### 2. Quyết Định Cuối Cùng của Ban Giám Đốc Vin Smart Future:

# ✅ **QUYẾT ĐỊNH: GO (Bắt đầu triển khai Bản thử nghiệm Prototype)**

### 3. Lý giải quyết định (Justification):
1. **Giá trị kinh tế và vận hành vượt trội (High ROI):** Tiết kiệm ~28 phút/ca xuất viện. Với quy mô 50 ca/ngày tại một cơ sở bệnh viện, giải pháp tiết kiệm được hơn 20 giờ làm việc chuyên môn của bác sĩ mỗi ngày, đồng thời tăng 12% hiệu suất sử dụng giường bệnh nội trú, mang lại doanh thu gia tăng ước tính hàng tỷ đồng mỗi năm cho Vinmec.
2. **Khả thi cao về mặt kỹ thuật:** Không cần đào tạo mô hình nền tảng mới từ đầu. Chỉ cần ứng dụng Gemini 2.5 Flash kết hợp kỹ thuật RAG trên kho dữ liệu EMR sẵn có, chi phí API trên mỗi lượt gọi cực kỳ rẻ (~0.005 USD/bệnh nhân).
3. **Phạm vi triển khai giai đoạn 1 (Narrow Scope Pilot):**
   * Triển khai thử nghiệm ban đầu tại **Khoa Nội tổng quát — Bệnh viện Đa khoa Quốc tế Vinmec Times City**.
   * Chỉ áp dụng cho các ca xuất viện thông thường (không áp dụng ngay cho các ca phẫu thuật phức tạp hoặc ca chuyển viện cấp cứu).
   * Đánh giá hiệu quả sau 30 ngày thử nghiệm trước khi mở rộng toàn hệ thống Vinmec toàn quốc.
