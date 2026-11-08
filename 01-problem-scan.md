01 --- Problem Scan & Quick Assess
Lab 02: AI Product Scoping --- Vin Smart Future
Người thực hiện: \(Điền họ tên\)
Nhóm: \(Điền tên/ mã nhóm\)
Phạm vi: Phân tích cơ hội ứng dụng AI trong các công ty thành viên
được nêu trong worksheet.
Lưu ý về dữ liệu: Các thời lượng, tỷ lệ và ngưỡng mục tiêu trong tài
liệu này là giả định ban đầu phục vụ scoping, không phải số liệu nội
bộ đã được Vingroup/Vinhomes công bố. Cần đo baseline bằng log vận hành
và phỏng vấn nhân sự trước khi triển khai thật.
Phase 1 --- SCAN
1.1. Cách tiếp cận
Sử dụng 4 lenses trong worksheet để tìm các công việc có khả năng tạo ra
điểm nghẽn:
- Repetitive: phát sinh thường xuyên, có nhiều thao tác lặp.
- Time-consuming: mất thời gian tra cứu, tổng hợp, nhập liệu hoặc
  chuyển giao.
- AI-upgrade: cần hiểu ngôn ngữ tự nhiên, phân loại nội dung hoặc
  tạo phản hồi phù hợp ngữ cảnh.
- Stakeholder Pain: gây khó chịu cho khách hàng hoặc tăng tải cho
  nhân viên vận hành.
1.2. Danh sách cơ hội
  #             Công ty        Lens chính        Bài toán /     Cơ hội cải
bottleneck     thiện
quan sát ở mức
giả thuyết     
  1              Vinhomes       Repetitive,       Bộ phận chăm   AI phân loại
Time-consuming,   sóc cư dân     yêu cầu, trích
Stakeholder Pain  tiếp nhận      xuất thông tin
nhiều yêu cầu  chính và đề
qua ứng dụng,  xuất bộ phận
hotline và     xử lý; nhân
quầy dịch vụ.  viên xác nhận
Nhân viên phải trước khi
đọc nội dung,  chuyển.
xác định loại
yêu cầu, mức
độ ưu tiên và
chuyển đến bộ
phận phụ
trách.         

  2              Vinmec         Time-consuming,   Nhân viên hành Trợ lý phân
AI-upgrade        chính phải đọc loại yêu cầu
và phân loại   hành chính,
các câu        kiểm tra
hỏi/yêu cầu    trường thông
đặt lịch,      tin còn thiếu
hướng dẫn thủ  và soạn câu
tục và chuyển  trả lời dựa
đúng bộ phận.  trên tài liệu
Nội dung có    đã duyệt;
thể thiếu      không chẩn
thông tin hoặc đoán hoặc tư
diễn đạt không vấn điều trị.
chuẩn.         

  3              Xanh SM (GSM)  Repetitive,       Bộ phận hỗ trợ AI phân loại
Stakeholder Pain  phải tiếp nhận phản ánh, nhận
phản ánh về    diện thông tin
chuyến đi như  chuyến đi và
điểm đón, thời đề xuất nhóm
gian chờ, hành xử lý; không
vi tài xế hoặc tự quyết định
thất lạc đồ;   bồi thường hay
việc đọc và    kỷ luật.
định tuyến
phản ánh có
thể thực hiện
thủ công.      

  4              VinFast        Repetitive,       Bộ phận hậu    AI chuẩn hóa
Time-consuming    mãi tiếp nhận  mô tả triệu
mô tả lỗi xe   chứng, trích
từ khách hàng  xuất mẫu xe/mã
với cách diễn  lỗi/thời điểm
đạt khác nhau. và đề xuất
Nhân viên cần  nhóm tiếp
đọc mô tả, hỏi nhận; kỹ thuật
thêm thông tin viên xác minh.
và chuyển đến
nhóm kỹ thuật
phù hợp.       
5              Vinpearl /     AI-upgrade,       Khách thường   Trợ lý hỏi đáp
VinWonders     Stakeholder Pain  hỏi lặp lại về dựa trên kho
vé, giờ hoạt   tri thức được
động, quy      cập nhật, trả
định, dịch vụ  lời kèm nguồn
và lịch trình. và chuyển nhân
Thông tin có   viên khi thiếu
thể nằm ở      dữ liệu hoặc
nhiều tài liệu câu hỏi ngoài
hoặc thay đổi  phạm vi.
theo cơ
sở/ngày.
1.3. Sàng lọc ban đầu
  Bài toán    Mức độ lặp  Có dữ liệu   Mức phù hợp Rủi ro nếu  Nhận định
lại         đầu vào dạng AI          AI sai
số/văn bản                           
  Vinhomes    Cao         Cao, nếu có  Cao         Trung bình  Ưu tiên
--- phân                ticket/log                           phân tích
loại yêu                                                     sâu; có thể
cầu cư dân                                                   giới hạn AI
ở khâu hỗ
trợ nhân
viên.

  Vinmec ---  Cao         Cao, nếu có  Trung       Cao nếu     Chỉ xem xét
phân loại               log tiếp     bình--cao   vượt sang   phạm vi
yêu cầu                 nhận                     tư vấn y tế hành chính,
hành chính                                                   không xử lý
quyết định
y khoa.

  Xanh SM --- Cao         Cao, nếu     Cao         Trung       Có tiềm
phân loại               liên kết                 bình--cao   năng, nhưng
phản ánh                được mã                              quyết định
chuyến đi               chuyến                               bồi thường
cần con
người.

  VinFast --- Trung       Trung        Cao         Cao nếu AI  AI chỉ
chuẩn hóa   bình--cao   bình--cao                kết luận    trích
mô tả lỗi                                        lỗi kỹ      xuất/định
thuật       tuyến,
không chẩn
đoán hoặc
hướng dẫn
sửa chữa.
Vinpearl    Cao         Cao nếu có   Cao         Trung bình  Có thể
--- hỏi đáp             knowledge                            triển khai
dịch vụ                 base chuẩn                           RAG, cần
quản trị
phiên bản
nội dung.
Kết quả Phase 1: Chọn 3 bài toán để làm Quick Problem Cards: (1)
Vinhomes --- phân loại yêu cầu cư dân; (2) Xanh SM --- phân loại phản
ánh chuyến đi; (3) Vinpearl --- trợ lý hỏi đáp dịch vụ. Đây là lựa chọn
theo mức phù hợp AI và khả năng giới hạn rủi ro, không phải kết luận về
mức độ ưu tiên thực tế của các công ty.
Phase 2 --- QUICK-ASSESS
Quick Problem Card #1 --- Vinhomes: Phân loại và định tuyến yêu cầu cư dân
Bài toán (1 câu): Nhân viên chăm sóc cư dân mất thời gian đọc, phân
loại và chuyển các yêu cầu gửi qua nhiều kênh đến đúng bộ phận phụ
trách.

Công ty thành viên: Vinhomes.

Actor đang gặp vấn đề: - Nhân viên chăm sóc cư dân / tổng đài: tiếp
nhận và phân loại yêu cầu. - Bộ phận kỹ thuật, vệ sinh, an ninh, vận
hành tiện ích: nhận và xử lý ticket. - Cư dân: cần được tiếp nhận và cập
nhật tiến độ đúng hạn.

Workflow thủ công hiện tại (giả thuyết): 1. Cư dân gửi yêu cầu qua
ứng dụng, hotline hoặc quầy dịch vụ. 2. Nhân viên đọc nội dung, kiểm tra
căn hộ/tòa nhà và hỏi bổ sung nếu thiếu thông tin. 3. Nhân viên xác định
nhóm vấn đề, mức độ ưu tiên và bộ phận chịu trách nhiệm. 4. Nhân viên
tạo/cập nhật ticket và chuyển bộ phận xử lý. 5. Bộ phận phụ trách tiếp
nhận, xử lý và cập nhật trạng thái; CSKH phản hồi cư dân.

Bottleneck: Bước 2--4, đặc biệt khi nội dung không rõ, sai chính tả,
nhiều vấn đề trong một yêu cầu hoặc phải chuyển qua lại.
Ước tính sơ bộ: 5--8 phút/ticket cho thao tác đọc, phân loại và định
tuyến; cần đo bằng timestamp thực tế.

AI hỗ trợ ở đâu? Sau khi tiếp nhận, AI trích xuất thông tin, phân
loại chủ đề, phát hiện trường còn thiếu và đề xuất nhóm xử lý/mức ưu
tiên. Nhân viên xem lại và xác nhận trước khi tạo hoặc chuyển ticket.

Metric đề xuất: - Giảm thời gian phân loại và định tuyến trung vị từ
baseline giả định 6 phút xuống không quá 2 phút/ticket. - Ít nhất 90%
ticket được gợi ý đúng nhóm xử lý trong tập kiểm thử đã gán nhãn. - Tỷ
lệ nhân viên phải sửa nhóm phân loại không quá 10%. - 100% ticket có độ
tin cậy thấp hoặc thuộc nhóm khẩn cấp được chuyển người kiểm tra.

Quick Architecture: LLM có cấu trúc đầu ra JSON kết hợp Rule-based
validation và Human-in-the-loop. Không cần Agent tự hành ở phiên bản
đầu.
Quick Problem Card #2 --- Xanh SM: Phân loại phản ánh sau chuyến đi
Bài toán (1 câu): Bộ phận hỗ trợ mất thời gian đọc phản ánh sau
chuyến đi, đối chiếu thông tin và chuyển phản ánh đến đúng nhóm xử lý.

Công ty thành viên: Xanh SM (GSM).

Actor đang gặp vấn đề: - Nhân viên chăm sóc khách hàng: đọc và phân
loại phản ánh. - Bộ phận vận hành / quản lý tài xế: xử lý theo loại sự
cố. - Khách hàng và tài xế: cần được xác minh sự việc công bằng.

Workflow thủ công hiện tại (giả thuyết): 1. Khách hàng gửi phản ánh
qua ứng dụng hoặc kênh CSKH. 2. Nhân viên đọc nội dung và yêu cầu mã
chuyến/thông tin bổ sung. 3. Nhân viên tra cứu chuyến đi và phân loại
phản ánh. 4. Nhân viên chuyển đến nhóm vận hành, thanh toán hoặc hỗ trợ
phù hợp. 5. Nhóm phụ trách xác minh và phản hồi kết quả.

Bottleneck: Đọc nội dung tự do và xác định đúng nhóm xử lý, nhất là
phản ánh có nhiều vấn đề hoặc thiếu mã chuyến.
Ước tính sơ bộ: 4--7 phút/phản ánh, chưa tính thời gian chờ xác
minh.

AI hỗ trợ ở đâu? Phân loại chủ đề (điểm đón, thời gian chờ, thái độ
phục vụ, thanh toán, thất lạc đồ...), trích xuất mã chuyến nếu có và đề
xuất thông tin cần hỏi thêm.

Metric đề xuất: - Giảm thời gian phân loại trung vị từ baseline giả
định 5 phút xuống không quá 2 phút. - Macro-F1 tối thiểu 0,90 trên tập
kiểm thử đại diện. - Tỷ lệ đề xuất sai nhóm dưới 5% trong nhóm lỗi
nghiêm trọng. - Không tự động kết luận lỗi thuộc về khách hàng/tài xế,
không tự duyệt bồi thường.

Quick Architecture: LLM classification + Rule-based kiểm tra mã
chuyến/trường bắt buộc + Human review. Agent chưa cần thiết vì quy trình
định tuyến có thể xử lý bằng workflow cố định.
Quick Problem Card #3 --- Vinpearl / VinWonders: Trợ lý hỏi đáp dịch vụ
Bài toán (1 câu): Nhân viên CSKH phải trả lời nhiều câu hỏi lặp lại
về vé, giờ hoạt động, quy định và tiện ích trong khi thông tin có thể
nằm ở nhiều tài liệu.

Công ty thành viên: Vinpearl / VinWonders.

Actor đang gặp vấn đề: - Nhân viên CSKH: tra cứu thông tin và phản
hồi khách. - Khách tham quan: cần câu trả lời nhanh, chính xác theo cơ
sở và thời điểm. - Nhân viên vận hành: cập nhật nội dung khi có thay
đổi.

Workflow thủ công hiện tại (giả thuyết): 1. Khách gửi câu hỏi qua
website, ứng dụng hoặc hotline. 2. Nhân viên xác định cơ sở, ngày tham
quan và nội dung cần hỏi. 3. Nhân viên tìm thông tin trong FAQ, tài liệu
hoặc hỏi bộ phận vận hành. 4. Nhân viên soạn câu trả lời và gửi khách.
5. Nếu câu hỏi ngoài phạm vi, nhân viên chuyển bộ phận liên quan.

Bottleneck: Tra cứu đúng phiên bản thông tin và ghép ngữ cảnh (cơ
sở, ngày, loại vé, đối tượng khách).
Ước tính sơ bộ: 3--6 phút/câu hỏi cần tra cứu.

AI hỗ trợ ở đâu? RAG truy xuất từ FAQ/chính sách đã duyệt, tạo câu
trả lời ngắn kèm nguồn tài liệu và thời điểm cập nhật; từ chối trả lời
nếu không tìm được căn cứ.

Metric đề xuất: - Giảm thời gian xử lý câu hỏi phổ biến từ baseline
giả định 4 phút xuống không quá 1 phút. - Tỷ lệ câu trả lời có căn cứ
trong knowledge base đạt ít nhất 95% trên bộ câu hỏi kiểm thử. - Tỷ lệ
câu trả lời sai về giá vé/điều kiện sử dụng bằng 0 trong bộ kiểm thử
quan trọng. - Câu hỏi không có nguồn hoặc có thông tin mâu thuẫn phải
chuyển nhân viên.

Quick Architecture: RAG + LLM, có kiểm tra nguồn và fallback sang
nhân viên. Cần cơ chế cập nhật và vô hiệu hóa tài liệu hết hạn.
Kết luận lựa chọn bài toán cho Phase 3
Đề xuất chọn Vinhomes --- AI hỗ trợ phân loại và định tuyến yêu cầu cư
dân để phân tích sâu.

Lý do lựa chọn: 1. Đầu vào chủ yếu là văn bản mô tả yêu cầu, phù hợp
với năng lực phân loại và trích xuất thông tin của LLM. 2. Đầu ra có thể
giới hạn thành nhãn, trường dữ liệu và gợi ý bộ phận; không trao quyền
tự quyết định các hành động rủi ro. 3. Có thể đo hiệu quả bằng thời gian
xử lý, độ chính xác phân loại, tỷ lệ sửa kết quả và tỷ lệ chuyển đúng bộ
phận. 4. Có thể giữ nhân viên làm bước phê duyệt, đồng thời quay về quy
trình hiện tại khi AI không chắc chắn.

Giả định cần xác minh trước khi triển khai: Vinhomes có hệ thống
ticket hoặc log tiếp nhận đủ quyền truy cập; dữ liệu được phép sử dụng
cho thử nghiệm; có taxonomy nhóm yêu cầu và bộ phận chịu trách nhiệm
được thống nhất.