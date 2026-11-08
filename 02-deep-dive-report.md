02 --- Deep Dive Report
AI hỗ trợ phân loại và định tuyến yêu cầu cư dân tại Vinhomes
Người thực hiện: \(Điền họ tên\)
Nhóm: \(Điền tên/mã nhóm\)
Đơn vị trong bối cảnh bài lab: Vinhomes --- Vin Smart Future
Trạng thái tài liệu: Đề xuất scoping ban đầu; các số liệu vận hành
là giả định cần được kiểm chứng.
1. Executive Summary
Báo cáo đề xuất xây dựng một tính năng AI hỗ trợ nhân viên chăm sóc cư
dân phân loại và định tuyến yêu cầu. Khi cư dân gửi nội dung qua ứng
dụng, hotline hoặc quầy dịch vụ, hệ thống sẽ chuẩn hóa văn bản, trích
xuất thông tin, dự đoán nhóm vấn đề và đề xuất bộ phận xử lý. Nhân viên
CSKH kiểm tra và xác nhận trước khi ticket được chuyển đi.

Phạm vi prototype không bao gồm tự động xử lý sự cố, tự cam kết thời
gian hoàn thành, tự phê duyệt chi phí/bồi thường, đánh giá lỗi của cá
nhân hay gửi thông báo cuối cùng mà không có kiểm duyệt. Mục tiêu là
giảm thời gian thao tác lặp lại và hạn chế chuyển nhầm bộ phận, không
thay thế nhân viên vận hành.

Đề xuất quyết định: NOT YET cho triển khai production; GO có điều
kiện cho prototype nội bộ. Lý do: hướng giải pháp có tính khả thi về
kỹ thuật và có thể giới hạn rủi ro, nhưng hiện chưa có dữ liệu nội bộ,
baseline và xác nhận từ stakeholder trong phạm vi bài lab.
2. Problem Statement --- 6 fields
  Field                               Phân tích
  1. Actor / Operator             Nhân viên CSKH/cư dân vụ là người
tiếp nhận và phân loại yêu cầu. Các
nhóm kỹ thuật, vệ sinh, an ninh,
cảnh quan và vận hành tiện ích là
đơn vị nhận ticket. Cư dân là người
gửi yêu cầu và theo dõi tiến độ.

  2. Current Workflow             Cư dân gửi phản ánh/yêu cầu qua ứng
dụng, hotline hoặc quầy dịch vụ.
Nhân viên đọc nội dung, xác minh
thông tin căn hộ/tòa nhà, hỏi bổ
sung nếu thiếu, xác định chủ đề và
mức độ ưu tiên, tạo ticket rồi
chuyển đến bộ phận phụ trách. Bộ
phận nhận xử lý và cập nhật trạng
thái để CSKH phản hồi cư dân. Công
cụ cụ thể cần được xác minh tại đơn
vị triển khai.

  3. Bottleneck                   Nội dung đầu vào không theo một mẫu
thống nhất; cư dân có thể dùng từ
địa phương, viết tắt, sai chính tả
hoặc gộp nhiều vấn đề. Nhân viên
phải diễn giải và tra cứu taxonomy
trước khi chọn nhóm xử lý. Nếu phân
loại sai, ticket có thể bị chuyển
vòng giữa các bộ phận.

  4. Business Impact              Tăng thời gian xử lý ban đầu, tạo
thêm thao tác cho CSKH và nhóm nhận
ticket, kéo dài thời gian phản hồi
đầu tiên và làm giảm trải nghiệm cư
dân. Chưa có số liệu nội bộ để
khẳng định mức tổn thất; cần đo số
ticket/ngày, thời gian phân loại,
tỷ lệ chuyển lại và SLA hiện tại.

  5. Success Metric               Mục tiêu thử nghiệm: giảm thời gian
phân loại/định tuyến trung vị từ
baseline giả định 6 phút xuống ≤2
phút/ticket; độ chính xác top-1
≥90% trên tập test đại diện; tỷ lệ
nhân viên sửa nhãn ≤10%; 100%
trường hợp confidence thấp, thiếu
dữ liệu hoặc có dấu hiệu khẩn cấp
được chuyển người kiểm tra. Các
ngưỡng này là mục tiêu đề xuất, cần
hiệu chỉnh sau khi có baseline.
6. Operational Boundary         AI chỉ được phân loại, trích xuất
trường thông tin, phát hiện dữ liệu
thiếu và gợi ý nhóm xử lý/mức ưu
tiên. AI không được tự đóng ticket,
tự kết luận trách nhiệm, tự phê
duyệt bồi thường/chi phí, tự đưa ra
cam kết SLA, tự chẩn đoán nguy cơ
kỹ thuật hoặc thay thế quy trình
khẩn cấp. Nhân viên phải duyệt
trước khi lưu/chuyển ticket.
2.1. Phạm vi vấn đề (Scope)
In-scope: - Tiếp nhận văn bản mô tả yêu cầu đã được hệ thống chuyển
thành dữ liệu. - Chuẩn hóa lỗi gõ/viết tắt ở mức không làm thay đổi ý
nghĩa. - Phân loại theo taxonomy được Vinhomes phê duyệt. - Trích xuất
thông tin có trong nội dung: tòa nhà, căn hộ, vị trí, thời gian, mô tả
sự cố. - Đánh dấu trường còn thiếu và đề xuất câu hỏi làm rõ. - Đề xuất
nhóm phụ trách và mức ưu tiên để nhân viên xem xét.

Out-of-scope: - Tự động điều phối nhân sự hoặc điều khiển thiết
bị. - Tự đưa ra kết luận kỹ thuật, pháp lý hoặc an toàn. - Tự quyết định
bồi thường, hoàn phí, phạt hoặc quy trách nhiệm. - Tự đóng ticket hoặc
tự cam kết thời hạn xử lý. - Xử lý sự cố khẩn cấp thay cho hotline/quy
trình khẩn cấp hiện có.
3. Current-State Workflow Mapping
3.1. Quy trình hiện tại (giả thuyết cần xác minh)
  Bước          Người/hệ      Hoạt động         Thời gian giả Handoff / Rủi
thống thực                               định ro
hiện                                          
  1             Cư dân        Gửi yêu cầu      Không tính vào Handoff sang
qua app,        thời gian xử lý CSKH; nội dung
hotline hoặc             nội bộ có thể thiếu
quầy dịch vụ                    thông tin.

  2             Nhân viên     Đọc nội dung,            2 phút Có thể phải
CSKH          xác định vấn                    đọc lại hoặc
đề chính và                     liên hệ cư
kiểm tra                        dân.
thông tin cư
dân                             

  3             Nhân viên     Hỏi bổ sung   1 phút trung bình Thời gian có
CSKH          và chuẩn hóa                    thể tăng đáng
nội dung nếu                    kể nếu phải
thiếu                           chờ cư dân.

  4             Nhân viên     Chọn nhóm vấn            2 phút Bottleneck
CSKH          đề, mức ưu                      chính: phụ
tiên và bộ                      thuộc kinh
phận phụ                        nghiệm và cách
trách                           diễn đạt của
cư dân.

  5             Nhân viên     Tạo ticket,              1 phút Handoff sang
CSKH / hệ     nhập thông                      bộ phận vận
thống ticket  tin và chuyển                   hành.
bộ phận                         
6             Bộ phận phụ   Tiếp nhận,     Ngoài phạm vi đo Nếu sai nhóm,
trách         xác minh và      ở bài toán này ticket phải
xử lý yêu cầu                   chuyển lại.
Tổng thời gian thao tác nội bộ ước tính: khoảng 6 phút/ticket, chưa
tính thời gian chờ cư dân cung cấp thông tin và thời gian xử lý sự cố.
3.2. Sơ đồ Current-State
flowchart TD
    A[Cư dân gửi yêu cầu] --> B[CSKH tiếp nhận]
    B --> C[Đọc và kiểm tra thông tin]
    C --> D{Thông tin đầy đủ?}
    D -- Không --> E[Liên hệ cư dân hỏi bổ sung]
    E --> C
    D -- Có --> F[Phân loại vấn đề và mức ưu tiên]
    F --> G[Chọn bộ phận phụ trách]
    G --> H[Tạo ticket và chuyển giao]
    H --> I[Bộ phận vận hành tiếp nhận]
    I --> J[Xử lý và cập nhật trạng thái]
    J --> K[CSKH phản hồi cư dân]

    classDef bottleneck fill:#ffe0e0,stroke:#d33,stroke-width:2px;
    class F,G bottleneck;
3.3. Điểm nghẽn và dữ liệu cần đo
- Bottleneck 1 --- hiểu nội dung: văn bản không theo biểu mẫu,
  chứa nhiều vấn đề hoặc thiếu vị trí cụ thể.
- Bottleneck 2 --- phân loại/định tuyến: nhân viên phải nhớ
  taxonomy và danh sách bộ phận chịu trách nhiệm.
- Bottleneck 3 --- chuyển ticket sai: ticket bị trả lại hoặc
  chuyển tiếp làm phát sinh handoff bổ sung.
Để xác nhận giả thuyết, cần thu thập tối thiểu: 1. Thời điểm ticket được
tạo, bắt đầu phân loại, chuyển bộ phận và bị chuyển lại. 2. Nhãn phân
loại cuối cùng đã được nhân viên xác nhận. 3. Nội dung ticket đã ẩn danh
và metadata tối thiểu cần thiết. 4. Số lần yêu cầu bổ sung thông tin. 5.
Tỷ lệ ticket quá SLA và nguyên nhân.
4. Future-State Workflow & AI Fit
4.1. So sánh Rule-based, LLM và Agentic Loop
  Tiêu chí          Rule / State      LLM Feature       Agentic Loop
Machine                             
  Xử lý từ khóa cố  Rất phù hợp       Có thể làm nhưng  Không cần thiết
định, mã tòa/căn                    không cần thiết
hộ, trường bắt
buộc                                                  

  Hiểu mô tả tự do, Hạn chế           Phù hợp           Có thể phù hợp
sai chính tả,                                         nhưng phức tạp
nhiều cách diễn                                       hơn
đạt                                                   

  Trích xuất thông  Khó mở rộng bằng  Phù hợp           Có thể thực hiện
tin và phân loại  luật thủ công                       qua nhiều bước
ngữ nghĩa                                             

  Kiểm soát đầu ra  Dễ kiểm soát      Cần schema,       Khó kiểm soát hơn
validation và     do nhiều hành
HITL              động

  Chi phí và độ     Thấp              Trung bình        Cao
phức tạp triển
khai                                                  
Rủi ro tự ý thực  Thấp nếu không    Thấp hơn khi chỉ  Cao hơn nếu được
hiện hành động    cấp quyền         trả JSON          cấp công cụ/hành
động
Lựa chọn: LLM Feature kết hợp Rule-based validation. Không chọn
Agentic Loop cho phiên bản đầu vì nhiệm vụ có đầu vào/đầu ra tương đối
rõ, không cần AI tự lập kế hoạch và gọi nhiều công cụ.
4.2. Vai trò cụ thể của từng thành phần
- Rule-based: kiểm tra trường bắt buộc, định dạng mã căn hộ/tòa
  nhà, danh sách nhãn hợp lệ, ánh xạ nhãn sang bộ phận và quy tắc ưu
  tiên đã được phê duyệt.
- LLM: hiểu ngôn ngữ tự nhiên; tóm tắt vấn đề; trích xuất thông
  tin; đề xuất nhãn và câu hỏi làm rõ.
- Backend workflow: kiểm tra JSON, lưu kết quả nháp, ghi log phiên
  bản model/prompt và chuyển cho nhân viên duyệt.
- Human-in-the-loop: nhân viên xác nhận hoặc sửa kết quả trước khi
  ticket được chuyển.
4.3. Future-State Flow
flowchart TD
    A[Cư dân gửi yêu cầu] --> B[Hệ thống tiếp nhận và ẩn danh dữ liệu cần thiết]
    B --> C[Rule kiểm tra trường bắt buộc]
    C --> D[LLM phân tích nội dung]
    D --> E[JSON: tóm tắt, nhãn, trường trích xuất, confidence, câu hỏi]
    E --> F[Rule validation: schema, taxonomy, trường bắt buộc]
    F --> G{Kết quả hợp lệ và đủ tin cậy?}
    G -- Không --> H[Fallback: đưa về hàng đợi CSKH xử lý thủ công]
    G -- Có --> I[Nhân viên CSKH review]
    I --> J{Nhân viên xác nhận?}
    J -- Không --> K[Nhân viên sửa nhãn/thông tin]
    K --> L[Ghi nhận feedback và tạo ticket]
    J -- Có --> L
    L --> M[Chuyển ticket đến bộ phận phụ trách]
    M --> N[Theo dõi trạng thái theo quy trình hiện có]
4.4. Human-in-the-loop (HITL)
Nhân viên CSKH là người ra quyết định cuối cùng ở khâu phân loại và
chuyển ticket.

Bắt buộc review khi: - Confidence thấp hơn ngưỡng thử nghiệm (đề
xuất ban đầu: 0,80). - Nội dung có nhiều vấn đề hoặc nhiều nhãn cạnh
tranh. - Thiếu mã căn hộ/tòa nhà/vị trí cần thiết. - Nội dung liên quan
đến an ninh, an toàn, sức khỏe, cháy nổ, thang máy hoặc tình huống khẩn
cấp. - AI đề xuất nhãn không tồn tại trong taxonomy. - Nội dung có thể
chứa thông tin cá nhân nhạy cảm hoặc yêu cầu xử lý đặc biệt.

Nguyên tắc: Confidence do mô hình tự báo cáo không được xem là xác
suất đúng đã hiệu chuẩn. Ngưỡng 0,80 chỉ là ngưỡng khởi đầu; cần hiệu
chuẩn trên tập validation và kiểm tra theo từng nhóm vấn đề.
4.5. Fallback và xử lý lỗi
  Tình huống                          Cách xử lý
  API LLM timeout / mất kết nối       Không chặn quy trình tiếp nhận; đưa
ticket vào hàng đợi thủ công.

  JSON sai schema hoặc thiếu trường   Backend từ chối kết quả, thử
sửa/parse có giới hạn; nếu vẫn lỗi
thì fallback.

  Nhãn ngoài taxonomy                 Không tự tạo nhãn mới; chuyển nhân
viên chọn nhãn hợp lệ.

  Nội dung không rõ hoặc confidence   Gợi ý câu hỏi bổ sung hoặc chuyển
thấp                                nhân viên review.

  Nội dung khẩn cấp                   Kích hoạt quy trình khẩn cấp hiện
có; không chờ LLM phân loại.
Model trả lời ngoài phạm vi / đưa   Loại bỏ nội dung đó, không đưa vào
ra kết luận không có căn cứ         ticket như kết luận; ghi log để
đánh giá.
5. Operational Boundary & Safety
5.1. AI được phép
1. Tóm tắt nội dung cư dân gửi.
2. Gợi ý một nhãn chính và tối đa hai nhãn phụ từ danh sách được cung
   cấp.
3. Trích xuất trường có căn cứ trực tiếp trong nội dung.
4. Nêu rõ trường còn thiếu hoặc thông tin mâu thuẫn.
5. Đề xuất nhóm xử lý dựa trên bảng ánh xạ đã được đơn vị vận hành phê
   duyệt.
5.2. AI tuyệt đối không được
1. Tự khẳng định nguyên nhân kỹ thuật khi chưa có kiểm tra hiện trường.
2. Tự kết luận cá nhân/bộ phận nào có lỗi.
3. Tự hứa hẹn thời gian hoàn thành hoặc bồi thường.
4. Tự đóng ticket, tự thay đổi trạng thái hoặc gửi thông báo cuối cùng.
5. Bỏ qua quy trình khẩn cấp hoặc tự xử lý yêu cầu liên quan đến an
   toàn.
5.3. Quy tắc dữ liệu
- Chỉ sử dụng dữ liệu cần thiết cho mục đích phân loại.
- Ẩn danh tên, số điện thoại và thông tin nhận dạng không cần thiết
  trước khi gửi tới mô hình, nếu kiến trúc và chính sách cho phép.
- Không dùng dữ liệu cư dân để huấn luyện hoặc mục đích khác nếu chưa
  có phê duyệt hợp lệ.
- Phân quyền truy cập, mã hóa khi truyền/lưu và quy định thời hạn lưu
  log.
- Log cần ghi phiên bản prompt/model, đầu vào đã xử lý, đầu ra, kết
  quả validation và thao tác sửa của nhân viên; hạn chế lưu dữ liệu
  định danh.
6. Metrics & Experiment Design
6.1. KPI đề xuất
  Metric              Baseline ban đầu   Mục tiêu prototype Cách đo
  Thời gian phân            Giả định 6       ≤2 phút/ticket So sánh
loại và định             phút/ticket                      timestamp
tuyến trung vị                                            trước/sau trên
cùng loại
ticket.

  Độ chính xác                 Chưa có                 ≥90% So sánh với
nhãn top-1                                                nhãn chuẩn do
người gán độc
lập.

  Tỷ lệ nhân viên              Chưa có                 ≤10% Số kết quả bị
sửa nhãn                                                  sửa / tổng kết
quả AI đề xuất.

  Tỷ lệ ticket         Cần đo baseline  Giảm ít nhất 30% so Đếm ticket bị
chuyển sai nhóm                              với baseline trả lại/chuyển
lại do sai định
tuyến.

  Tỷ lệ xử lý                  Chưa có  Theo dõi, không đặt Số ticket
fallback                               mục tiêu giảm bằng fallback / tổng
mọi giá ticket AI xử
lý.
Sự cố nghiêm     0 hành động tự động                    0 Kiểm thử quyền
trọng do AI tự             được phép                      và audit log.
hành động
6.2. Thiết kế thử nghiệm
Giai đoạn 1 --- Offline evaluation - Lấy mẫu ticket đã được xử lý,
loại bỏ hoặc ẩn danh dữ liệu định danh. - Nhờ nhân viên có chuyên môn
gán nhãn chuẩn theo taxonomy thống nhất. - Chia dữ liệu train/dev/test
hoặc few-shot/reference theo thời gian, tránh để các ticket gần trùng
lặp xuất hiện ở cả tập tham chiếu và test. - Đánh giá precision, recall,
macro-F1 theo từng nhóm; xem confusion matrix để phát hiện nhóm dễ
nhầm. - Kiểm thử riêng các tình huống khẩn cấp, thiếu dữ liệu, nhiều vấn
đề và prompt injection.

Giai đoạn 2 --- Shadow mode - AI đưa ra gợi ý nhưng không tác động
đến ticket thật. - Nhân viên vẫn làm quy trình hiện tại; so sánh gợi ý
AI với kết quả nhân viên. - Ghi nhận thời gian, độ chính xác, tỷ lệ
fallback và loại lỗi.

Giai đoạn 3 --- Assisted pilot - Chỉ triển khai cho một nhóm yêu cầu
phổ biến, rủi ro thấp. - AI hiển thị kết quả nháp; nhân viên bắt buộc
xác nhận. - Có nút sửa/không sử dụng kết quả AI và cơ chế quay về xử lý
thủ công. - Chỉ mở rộng khi đạt ngưỡng chất lượng và được stakeholder
phê duyệt.
7. AI Readiness Checklist --- Phase 5
  #                Câu hỏi đánh giá  Trạng thái hiện   Bằng chứng / Việc
tại               cần làm
  1                 Có dữ liệu        Chưa xác minh Cần xin mẫu
mẫu/logs sạch để                    ticket đã ẩn
test không?                         danh, taxonomy và
nhãn chuẩn từ đơn
vị vận hành.

  2                 Rủi ro khi AI sai Có thể kiểm     AI chỉ đề xuất;
có kiểm soát được soát trong scope  có validation,
không?            đề xuất         HITL, fallback và
không có quyền tự
đóng/chuyển
ticket. Cần kiểm
thử thực tế.
3                 Stakeholders sẵn  Chưa xác minh Cần phỏng vấn
sàng thay đổi quy                   CSKH, bộ phận vận
trình không?                        hành và quản lý
hệ thống; đánh
giá mức chấp nhận
gợi ý AI.
7.1. Quyết định cuối cùng
<badge color="warning">{=html}NOT YET --- Production`</badge>`{=html}

GO có điều kiện cho prototype nội bộ; NOT YET cho triển khai
production.

Justification:
- Về kỹ thuật, bài toán phù hợp với LLM ở khâu hiểu văn bản tự do,
  trích xuất thông tin và phân loại. Các bước kiểm tra trường bắt
  buộc, taxonomy và ánh xạ bộ phận nên dùng rule-based để tăng tính ổn
  định.
- Về vận hành, giải pháp có thể được thiết kế theo hướng
  human-in-the-loop, không trao quyền tự thực hiện hành động cho mô
  hình. Khi AI không chắc chắn, hệ thống quay về quy trình thủ công.
- Tuy nhiên, hiện chưa có dữ liệu ticket nội bộ, nhãn chuẩn, baseline
  thời gian và xác nhận của stakeholder. Vì vậy chưa đủ bằng chứng để
  cam kết mục tiêu tiết kiệm thời gian hoặc độ chính xác trong môi
  trường thực tế.
- Trước khi quyết định GO production, cần hoàn thành offline
  evaluation, shadow mode, kiểm thử bảo mật/riêng tư và pilot có giám
  sát.
Điều kiện để chuyển từ NOT YET sang GO: 1. Có tập dữ liệu ticket
được phép sử dụng, đã ẩn danh và có nhãn chuẩn. 2. Có taxonomy và bảng
ánh xạ bộ phận được chủ quy trình phê duyệt. 3. Đạt các ngưỡng chất
lượng đề xuất trên tập test đại diện, không có lỗi nghiêm trọng ở nhóm
khẩn cấp. 4. Stakeholder đồng ý quy trình nhân viên duyệt và có phương
án rollback. 5. Có cơ chế giám sát, audit log và người chịu trách nhiệm
khi AI gợi ý sai.
8. Kết luận
AI nên đóng vai trò trợ lý phân loại, không phải người ra quyết định
vận hành. Kiến trúc LLM kết hợp rule-based validation phù hợp hơn
Agentic Loop ở giai đoạn đầu vì dễ kiểm soát, dễ đo lường và giảm rủi
ro. Hướng đi hợp lý là thử nghiệm offline, chạy shadow mode, sau đó mới
pilot có nhân viên phê duyệt. Quyết định NOT YET cho production phản ánh
đúng việc thiếu dữ liệu và bằng chứng triển khai, thay vì đánh đồng một
ý tưởng có tiềm năng với một sản phẩm đã sẵn sàng.