# Lab 3. Identify design elements
## Xác định các phần tử thiết kế của hệ thống “Payroll System”
### Subsystem context diagrams
#### Hệ thống con: BankSystem, PrintService, ProjectManagementDatabase subsystems.
#### 1. Biểu đồ ngữ cảnh cho các hệ thống con
1.1 Biểu đồ ngữ cảnh cho BankSystem
##### BankSystem là hệ thống bên ngoài xử lý các giao dịch ngân hàng cho nhân viên. Payroll System sẽ gửi yêu cầu chuyển khoản cho nhân viên có lựa chọn thanh toán qua ngân hàng, và BankSystem sẽ phản hồi kết quả giao dịch.
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT0OcLHVavES6LnIMgkWgwTWbDYNZQ4PwKGb5fOcbfSek2IMPIQ3AHI2_ABCqku44eKT84wK8omKd3EpqlBBCfL22bAp2jEJ2x9pCzJ22v9B2ajvd98pKi1MGe0003__mC0)
##### PayrollSystem: Hệ thống chính quản lý thông tin nhân viên và thực hiện tính toán tiền lương.
##### BankSystem: Hệ thống ngân hàng nhận yêu cầu chuyển khoản từ PayrollSystem và phản hồi trạng thái giao dịch.
#### Giải thích: PayrollSystem gửi yêu cầu chuyển khoản đến BankSystem và nhận phản hồi về trạng thái giao dịch (thành công/thất bại).
1.2 Biểu đồ ngữ cảnh cho PrintService
##### PrintService chịu trách nhiệm in phiếu lương. Sau khi PayrollSystem hoàn tất tính toán, nó sẽ gửi yêu cầu in phiếu lương đến PrintService.
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT0OcLHVavES6LnIMgkWgwTGa1HPbv9S6fHMMPogfL2S6fUYW9GJN96QdAsWajYII8NiW85NP0EP2Ei80OeEEVdfMKMvIQMPERdSJa0JG5P1W000F__0m00)
##### PayrollSystem: Gửi dữ liệu phiếu lương cho PrintService để in.
##### PrintService: In phiếu lương và xác nhận lại với PayrollSystem.
#### Giải thích: PrintService xử lý in phiếu lương và phản hồi PayrollSystem sau khi hoàn thành.
1.3 Biểu đồ ngữ cảnh cho ProjectManagementDatabase
###### ProjectManagementDatabase lưu thông tin các dự án và số hiệu mã dự án (charge number). PayrollSystem sẽ truy xuất dữ liệu từ hệ thống này để hỗ trợ tính toán chi phí dự án.
![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT0OcLHVavES6LnIMgkWgwTGa1HVbPgSeblObvYUcfkQbw9Is99Ob9YSQgLWbjgIN86J852ObwAWdD6Ob5wge9VQMvIQb4n5qwz2heWav6jib88IYqfBSg36mTIokMGcfS2SXK0003__mC0)
##### PayrollSystem: Truy xuất thông tin mã dự án từ ProjectManagementDatabase để kiểm tra dữ liệu làm việc của nhân viên.
##### ProjectManagementDatabase: Cơ sở dữ liệu chỉ cho phép truy xuất thông tin dự án mà không cập nhật.
#### Giải thích: PayrollSystem chỉ truy xuất thông tin từ ProjectManagementDatabase mà không có quyền thay đổi.
### 2.Chuyển lớp phân tích thành phần tử thiết kế
#### chuyển các lớp phân tích thành các phần tử thiết kế sau:

+Employee:

##### Thiết kế lớp Employee làm lớp cha với các lớp con cụ thể: HourlyEmployee, SalariedEmployee, và CommissionedEmployee.
##### Các lớp con sẽ bao gồm các thuộc tính riêng như hourlyRate, salary, và commissionRate.
+Timecard:

#### Thiết kế lớp Timecard để lưu thông tin thời gian làm việc của nhân viên.
#### Lớp TimecardManager quản lý các thao tác với timecard, như thêm mới, cập nhật và xác nhận.
+Purchase Order:

##### Thiết kế lớp PurchaseOrder chứa thông tin đơn hàng của nhân viên hưởng hoa hồng.
##### Lớp PurchaseOrderManager sẽ đảm nhận các thao tác tạo, cập nhật và xóa đơn hàng.
+Payroll Administrator:

##### Thiết kế lớp PayrollAdministrator cho phép thực hiện các hành động liên quan đến quản lý nhân viên và báo cáo hành chính.

 ### 3.Tổ chức các phần tử thiết kế thành các gói (Packages)
#### Tổ chức hệ thống thành các gói sau để rõ ràng và dễ quản lý:

+ UserManagement Package
##### Employee
##### HourlyEmployee
##### SalariedEmployee
##### CommissionedEmployee
##### PayrollAdministrator
##### PayrollProcessing Package

+ Timecard
##### TimecardManager
##### SalaryCalculator
##### OrderManagement Package

+ PurchaseOrder
##### PurchaseOrderManager
##### IntegrationServices Package

+ BankSystemInterface
##### PrintServiceInterface
##### ProjectManagementDatabaseInterface
### Giải thích: Các phần tử được nhóm theo chức năng, tạo ra một cấu trúc gói dễ bảo trì và mở rộng.

### 4. Kiến trúc tầng và quan hệ phụ thuộc giữa các tầng
#### Thiết kế hệ thống thành các tầng kiến trúc sau:

##### Presentation Layer: Quản lý giao diện người dùng, bao gồm các màn hình cho nhân viên và quản trị viên.
##### Business Logic Layer: Chứa các logic nghiệp vụ như tính toán lương và xử lý đơn hàng.
##### Data Access Layer: Xử lý truy cập dữ liệu từ cơ sở dữ liệu nội bộ và từ hệ thống ngoài.
##### Integration Layer: Quản lý giao tiếp với hệ thống ngoài như BankSystem, PrintService, và ProjectManagementDatabase.

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTqG55gSMfUIM99PdwUWazYPMfHh8AkdKAqKsbnPbvgSR62JtvwPZ9KXWkxC5Y3Is99ee9ZSZ9Oag1gpxoIrFGYP5kv75BpKa1E0W000F__0m00)
#### Giải thích:

##### Tầng Presentation chỉ giao tiếp với tầng Business Logic.
##### Business Logic xử lý các nghiệp vụ và truy xuất dữ liệu từ Data Access hoặc gọi đến Integration Layer khi cần tương tác với hệ thống ngoài.


