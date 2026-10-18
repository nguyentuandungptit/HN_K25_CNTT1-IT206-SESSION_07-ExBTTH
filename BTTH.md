# Kế hoạch Sprint tích hợp cho CampusFood

- Môn học: IT206 (Quản lý dự án với Agile/Scrum)
- Bài học: Session 07 - Bài tập tổng hợp: Xây dựng kế hoạch Sprint tích hợp
- Dự án: CampusFood (Đặt món trực tuyến, quét mã QR và nhận đồ ăn tại 2 căn tin trong trường)
- Khung thời gian: Sprint 10 ngày làm việc
- Nhóm phát triển: Lan (Frontend), Minh (Backend), Ngọc (QA/BA), Phúc (Tích hợp)

---

## 1. Thông tin đầu vào của dự án

### Quỹ thời gian làm việc của các thành viên (Sprint 10 ngày)
- Lan (Frontend): 10 ngày x 6 giờ/ngày - 6 giờ hỗ trợ dự án khác = 54 giờ.
- Minh (Backend): 8 ngày x 6 giờ/ngày - 0 giờ = 48 giờ.
- Ngọc (QA/BA): 10 ngày x 5 giờ/ngày - 5 giờ họp dự án khác = 45 giờ.
- Phúc (Tích hợp): 9 ngày x 6 giờ/ngày - 8 giờ bảo trì hệ thống cũ = 46 giờ.
- Tổng quỹ giờ ban đầu của cả nhóm: 54 + 48 + 45 + 46 = 193 giờ.

### Danh sách Product Backlog và kết quả Planning Poker
- CF01: Xem thực đơn, kiểm tra còn món hay hết món (Ưu tiên 1), đồng thuận 3 SP, đã đủ tiêu chí sẵn sàng (DoR).
- CF02: Tạo đơn hàng, cấp mã nhận món (Ưu tiên 2), đồng thuận 5 SP, phụ thuộc sau CF01.
- CF03: Chọn điểm nhận món (Ưu tiên 3), kết quả bỏ phiếu là 3, 5, 5, 8 SP (chưa rõ phạm vi giao ngoài trường).
- CF04: Nhận đơn và cập nhật trạng thái giao hàng (Ưu tiên 4), kết quả bỏ phiếu là 5, 8, 8, 13 SP (phụ thuộc sau CF02, CF03; bất đồng về giải pháp kỹ thuật).
- CF05: Xem trạng thái giao hàng (Ưu tiên 5), đồng thuận 5 SP, phụ thuộc sau CF04.
- CF06: Thanh toán qua mã QR (Ưu tiên 6), kết quả bỏ phiếu là 5, 8, 13, 13 SP (chưa có tài liệu và cam kết thời gian phản hồi từ cổng thanh toán).
- CF07: Gửi biên nhận điện tử (Ưu tiên 7), đồng thuận 3 SP, phụ thuộc sau CF06.
- CF08: Hoàn tiền khi quán hủy đơn (Ưu tiên 8), tạm chốt 13 SP, chưa có tiêu chí chấp nhận (AC).
- CF09: Đánh giá người giao món (Ưu tiên 9), đồng thuận 3 SP, chưa có quy tắc sửa hoặc xóa đánh giá.

### Lịch sử Velocity các Sprint trước
- Sprint 3: 18 SP
- Sprint 4: 21 SP
- Sprint 5: 15 SP (Có một PBI 8 SP mới làm được 75% nên không được tính điểm).
- Velocity trung bình 3 Sprint gần nhất: (18 + 21 + 15) / 3 = 18 SP.

### Số liệu Burndown thực tế qua từng ngày (từ Ngày 0 đến Ngày 10)
- Điểm còn lại mỗi ngày: 21, 21, 18, 18, 23, 18, 18, 13, 8, 5, 5 SP.
- Các sự kiện xảy ra trong Sprint:
  - Ngày 4: PO đưa thêm tính năng mới tương đương 5 SP vào giữa chừng.
  - Ngày 5: Cổng thanh toán QR bị chậm phản hồi làm ách tắc kiểm thử.
  - Ngày 6: Nhóm họp nhưng không thống nhất được ai chịu trách nhiệm xử lý.

---

## 2. Làm rõ các hạng mục có ý kiến khác nhau khi ước lượng

Nhóm phân loại nguyên nhân và thống nhất phương án xử lý cho 4 hạng mục có phiếu chấm chênh lệch:

| Mã PBI | Tên hạng mục | Các mức phiếu | Lý do chênh lệch ý kiến | Hướng thống nhất | Điểm chốt |
| :---: | :--- | :---: | :--- | :--- | :---: |
| CF03 | Chọn điểm nhận | 3, 5, 5, 8 | Người chấm 8 lo ngại việc mở rộng địa chỉ giao ra ngoài trường sẽ kéo theo bản đồ, tính khoảng cách và phí ship. Người chấm 3 và 5 chỉ tính việc chọn giữa 2 căn tin trong trường. | Thống nhất với PO chỉ làm việc chọn giữa 2 căn tin nội khu trường trong Sprint này. Tính năng giao ngoài trường tách ra để làm sau. | 3 SP |
| CF04 | Nhận đơn và cập nhật giao | 5, 8, 8, 13 | Phiếu 13 lo ngại việc thông báo thời gian thực và xung đột dữ liệu khi nhiều người cùng bấm nhận một đơn hàng. Phiếu 5 chỉ tính việc đổi trạng thái đơn giản trong cơ sở dữ liệu. | Dùng cơ chế khóa bản ghi cơ bản, ai bấm trước thì nhận trước, kèm kiểm tra trạng thái qua API thông thường thay vì dựng hạ tầng phức tạp. | 8 SP |
| CF06 | Thanh toán QR | 5, 8, 13, 13 | Hai phiếu 13 điểm xuất phát từ rủi ro chưa có tài liệu API và chưa rõ thời gian phản hồi từ bên cổng thanh toán. Phiếu 5 và 8 giả định bên thứ ba đã có sẵn môi trường thử nghiệm chạy tốt. | Phúc liên hệ ngay đối tác để lấy tài liệu kết nối. Phạm vi Sprint này chỉ làm việc sinh mã VietQR động kèm callback cơ bản xác nhận tiền về. | 8 SP |
| CF08 | Hoàn tiền quán hủy | Tạm chốt 13 | Chưa có tiêu chí chấp nhận nào, chưa rõ quy trình hoàn tiền qua ngân hàng, ví hay đổi thành điểm tích lũy, cũng chưa rõ ai duyệt hoàn tiền. | Loại hẳn khỏi Sprint này vì chưa đạt chuẩn sẵn sàng (DoR). Trả lại Product Backlog để PO viết tiêu chí chi tiết. | Loại khỏi Sprint |

---

## 3. Mục tiêu Sprint và phạm vi công việc

### Tuyên ngôn mục tiêu Sprint (Sprint Goal)
"Vận hành luồng đặt món hoàn chỉnh từ xem thực đơn, tạo đơn hàng, thanh toán qua mã QR đến nhận món và cập nhật trạng thái tại 2 căn tin trong trường."

### Danh sách Product Backlog đưa vào Sprint

| Mã PBI | Tên User Story | Điểm SP | Lý do lựa chọn |
| :---: | :--- | :---: | :--- |
| CF01 | Xem thực đơn, còn món hay hết món | 3 | Chức năng đầu tiên người dùng nhìn thấy, đã có đủ tiêu chí chấp nhận. |
| CF02 | Tạo đơn hàng, cấp mã nhận món | 5 | Tạo giao dịch mua hàng, nối tiếp sau CF01. |
| CF03 | Chọn điểm nhận tại 2 căn tin trường | 3 | Xác định căn tin nhận món, phạm vi đã được chốt rõ. |
| CF06 | Thanh toán qua mã QR | 8 | Đảm bảo đúng mục tiêu thanh toán không dùng tiền mặt của Sprint. |
| CF04 | Nhận đơn và cập nhật trạng thái giao | 8 | Hoàn tất khâu nhận và bàn giao đồ ăn tại căn tin. |

Tổng khối lượng của 5 PBI là 27 SP. Nhóm đặt cam kết chính vào 19 SP đầu tiên (CF01, CF02, CF03, CF06) để bảo đảm luồng đặt món và trả tiền chạy thông suốt; CF04 (8 SP) được theo dõi sát theo tiến độ làm việc thực tế.

### Tiêu chuẩn hoàn thành của nhóm (Definition of Done)
1. Mã nguồn được ít nhất một lập trình viên khác xem và duyệt (peer review), không còn cảnh báo lỗi linter.
2. Viết unit test cho các luồng xử lý chính với độ bao phủ từ 80% trở lên.
3. Vượt qua kiểm thử chức năng của QA trên môi trường Staging, không còn lỗi nghiêm trọng.
4. Đạt toàn bộ tiêu chí chấp nhận đã chốt với PO.
5. Triển khai lên môi trường kiểm thử và có tài liệu tóm tắt các bước dùng thử cho căn tin.

---

## 4. Phân rã công việc và điều chỉnh giờ làm việc thực tế

### Cập nhật giờ làm việc sau khi có thay đổi nhân sự
- Trước biến động: Cả nhóm có 193 giờ (Lan 54h, Minh 48h, Ngọc 45h, Phúc 46h).
- Sau biến động: Minh bận việc đột xuất nên nghỉ thêm 2 ngày, giảm 12 giờ làm việc (còn 36 giờ).
- Quỹ giờ mới của cả nhóm: 193 - 12 = 181 giờ.
- Phương án gỡ nghẽn: Minh chỉ còn 36 giờ nên phần backend sẽ bị chậm nếu làm một mình. Phúc có nền tảng backend nên sẽ nhận bớt các việc viết API tạo đơn hàng để Minh tập trung vào luồng thực đơn và dữ liệu căn tin.

### Bảng phân rã công việc cho 3 PBI tiêu biểu

| Hạng mục | Mã việc | Nội dung công việc | Người làm | Ước tính giờ | Phụ thuộc |
| :---: | :---: | :--- | :---: | :---: | :---: |
| CF01 (3 SP) | T-01.1 | Dựng giao diện danh sách thực đơn và nhãn trạng thái món | Lan | 8h | Không |
| | T-01.2 | Viết API lấy danh sách món ăn và số lượng theo từng căn tin | Minh | 6h | Không |
| | T-01.3 | Nối API thực đơn vào giao diện, lưu dữ liệu tạm phía client | Lan | 4h | T-01.1, T-01.2 |
| | T-01.4 | Viết kịch bản và kiểm thử hiển thị món ăn trên môi trường test | Ngọc | 5h | T-01.3 |
| CF02 (5 SP) | T-02.1 | Dựng giao diện giỏ hàng và màn hình xác nhận đơn hàng | Lan | 10h | T-01.1 |
| | T-02.2 | Viết API tạo đơn, kiểm tra tồn kho và sinh mã nhận món | Minh, Phúc | 12h | T-01.2 |
| | T-02.3 | Ghép luồng đặt hàng giữa giao diện và backend | Lan, Minh | 6h | T-02.1, T-02.2 |
| | T-02.4 | Kiểm thử các trường hợp đặt hàng hợp lệ, đặt trùng, hết món | Ngọc | 8h | T-02.3 |
| CF06 (8 SP) | T-06.1 | Đọc tài liệu đối tác, lập danh sách tham số kết nối và mã lỗi | Phúc | 8h | Tài liệu đối tác |
| | T-06.2 | Viết dịch vụ sinh mã VietQR động và API nhận webhook thanh toán | Phúc | 14h | T-06.1 |
| | T-06.3 | Dựng màn hình hiện mã QR và đồng hồ đếm ngược chờ trả tiền | Lan | 10h | T-02.1 |
| | T-06.4 | Kiểm thử các trường hợp thanh toán thành công, hết hạn và lỗi mạng | Ngọc | 10h | T-06.2, T-06.3 |

---

## 5. Đánh giá Velocity và lựa chọn phương án nhận việc

### Nhìn lại Velocity các Sprint trước
- Ba Sprint trước nhóm đạt lần lượt 18, 21 và 15 SP. Mức trung bình là 18 SP.
- Ở Sprint 5, một story 8 SP chỉ làm được 75% nên không được tính điểm, kéo điểm số xuống 15 SP. Điều này cho thấy nhóm gặp khó ở khâu hoàn tất kiểm thử vào cuối Sprint nếu nhận việc dàn trải.

### So sánh hai phương án nhận việc cho Sprint này

| Tiêu chí | Phương án A: Nhận theo mức trung bình cũ (18 - 21 SP) | Phương án B: Nhận theo giờ thực tế và rủi ro (16 - 19 SP) |
| :--- | :--- | :--- |
| Độ tin cậy | Thấp: Coi như nhân sự không thay đổi, trong khi thực tế Minh nghỉ mất 2 ngày khiến khâu backend chỉ còn 36 giờ. | Cao: Tính đúng theo số giờ còn lại của từng vai trò và tính đến rủi ro kết nối cổng thanh toán. |
| Ứng phó khi thành viên vắng mặt | Kém: Dễ bị dồn ứ công việc ở backend vào cuối kỳ, không ai kịp gánh. | Tốt: Chủ động phân công Phúc hỗ trợ backend ngay từ đầu để giữ tiến độ. |
| Đạt được mục tiêu Sprint | Yếu: Khi thiếu giờ, nhóm dễ cắt bớt kiểm thử để kịp bàn giao, làm giảm chất lượng. | Rất tốt: Tập trung hoàn thành trọn vẹn luồng đặt món và thanh toán không tiền mặt theo đúng chuẩn hoàn thành. |
| Áp lực làm việc | Căng thẳng: Cố nhận nhiều điểm để đẹp số liệu, dễ để lại lỗi cho các Sprint sau. | Ổn định: Nhận khối lượng vừa sức, làm đến đâu chắc đến đó. |

Nhóm quyết định chọn Phương án B.

---

## 6. Phân tích biểu đồ Burndown và xử lý bất thường

### Bảng theo dõi điểm số còn lại qua từng ngày
- Đường lý tưởng: Bắt đầu từ 21 SP ở Ngày 0, giảm đều mỗi ngày khoảng 2.1 SP để về 0 SP ở Ngày 10.
- Đường thực tế:
  - Ngày 0: 21 SP
  - Ngày 1: 21 SP
  - Ngày 2: 18 SP (hoàn thành CF01, giảm 3 SP)
  - Ngày 3: 18 SP (chưa có thêm việc nào xong hẳn)
  - Ngày 4: 23 SP (tăng vọt 5 SP do có việc mới thêm vào)
  - Ngày 5: 18 SP (cổng thanh toán phản hồi chậm)
  - Ngày 6: 18 SP (họp nhưng chưa chốt cách làm)
  - Ngày 7: 13 SP
  - Ngày 8: 8 SP
  - Ngày 9: 5 SP
  - Ngày 10: 5 SP (kết thúc Sprint vẫn còn 5 SP chưa xong)

### Điều tra 3 điểm bất thường và cách xử lý
1. Ngày 4 điểm số nhảy từ 18 lên 23 SP:
   - Nguyên nhân: PO tự ý đưa thêm story mã khuyến mãi (5 SP) vào Sprint mà không trao đổi với nhóm và không rút việc cũ ra.
   - Dữ liệu cần kiểm tra: Xem lại nhật ký Daily Scrum ngày hôm đó và lịch sử cập nhật trên bảng Jira.
   - Cách xử lý: Scrum Master trao đổi lại với PO về nguyên tắc không được tự ý nhét thêm việc làm vỡ mục tiêu đã chốt. Nếu bắt buộc cần tính năng khuyến mãi thì phải rút một việc 5 SP khác ra ngoài, hoặc chuyển story này sang Sprint sau.
2. Ngày 5 và 6 đường burndown đi ngang ở mốc 18 SP:
   - Nguyên nhân: Phía đối tác cổng QR phản hồi chậm làm nghẽn khâu kiểm thử của Ngọc và Lan; cuộc họp ngày 6 diễn ra chung chung, không ai đứng ra chịu trách nhiệm gỡ rối.
   - Dữ liệu cần kiểm tra: Nhật ký gọi API sang cổng thanh toán và biên bản cuộc họp ngày 6.
   - Cách xử lý: Phúc lập tức dựng một dịch vụ giả lập (mock service) trả về kết quả quét QR để Lan và Ngọc tiếp tục kiểm thử giao diện và luồng xử lý đơn, không chờ đối tác.
3. Ngày 9 và 10 đứng yên ở mốc 5 SP, kết thúc Sprint vẫn còn 5 SP:
   - Nguyên nhân: Story xem trạng thái giao hàng hoặc tạo đơn bị kẹt ở khâu kiểm thử, phát hiện lỗi trước khi nghiệm thu nên chưa đạt chuẩn hoàn thành.
   - Dữ liệu cần kiểm tra: Trạng thái các thẻ việc trên bảng Scrum (cột Đang kiểm thử hoặc Lỗi).
   - Cách xử lý: Giữ nguyên số liệu thực tế, không sửa biểu đồ. Story này không được tính điểm vào Velocity của Sprint. Chuyển story về lại Product Backlog để PO đánh giá lại và đưa vào Sprint kế tiếp.

---

## 7. Bảng xử lý các tình huống ngoại lệ trong Sprint

| Tình huống ngoại lệ | Ảnh hưởng đến mục tiêu và chuẩn hoàn thành | Ảnh hưởng đến tiến độ và biểu đồ | Cách xử lý minh bạch |
| :--- | :--- | :--- | :--- |
| Mã QR bị lỗi sau khi tạo đơn hàng | Người dùng không trả được tiền, ảnh hưởng trực tiếp đến mục tiêu Sprint. | Làm chậm khâu nghiệm thu, đường burndown đi ngang vì tắc ở PBI CF06. | Chuẩn bị phương án dự phòng: Hiện số tài khoản ngân hàng và cú pháp chuyển khoản, hoặc cho phép trả tiền mặt tại quầy căn tin. Báo rõ tình trạng này ở buổi Daily Scrum. |
| Người dùng nhập thiếu số điện thoại hoặc chọn địa chỉ ngoài trường | Không ảnh hưởng mục tiêu vì nhóm đã thống nhất chỉ phục vụ 2 căn tin trường, nhưng có thể gây sai dữ liệu nếu không chặn từ đầu. | Không làm thay đổi điểm số đã cam kết. | Cài đặt kiểm tra dữ liệu chặt chẽ trên giao diện: Bắt buộc điền đủ 10 chữ số điện thoại và điểm nhận chỉ là danh sách chọn giữa 2 căn tin. Nhắc lại với PO rằng giao ngoài trường sẽ làm ở đợt sau. |
| PO đưa thêm story 5 SP (Mã khuyến mãi) vào giữa Sprint | Làm quá tải khả năng làm việc của nhóm, đe dọa các việc đã cam kết từ trước. | Biểu đồ burndown bị đẩy ngược lên 23 SP, làm lệch kế hoạch. | Scrum Master và nhóm họp với PO: Nếu PO cần tính năng khuyến mãi gấp thì phải rút một story 5 SP khác ra ngoài để giữ nguyên tổng khối lượng. Nếu không, chuyển việc này sang Sprint sau. |
| Story đạt 80% khối lượng nhưng chưa kịp kiểm thử khi hết Sprint | Không đạt Definition of Done vì chưa vượt qua khâu kiểm thử chất lượng. | Tính 0 SP cho story này trong Sprint hiện tại theo nguyên tắc xong hoàn toàn mới tính điểm. Điểm burndown dừng ở 5 SP. | Không nghiệm thu dở dang và không tính điểm một phần. Đưa lại story về Product Backlog, PO ước lượng lại phần việc còn thiếu để nhóm làm ở Sprint tới và báo rõ trong buổi Sprint Review. |
