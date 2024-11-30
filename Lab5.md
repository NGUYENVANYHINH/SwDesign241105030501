# **Thiết kế hệ thống con trong Payroll System**

## **1. Giới thiệu**

Dựa trên kết quả từ bài Lab 4 về thiết kế các ca sử dụng (**Login**, **Maintain Timecard**, và **Run Payroll**), hệ thống **Payroll System** được chia thành các hệ thống con (**Subsystems**) để đảm bảo tính mô-đun, tái sử dụng, bảo mật và khả năng mở rộng.

---

## **2. Thiết kế các hệ thống con**

### **2.1 Login Subsystem**

**Mục đích**:  
- Hỗ trợ người dùng đăng nhập vào hệ thống.  
- Quản lý phiên đăng nhập (authentication session).  

**Chức năng chính**:  
- Kiểm tra thông tin xác thực (username, password).  
- Quản lý phiên đăng nhập của người dùng.  

**Thành phần**:  
- **LoginForm**: Giao diện để người dùng nhập thông tin đăng nhập.  
- **LoginController**: Xử lý logic nghiệp vụ cho ca sử dụng Login.  
- **EmployeeDatabase**: Lưu trữ thông tin tài khoản người dùng.  

**Luồng hoạt động chính**:  
1. Người dùng nhập thông tin vào **LoginForm**.  
2. **LoginController** xác thực thông tin với **EmployeeDatabase**.  
3. Nếu hợp lệ, hệ thống khởi tạo phiên đăng nhập; nếu không, trả về thông báo lỗi.  

**Mô hình hệ thống con**:

 ![](https://www.planttext.com/api/plantuml/png/P91D3e9038NtSug9Arrm0HQ617NbZXEKePA9yqEcXOGe9tFXaRo20v6eq4MJjk_bU-dhySo88N1hZMX0NQ56kJdxMZjPj2Nrn6WtyYQaL0Q8v7Gw-M2dNQmEZAw0SRkBy_2loxtZu8t1CAjLmAWja4Xxjx0SRMDyZtW0XX88buGyO8MEDHZwE6FxvacI-tw5JQLsZ04Kqop-kKwM5JQL7GPzqKXZt1af1f6XgyO_lG400F__0m00)
 
---
### **2.2 Timecard Management Subsystem**

**Mục đích**:
- Quản lý bảng chấm công của nhân viên.
- Quản lý mã dự án (charge codes).

**Chức năng chính**:
- Lấy bảng chấm công hiện tại của nhân viên.
- Lưu bảng chấm công sau khi chỉnh sửa.
- Cung cấp danh sách mã dự án hợp lệ.

**Thành phần**:
- **TimecardForm**: Giao diện để nhân viên nhập và chỉnh sửa bảng chấm công.
- **TimecardController**: Xử lý logic nghiệp vụ.
- **ProjectManagementDatabase**: Lưu trữ bảng chấm công và mã dự án.

**Luồng hoạt động chính**:
1. **TimecardController** lấy dữ liệu bảng chấm công từ **ProjectManagementDatabase**.
2. **TimecardForm** hiển thị dữ liệu để nhân viên chỉnh sửa.
3. Sau khi chỉnh sửa, **TimecardController** lưu dữ liệu vào **ProjectManagementDatabase**.

**Mô hình hệ thống con**:

 ![](https://www.planttext.com/api/plantuml/png/X94zJWD138NxFOML2eg8FWMAj8WE2GakuCmyDWFpixAzaQ8a9wFWIBb2beGL-I72XOjd-_EplFtycggnM9TYrRBxu0OqUWq9ZiNJ4-TUICX6BzrCbsf88rfLH2woAWsDZqNINkx31sqZBuVIpUr1XWzsecqkA7N99YL6oC1gOESSvGMkS9wblCFPh-a7DfwnOi2zmTpyN-1XRprdQL0N3_rPqwUJUyVZzVrVtYSKia7OcHwD73Ni1w-RdP309601lUjQpmQbFdErgQR8_ljJEm000F__0m00)
 
##
### **2.3 Payroll Processing Subsystem**

**Mục đích**:  
- Điều phối việc tính toán lương và xử lý thanh toán.

**Chức năng chính**:  
- Lấy thông tin nhân viên và bảng chấm công.  
- Tính toán lương dựa trên loại nhân viên.  
- Tạo phiếu lương (**Paycheck**).  
- Điều phối việc gửi thanh toán hoặc in phiếu lương.

**Thành phần**:  
- **PayrollController**: Điều phối toàn bộ quy trình.  
- **PaycheckManager**: Quản lý việc tạo và lưu phiếu lương.  
- **Timecard**, **Employee**, **Paycheck**: Các thực thể cung cấp thông tin và lưu kết quả.

**Luồng hoạt động chính**:  
1. **PayrollController** khởi động từ **SystemClock** vào ngày trả lương.  
2. Lấy dữ liệu từ **Timecard** và **Employee** để tính toán.  
3. Tạo **Paycheck** và chuyển thông tin đến **Banking Subsystem** hoặc **Printing Subsystem**.

**Mô hình hệ thống con**:  

 ![](https://www.planttext.com/api/plantuml/png/T97DIiD04CVlUOgXfthe2_GW1HMy20K5p-DaY26RtJ0pMmYrJ-R1H_8Lt2RP62tDOGE__yVExdv_VktKK2oshkYG6gmOLdli9JW7Umd4ghMlu3c-QQ_6xGgE1G0vL8N9TnUydVyiWvO-YNxIrZSZ8NGK7HedFh3JieNUcPedz6dtkOE4H_iWvXx5mr_ss_DIjqmePIwes1v357qDqd3vp_pGTYxqp0jpHlTiM3kT0ccvFEPcyt5xCVSMkl6-MA6RjElfUTej29lKV4Wnox14m-lPUVXbbZCSigTYnxuyl-eF0000__y30000)
 
 
### **2.4 Banking Subsystem**

**Mục đích**:  
- Thực hiện các giao dịch ngân hàng, bao gồm chuyển khoản lương cho nhân viên.

**Chức năng chính**:  
- Xử lý chuyển khoản ngân hàng.  
- Giao tiếp với các hệ thống ngân hàng bên ngoài.

**Thành phần**:  
- **BankSystem**: Xử lý các giao dịch ngân hàng.  
- **IBankSystem (interface)**: Định nghĩa phương thức giao tiếp, ví dụ:
  - `deposit(Paycheck, BankInfo)`: Chuyển khoản tiền lương vào tài khoản của nhân viên.

**Luồng hoạt động chính**:  
1. **PayrollController** gửi yêu cầu thanh toán đến **BankSystem**.  
2. **BankSystem** xử lý giao dịch với thông tin từ **Paycheck** và **BankInfo**.  
3. **BankSystem** trả kết quả thành công hoặc thất bại về **PayrollController**.

**Mô hình hệ thống con**:  

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWf9JObvsPbwwGd1fKd5bSKbghf92DPU2GcPUIMfHMc9oge8dI4KmM0ei0mGfgGNvnPab6WM9bSaPgSdPEWf9G3MUUMdvca05jLn08ZadiRXOWIojo1RQrEZf8PjYfP2PMv2JcfkQLrBCLSlba9gN0l8D0000__y30000)

### **2.5 Printing Subsystem**

**Mục đích**:  
- Hỗ trợ in phiếu lương cho nhân viên không sử dụng phương thức thanh toán qua ngân hàng.

**Chức năng chính**:  
- In phiếu lương dưới dạng tài liệu.  
- Giao tiếp với máy in được chỉ định để thực hiện lệnh in.

**Thành phần**:  
- **PrintService**: Xử lý việc in phiếu lương.  
- **IPrintService (interface)**: Định nghĩa các phương thức giao tiếp với hệ thống in, bao gồm:
  - `print(Paycheck, PrinterName)`: In phiếu lương cho nhân viên bằng máy in được chỉ định.

**Luồng hoạt động chính**:  
1. **PayrollController** gửi yêu cầu in phiếu lương đến **PrintService**.  
2. **PrintService** nhận dữ liệu từ đối tượng **Paycheck** và tên máy in (**PrinterName**).  
3. **PrintService** giao tiếp với máy in để thực hiện lệnh in.  
4. Sau khi hoàn tất, **PrintService** thông báo kết quả in về **PayrollController**.

**Mô hình hệ thống con**:  

 ![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWb90KMPUIMPUka9mQL9nPN59QgwIGZMNWW9GDBKeBJ4vLS4Jh2GujQWi4yW3oG510KXCeo2nCZaZDJbR1y9FBV9Bp4tL1AgevG8IoJc9nSKAvEf6jTQcHayFrIWhXSpSWfpKtDIyacAkMYw7rBmKaCS00000__y30000)
 
 
### **2.6 Security Subsystem**

**Mục đích**:  
- Đảm bảo an toàn và bảo mật cho các dữ liệu nhạy cảm trong hệ thống.  
- Quản lý xác thực người dùng và kiểm soát truy cập.  

**Chức năng chính**:  
- Kiểm tra thông tin đăng nhập của người dùng.  
- Đảm bảo bảo mật dữ liệu, bao gồm mã hóa và kiểm tra quyền truy cập.  

**Thành phần**:  
- **AuthenticationManager**: Quản lý xác thực người dùng.  
  - `validate(username, password)`: Kiểm tra thông tin đăng nhập của người dùng.  
  - `manageAccess(employeeID, resource)`: Kiểm soát quyền truy cập vào tài nguyên dựa trên vai trò người dùng.  
- **EmployeeDatabase**: Lưu trữ thông tin tài khoản và quyền của nhân viên.  

**Luồng hoạt động chính**:  
1. **LoginController** gửi yêu cầu xác thực đến **AuthenticationManager** với thông tin đăng nhập của người dùng.  
2. **AuthenticationManager** so sánh thông tin với cơ sở dữ liệu trong **EmployeeDatabase**.  
3. Nếu xác thực thành công, **AuthenticationManager** khởi tạo phiên đăng nhập cho người dùng.  
4. Nếu thất bại, trả về thông báo lỗi cho **LoginController**.  

**Mô hình hệ thống con**:  

 ![](https://www.planttext.com/api/plantuml/png/R90xRW9H34NxMOL5DKYmWHG811GKLAp0lBaaJtcVaUqND4fO6GLBoXOomoT5WWitliV7ylVvCbTZiH93rR9xvrVGQ0TNn5j7kxBNJWrnH9yLaGkiIejYRqZc7PlFQSkfP-Gwx-k3Ws_OK1U598wOKDj3nopD-9Q8Ls3X75Hhn3Ra3jYi9YJGNCHXo9r-RUjxOiN6UrRy5Iq5pN0D1wtl1hKiU72RTCZrRMNVdjy-dNxD_ejUo2U3i3EjJjKSgHcUz0C00F__0m00)
 
 

## **3. Kết luận**

Hệ thống **Payroll System** được chia thành 6 hệ thống con chính:
1. **Login Subsystem**: Quản lý đăng nhập và xác thực người dùng.  
2. **Timecard Management Subsystem**: Quản lý bảng chấm công và mã dự án.  
3. **Payroll Processing Subsystem**: Điều phối việc tính toán và xử lý thanh toán lương.  
4. **Banking Subsystem**: Thực hiện giao dịch ngân hàng.  
5. **Printing Subsystem**: Hỗ trợ in phiếu lương cho nhân viên không sử dụng phương thức thanh toán qua ngân hàng.  
6. **Security Subsystem**: Đảm bảo bảo mật cho các dữ liệu nhạy cảm và quản lý quyền truy cập.

Thiết kế các hệ thống con này không chỉ giúp hệ thống trở nên **mô-đun** mà còn đảm bảo rằng các thành phần có thể dễ dàng **mở rộng** và **bảo trì**. Các hệ thống con độc lập có thể được phát triển, kiểm thử và triển khai riêng biệt mà không làm gián đoạn các chức năng khác trong hệ thống.

Hệ thống được xây dựng trên cơ sở các **giao diện (interface)**, giúp các thành phần dễ dàng **tái sử dụng** trong các hệ thống khác hoặc mở rộng khi có yêu cầu mới. Điều này giúp giảm thiểu chi phí phát triển trong tương lai, đồng thời đảm bảo hệ thống có khả năng thay đổi linh hoạt khi cần thiết.

Các subsystem này đáp ứng các yêu cầu chức năng đã được nêu ra trong bài Lab 4, bao gồm việc xử lý lương, bảo mật thông tin người dùng, và việc giao tiếp với các hệ thống ngân hàng và hệ thống in ấn. Mỗi hệ thống con làm nhiệm vụ riêng biệt và có trách nhiệm rõ ràng, từ đó đảm bảo hệ thống vận hành ổn định và hiệu quả.

Với thiết kế này, **Payroll System** không chỉ đáp ứng được các yêu cầu hiện tại mà còn có khả năng mở rộng và thích ứng với các thay đổi trong tương lai.













