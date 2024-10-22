#  LAB 1
# PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG HỆ THỐNG "PAYROLL SYSTEM"

## 1. Đề xuất kiến trúc, giải thích lý do lựa chọn và ý nghĩa từng thành phần trong kiến trúc, vẽ biểu đồ package mô tả kiến trúc

### Đề xuất kiến trúc:
#
Hệ thống Payroll System là một hệ thống quản lý bảng lương , có nhiều người dùng và tích hợp với cơ sở dữ liệu khác nhau.Kiến trúc phù hợp cho hệ thống này là kiến trúc phân lớp (Layered Architecture), với 4 lớp chính:
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
## 2. Cơ chế phân tích
### Đề xuất các cơ chế phân tích :
#### Xác thực và phân quyền: Đảm bảo chỉ nhân viên mới có thể xem và chỉnh sửa dữ liệu của riêng họ.
-Lý do: Tăng cường tính bảo mật và phù hợp với yêu cầu không cho phép truy cập dữ liệu của nhân viên khác.
#### Tính toán lương: Tự động tính lương theo giờ, theo hoa hồng và theo lương cố định.
-Lý do: Cơ chế quan trọng để hệ thống trả lương chính xác theo quy định.
#### Bảo mật thông tin cá nhân: Bảo vệ thông tin nhân viên và dữ liệu lương.
-Lý do: Đáp ứng yêu cầu bảo mật thông tin nhân viên nhạy cảm.
#### Đồng bộ hóa dữ liệu: Hệ thống mới cần lấy dữ liệu từ cơ sở dữ liệu DB2 mà không làm ảnh hưởng đến dữ liệu gốc.
-Lý do: Tương thích với cơ sở dữ liệu cũ và tránh làm gián đoạn hệ thống hiện có.
