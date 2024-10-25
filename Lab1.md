#  LAB 1
# PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG HỆ THỐNG "PAYROLL SYSTEM"

## 1. Đề xuất kiến trúc, giải thích lý do lựa chọn và ý nghĩa từng thành phần trong kiến trúc, vẽ biểu đồ package mô tả kiến trúc

### Đề xuất kiến trúc:
#
Hệ thống Payroll System là một hệ thống quản lý bảng lương , có nhiều người dùng và tích hợp với cơ sở dữ liệu khác nhau.Kiến trúc phù hợp cho hệ thống này là kiến trúc phân lớp  (Layered Architecture), với 4 lớp chính:
#### Lớp Giao diện (Presentation Layer):
Chịu trách nhiệm hiển thị thông tin và nhận đầu vào từ người dùng. Lớp này sẽ gồm các giao diện cho các chức năng như nhập bảng chấm công, chọn phương thức thanh toán, và báo cáo.
Các công nghệ có thể sử dụng: Java Swing hoặc .NET Windows Forms cho giao diện desktop.
#### Lớp Dịch vụ (Service Layer):
Đảm nhiệm xử lý các logic nghiệp vụ của hệ thống, xử lý các yêu cầu liên quan đến tính lương, ghi nhận bảng chấm công, và thanh toán lương.
Lớp này tương tác với cơ sở dữ liệu thông qua các dịch vụ và API, đảm bảo sự tách biệt giữa giao diện và dữ liệu.
#### Lớp Dữ liệu (Data Access Layer):
Lớp này quản lý việc truy xuất, cập nhật dữ liệu từ cơ sở dữ liệu (Payroll Database, Project Management Database).
Lớp này sẽ kết nối với cơ sở dữ liệu của Project Management Database, nhưng chỉ truy xuất thông tin mà không cập nhật.
#### Lớp Lưu trữ (Storage Layer):
Chứa cơ sở dữ liệu cần thiết cho hệ thống. Hệ thống Payroll cần một cơ sở dữ liệu riêng để lưu trữ thông tin về nhân viên, bảng chấm công, và phiếu lương.
### Vẽ biểu đồ package mô tả kiến trúc
![](https://www.planttext.com/api/plantuml/png/b5J1Ji904BttAoQSyC35emU3qCI33O7G4A-RPKCRofPiTqqQuy6J1p_14nfYmaL9FD4O3vlm7_q2Vy4TG46wZNZgDlFUcpVpjltCFkg994AgKUGamv23Y1FcZ0aTaW63YfTd3sCu3qaCRfXdTnogRS4InYMHOSp18oaJHnMuTW1eH99aXNL3nbi1uJtpB1GwYd1VXCwDiz_6pRDx6a0lpwPGxJ9n5L9cwR268QgHBvxum5k-BYTyOAatWtmn7JNrcxNg6uU17-i9jtZnXKhXKXc-HCeBU3Y-WgfB984pIfdHAdgx2694hy6jG3-Q7UWPjzTjzffTr-iedClJxmOwrxVSRHnR79gnbR69tgfT6Gii5GsXNfka8euYrDXF1sgrqxA5mWd8pKdg2NNs0lmFjGpsMs9d7qOWrJC5D5yygmFfsppBsBiDa5kMXk57vYM5FcutMfKTQwE2oZRpFqIAavH4_wCZWvKtQJvI8pa7lBYb4tmBRh974RmlkrxAV1z0hJFUnp_65m000F__0m00)
## Cơ chế phân tích
### Đề xuất các cơ chế phân tích :
#### Xác thực và phân quyền: Đảm bảo chỉ nhân viên mới có thể xem và chỉnh sửa dữ liệu của riêng họ.
+Lý do: Tăng cường tính bảo mật và phù hợp với yêu cầu không cho phép truy cập dữ liệu của nhân viên khác.
#### Tính toán lương: Tự động tính lương theo giờ, theo hoa hồng và theo lương cố định.
+Lý do: Cơ chế quan trọng để hệ thống trả lương chính xác theo quy định.
#### Bảo mật thông tin cá nhân: Bảo vệ thông tin nhân viên và dữ liệu lương.
+Lý do: Đáp ứng yêu cầu bảo mật thông tin nhân viên nhạy cảm.
#### Đồng bộ hóa dữ liệu: Hệ thống mới cần lấy dữ liệu từ cơ sở dữ liệu DB2 mà không làm ảnh hưởng đến dữ liệu gốc.
+Lý do: Tương thích với cơ sở dữ liệu cũ và tránh làm gián đoạn hệ thống hiện có.
## Phân tích ca sử dụng
###  Phân tích ca sử dụng "Payment" (Thanh toán).
####  1. Xác định các tác nhân (actors).
+Admin (Quản trị viên): Người sẽ xem báo cáo thanh toán và theo dõi việc thực hiện thanh toán.

+Payroll System (Hệ thống thanh toán): Thực hiện việc tính lương và thanh toán tự động vào những ngày quy định.
####  2.Mô tả quy trình nghiệp vụ
+Bắt đầu: Hệ thống Payroll tự động kích hoạt vào các ngày thanh toán (thứ Sáu hàng tuần cho nhân viên theo giờ hoặc cuối tháng cho nhân viên lương cố định).

+Tính toán lương: Hệ thống tính toán lương dựa trên số giờ làm việc (thẻ chấm công) và mức lương hoặc hoa hồng (nếu có) của từng nhân viên.

+Thanh toán: Hệ thống thanh toán cho nhân viên theo phương thức họ đã chọn (chuyển khoản, nhận séc, hoặc nhận trực tiếp).

+Xác nhận: Hệ thống lưu lại trạng thái thanh toán và cập nhật thông tin vào cơ sở dữ liệu.

+Báo cáo: Quản trị viên có thể truy vấn hệ thống để xem báo cáo chi tiết về các khoản thanh toán.
 #### 3.Xác định các lớp phân tích
+Employee: Chứa thông tin về nhân viên, phương thức thanh toán, tài khoản ngân hàng, mức lương.

+Payroll: Thực hiện tính toán lương và thanh toán.

+Timecard: Chứa thông tin về số giờ làm việc của nhân viên.

+Project: Thông tin về các dự án và mã số công việc (charge number).

+PaymentService: Xử lý yêu cầu thanh toán lương.

+PayrollDatabase: Cơ sở dữ liệu lưu trữ thông tin lương và thanh toán.
#### 4. Biểu đồ lớp phân tích (Analysis Class Diagram)
![Analysis Class Diagram](https://www.planttext.com/api/plantuml/png/R991JiCm44NtFeMNiCW5iggWI6oG4At4UkfCYHKxZcR6aIh4oLXm9Av0NCSDgRgnfJypR_o__Flzis41akYTCWwOzPCVN3WXwa-bTMMRTFRWCTq3d3psyeBIXbJG7oYlMTkYW7LyTw--r4pQMuy6gCcaDaJYzq0Tdf5XH9AfuJd9CweCt61DMoWuTqPf0yv41uAJEZLDoa318FFybgl19EsGHckogTBz07st9-ZvYBJ2FBPekXlRjo1m09ufB85mnh-X2THa2A6GnH6BcxLQubrvl6HULKjgjUPuy5PuLIv1r4iAZJu6KgMGU_vxhdLaP7MbBgoBhJfxOhN1laa_uWy00F__0m00)
#### 5.Biểu đồ Sequence (Sequence Diagram)
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/T99DJiCm48NtESLSe1Ue46ggL8XT19JzC9bA1iSsut5BpiQ28t45d9-sKaWtbgptFljvdd-_VpPHKJIrja1IBr0shN75iCBgVjpk7s4DhuPF4B1hsIa81ozQdDLihB4JR-qpoz4GP_yJVoQEsYEz08IMaaKrtXKpSyPVJCk4qbIeM19nZCCHAeQF33gfq6HvWTwrmVgEUPdcIRr5r-BVcNGP3gC8nXty4ZiEvFhitHTJKZvFgfWPReLzO8KtT1-0H3wvwtqpU9izPTttaLCFx42fe8i7bWLYobnjCxCFUGINR92hrnGlBTwj_hTOcHWiTlFYD-oQ_i_y0G00__y30000)
###  Phân tích ca sử dụng "Maintain Timecard" (Duy trì thẻ chấm công).
####  1. Xác định các tác nhân (actors).
+Employee (Nhân viên): Người nhập và duy trì thông tin thẻ chấm công hàng ngày.

+Payroll System: Lưu trữ thông tin về thẻ chấm công và sử dụng dữ liệu này để tính lương.
####  2.Mô tả quy trình nghiệp vụ
+Nhập thông tin: Nhân viên nhập số giờ làm việc vào hệ thống hàng ngày.

+Xác thực: Hệ thống kiểm tra thông tin để đảm bảo tính hợp lệ (giờ làm việc không vượt quá giới hạn).

+Lưu trữ: Thông tin thẻ chấm công được lưu lại trong cơ sở dữ liệu và liên kết với nhân viên và dự án mà nhân viên đang làm việc.

+Xác nhận: Hệ thống lưu lại trạng thái thanh toán và cập nhật thông tin vào cơ sở dữ liệu.

+Xem lại: Nhân viên có thể xem lại các thẻ chấm công đã nhập để kiểm tra hoặc chỉnh sửa (nếu cần).
 #### 3.Xác định các lớp phân tích
+Employee: Nhân viên nhập thông tin thời gian làm việc.

+Payroll: Thực hiện tính toán lương và thanh toán.

+Timecard: Chứa các thuộc tính như số giờ làm việc, ngày làm việc, và dự án liên quan.

+TimecardService: Xử lý yêu cầu nhập thẻ chấm công và lưu trữ thông tin.

+TimecardDatabase: Lưu trữ tất cả các thẻ chấm công của nhân viên.

#### 4. Biểu đồ lớp phân tích (Analysis Class Diagram)
![Analysis Class Diagram](https://www.planttext.com/api/plantuml/png/V94nZi8m44LxdyBbRf4Bf4A2RMbOQUk9_GK66wEPIII4E1a5HzehB2OXe0XjOqiUp_Fxuz_BTIPAh6sAnaKIiL_f4FCHi2TZRHLyMVUKSDkjj4qA-XqI7B7_-3HdCtGzplekJrhkLvlSilnatk6EEN3UmkbyGxp6iaqDk53N694BA8KexyWhS1TShsKxYg4yyg9Iz3Gp_hDRa593Ca24kWc0eHpGJHZZHAhgcRCUXY5lom_PsjuoEuZ0s-PefkMNZb6jxcE8cM7loxVy0G00__y30000)
#### 5.Biểu đồ Sequence (Sequence Diagram)
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/X9112i8m44NtEKKkq0k8IDLsuKweFS0u6I6GD6KoBVHiBZoILp05RQCRTyF_xp7CFE-FCWgm3DufG0ciQz-xC16fpw2BtHAs9xtHTIV4Mgmd13Ogwn9vUSSDyMYH4juCLszbuRK10VMBPMQL-ZqYnJZBCD9_zGmJ1-UgGpBQFb6PmuI1JLpFsHRVvnn3TxFiLoEcdKQLr9dvAoy0003__mC0)
## Hợp nhất kết quả phân tích các ca sử dụng "Payment" và "Maintain Timecard"
### Lớp Employee (Nhân viên):
+Vai trò trong Payment: Nhận lương dựa trên giờ làm việc, mức lương hoặc hoa hồng.

+Vai trò trong Maintain Timecard: Nhập thông tin giờ làm việc.

+Tích hợp: Nhân viên vừa nhập thẻ chấm công vừa nhận lương từ hệ thống.
### Lớp Timecard (Thẻ chấm công):
+Vai trò: Chứa dữ liệu về giờ làm việc của nhân viên.

+Tích hợp: Là nguồn dữ liệu đầu vào cho việc tính lương.
### Lớp Payroll (Xử lý lương):
+Vai trò: Tính toán lương dựa trên thẻ chấm công và thông tin lương/hoa hồng.

+Tích hợp: Liên kết giữa thẻ chấm công và thanh toán lương.
### Lớp PaymentService (Dịch vụ thanh toán):
+Vai trò: Xử lý thanh toán (chuyển khoản, in hóa đơn).

+Tích hợp: Thực hiện thanh toán dựa trên kết quả tính lương.
### Lớp TimecardService (Dịch vụ thẻ chấm công):
+Vai trò: Xác minh và lưu trữ thẻ chấm công.

+Lớp PayrollDatabase (Cơ sở dữ liệu lương):

+Vai trò: Lưu trữ tất cả thông tin nhân viên, thẻ chấm công, và thanh toán.
### Mô hình tổng hợp: Nhân viên nhập thẻ chấm công, dữ liệu được xử lý để tính lương và thanh toán, quản trị viên có thể truy vấn báo cáo thanh toán đầy đủ.
