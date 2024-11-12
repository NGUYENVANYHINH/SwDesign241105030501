
#  LAB 2
# PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG HỆ THỐNG "PAYROLL SYSTEM"

##  Đề xuất kiến trúc, giải thích lý do lựa chọn và ý nghĩa từng thành phần trong kiến trúc, vẽ biểu đồ package mô tả kiến trúc
### 1. Maintain Timecard
   
#### Tác nhân liên quan:

+Employee

- Mô tả:
Nhân viên nhập thông tin thời gian làm việc trong tuần vào thẻ chấm công và có thể chỉnh sửa, cập nhật cho đến khi nộp.

- Quy trình:

--> Nhân viên chọn chức năng nhập thẻ chấm công 
--> Hệ thống kiểm tra thẻ chấm công hiện tại cho nhân viên trong kỳ trả lương hiện tại:
--> Nếu chưa có, hệ thống sẽ tạo thẻ chấm công mới với ngày bắt đầu và kết thúc của kỳ hiện tại.
--> Nhân viên nhập các ngày làm việc, giờ làm việc và mã dự án liên quan.
--> Hệ thống lưu thông tin vào thẻ chấm công.
--> Khi nhân viên gửi thẻ chấm công, hệ thống kiểm tra tính hợp lệ:
--> Số giờ làm phải nằm trong khoảng hợp lệ và không vượt quá giới hạn.
--> Hệ thống lưu trạng thái "đã gửi" và khóa chỉnh sửa.

- Biểu đồ lớp phân tích:

+Timecard: Lưu trữ ngày bắt đầu, ngày kết thúc, số giờ làm mỗi ngày và trạng thái.

+Employee: Liên kết với Timecard (1-n).

+ProjectManagementDatabase: Hỗ trợ lấy mã dự án để nhân viên nhập vào thẻ.
- sơ đồ 
!(https://www.planttext.com/api/plantuml/png/b5BBQiCm4BphAnQVqj8SUZN1X3Q55feIIA7djRKuRlG8aXmmfL_MGp-flr0faModBwWEHjx7xCoiFjxUvzQXSQqKp6uR1KPROfL0Q-56xeJkYE25WJzJK2WfXxKpZQfZY6BD7Jz905I6qD5Z8wb2moU78GiVoI5yBu0K7txFSaYLiTssfMnSt-xYPQZpBNlTSFRA8jkKwDb-6Pa8Z-V6s4QtnZvfioK_O8cxsP7YGhUbe2B17HYvK7AbjI1KaIfoVXi09dmaxm2PHuZ4TInjyat02ZkZXLXtrf6CAW1g6bn8PkVzQdum3lVq7zjMHZzJvPQei2P9AZY69LeQCxZUeAdfePKbUPqUuxwnRdRSTn6m-gUINMOmdHQGdMS3irDb8Vr7Aa6nVg4X-YjDnkP-fU7vVW800F__0m00)
2. Run Payroll
Tác nhân liên quan:
System Clock
Bank System
Payroll Administrator
Mô tả:
Chạy quá trình tính lương định kỳ vào mỗi thứ Sáu và ngày làm việc cuối tháng, trả lương cho nhân viên dựa trên dữ liệu thời gian làm việc và các quy định về mức lương, hoa hồng (nếu có).

Quy trình:
Hệ thống được kích hoạt vào ngày chạy lương.
Hệ thống lấy danh sách nhân viên cần thanh toán cho kỳ hiện tại.
Đối với từng nhân viên:
Tính lương dựa trên thẻ chấm công, dữ liệu mức lương và các khấu trừ.
Nếu có phương thức thanh toán là chuyển khoản, hệ thống tạo giao dịch và gửi đến hệ thống ngân hàng.
Nếu phương thức thanh toán là gửi qua bưu điện hoặc lấy tại văn phòng, hệ thống in phiếu lương.
Lưu các giao dịch và trạng thái thanh toán cho nhân viên.
Biểu đồ lớp phân tích:
PayrollSystem: Quản lý quá trình tính lương, tạo và gửi giao dịch thanh toán.
Payment: Lưu thông tin giao dịch, bao gồm phương thức thanh toán, ngày thanh toán, trạng thái.
BankSystem: Xử lý các giao dịch qua ngân hàng.
3. Maintain Employee Information
Tác nhân liên quan:
Payroll Administrator
Mô tả:
Quản trị viên lương quản lý thông tin nhân viên, bao gồm thêm, chỉnh sửa và xóa thông tin nhân viên.

Quy trình:
Quản trị viên chọn chức năng quản lý thông tin nhân viên.
Hệ thống yêu cầu nhập mã nhân viên và chức năng cụ thể (thêm, cập nhật hoặc xóa):
Thêm: Hệ thống yêu cầu nhập thông tin chi tiết nhân viên như họ tên, địa chỉ, loại hợp đồng, phương thức thanh toán, mức lương, và các khấu trừ.
Cập nhật: Hệ thống lấy thông tin nhân viên từ mã và cho phép chỉnh sửa các trường dữ liệu.
Xóa: Hệ thống xác nhận và đánh dấu xóa nhân viên, lưu lại cho lần chạy lương tiếp theo.
Hệ thống lưu lại thay đổi và cập nhật vào cơ sở dữ liệu.
Biểu đồ lớp phân tích:
Employee: Lưu trữ thông tin nhân viên.
Payroll Administrator: Tác nhân có quyền truy cập và thay đổi thông tin nhân viên.
4. Create Reports
Tác nhân liên quan:
Employee
Payroll Administrator
Mô tả:
Nhân viên và quản trị viên có thể tạo báo cáo về giờ làm việc, lương nhận được, và các thông tin liên quan đến dự án hoặc ngày nghỉ.

Quy trình:
Tác nhân chọn chức năng báo cáo.
Hệ thống yêu cầu nhập các tiêu chí báo cáo như loại báo cáo (giờ làm việc, lương, số giờ làm việc trên dự án, nghỉ phép) và khoảng thời gian.
Nếu báo cáo liên quan đến dự án, hệ thống truy cập vào cơ sở dữ liệu dự án để lấy mã số dự án.
Hệ thống tạo báo cáo theo yêu cầu.
Tác nhân có thể chọn lưu hoặc chỉ xem báo cáo.
Biểu đồ lớp phân tích:
Report: Lưu trữ thông tin về báo cáo như loại, thời gian, nội dung chi tiết.
Employee và Payroll Administrator liên kết với Report để xem hoặc tạo báo cáo.
5. Select Payment Method
Tác nhân liên quan:
Employee
Mô tả:
Nhân viên lựa chọn phương thức thanh toán lương theo sở thích (lấy trực tiếp, gửi qua bưu điện hoặc chuyển khoản ngân hàng).

Quy trình:
Nhân viên chọn chức năng thay đổi phương thức thanh toán.
Hệ thống yêu cầu nhân viên chọn một trong ba phương thức:
Lấy trực tiếp: Không yêu cầu thêm thông tin.
Gửi qua bưu điện: Yêu cầu địa chỉ nhận.
Chuyển khoản ngân hàng: Yêu cầu tên ngân hàng và số tài khoản.
Hệ thống cập nhật phương thức thanh toán vào hồ sơ nhân viên.
Biểu đồ lớp phân tích:
Employee: Lưu trữ phương thức thanh toán.
BankSystem: Liên kết với Employee khi lựa chọn phương thức thanh toán là chuyển khoản.
