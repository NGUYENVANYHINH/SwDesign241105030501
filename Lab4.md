# **Payroll System Design Documentation**

## **1. Giới thiệu**

Tài liệu này trình bày chi tiết thiết kế hệ thống **Payroll System**, tập trung vào các ca sử dụng chính: **Login**, **Maintain Timecard**, và **Run Payroll**. Thiết kế được xây dựng với mục tiêu đảm bảo tính mô-đun, khả năng mở rộng, và bảo mật, tuân thủ các nguyên tắc Phân tích và Thiết kế Hướng đối tượng (OOAD) với UML 2.0.

---

## **2. Các bước thực hiện**

### **2.1 Describe Interaction Among Design Objects**  
**Mô tả cách các đối tượng thiết kế tương tác để thực hiện từng ca sử dụng:**

#### **Ca sử dụng: Login**  
**Mục tiêu**: Người dùng xác thực để truy cập hệ thống.

- **Đối tượng thiết kế**:
  - **LoginForm** (boundary): Nhận thông tin đăng nhập từ người dùng.
  - **LoginController** (control): Xử lý logic xác thực.
  - **EmployeeDatabase** (entity): Lưu trữ thông tin người dùng và kiểm tra xác thực.

**Mô tả tương tác**:
- Người dùng nhập tên đăng nhập và mật khẩu vào **LoginForm**.  
- **LoginForm** gửi thông tin đến **LoginController** để kiểm tra.  
- **LoginController** tương tác với **EmployeeDatabase** để xác thực thông tin.  
- Trả kết quả xác thực về **LoginForm** để thông báo cho người dùng.

#### **Ca sử dụng: Maintain Timecard**  
**Mục tiêu**: Nhân viên quản lý bảng chấm công.

- **Đối tượng thiết kế**:
  - **TimecardForm** (boundary): Giao diện quản lý bảng chấm công.
  - **TimecardController** (control): Xử lý logic nghiệp vụ liên quan đến bảng chấm công.
  - **ProjectManagementDatabase** (entity): Lưu trữ bảng chấm công và mã dự án.

**Mô tả tương tác**:
- Nhân viên mở **TimecardForm**, hệ thống hiển thị bảng chấm công hiện tại.  
- **TimecardForm** gửi yêu cầu lấy dữ liệu đến **TimecardController**.  
- **TimecardController** truy xuất thông tin từ **ProjectManagementDatabase** và trả về **TimecardForm**.  
- Nhân viên nhập giờ làm việc mới, và các thay đổi được lưu lại qua **TimecardController**.

#### **Ca sử dụng: Run Payroll**  
**Mục tiêu**: Xử lý lương và thanh toán cho nhân viên.

- **Đối tượng thiết kế**:
  - **PayrollController** (control): Điều phối các bước trong quá trình tính lương.  
  - **Employee**, **Timecard**, **Paycheck** (entity): Cung cấp thông tin và lưu trữ kết quả tính lương.  
  - **BankSystem** và **PrinterInterface** (boundary): Xử lý thanh toán hoặc in phiếu lương.

**Mô tả tương tác**:
- **PayrollController** khởi động từ **SystemClock**, lấy thông tin bảng chấm công và nhân viên.  
- Lương được tính toán và tạo đối tượng **Paycheck**.  
- Thanh toán qua **BankSystem** hoặc in qua **PrinterInterface** dựa trên phương thức thanh toán của nhân viên.

---

### **2.2 Simplify Sequence Diagrams Using Subsystems**  

#### **Hệ thống con sử dụng**:
- **BankSystem**: Đóng gói giao tiếp với các hệ thống ngân hàng thông qua interface **IBankSystem**.
- **PrintService**: Đóng gói chức năng in thông qua interface **IPrintService**.
- **ProjectManagementDatabase**: Đóng gói dữ liệu bảng chấm công và mã dự án.

**Ví dụ biểu đồ trình tự: Run Payroll**
![](https://www.planttext.com/api/plantuml/png/Z59BJiCm4Dtx5BDq9RX05gYY1IaII9NW0bDdIgBw4pcJHSx6WYDn1SPnJH2b5LxOUkDvRzvu_Fd-iHuO8u_EAZGS8hnC0vFRs62EoWJFCLZOuII7tMHeAIhotF443wwtOI8g-BLpP30s1GlHj2HA-p3w1kC4z-YFkSGIsyNECyKwRGSqfDGF4t1xTrw_WjcrNgcpgvHVR5NmHbp0KpSaWWsXXqTfbD2qGAK1aFMdLcbfrYf05rwzNLscBZOCMZDQP98ypIUHAypoRiAC93IDJXwB_rLBR4g6amay4xUXqPc5bc7RHJ9oK1-6ZkVmHS5bK1KqcQ2BhHlOostj3o5hanqeJ_6wvkz1Lz2doBVkISsd_zEejMpfNtu1003__mC0)

### **2.3 Describe Persistence-Related Behavior**  

**Các thực thể cần được lưu trữ**:
- **Employee**: Lưu trữ thông tin cá nhân của nhân viên, bao gồm tên, số điện thoại, phương thức thanh toán, và các chi tiết liên quan khác.
- **Timecard**: Lưu trữ dữ liệu về giờ làm việc của nhân viên cho từng dự án.
- **Paycheck**: Lưu trữ thông tin về lương của nhân viên sau khi tính toán và xử lý.

#### **Cơ chế lưu trữ**:
- Hệ thống sử dụng **ObjectStore Support** hoặc **RDBMS** để lưu trữ dữ liệu.  
- **Timecard**, **Employee**, và **Paycheck** được lưu trữ vào cơ sở dữ liệu trung tâm để dễ dàng truy xuất và cập nhật.
- **ProjectManagementDatabase**: Quản lý bảng chấm công và mã dự án.

**Ví dụ hành vi lưu trữ: Timecard**
- Khi nhân viên cập nhật bảng chấm công, các thay đổi được lưu vào **ProjectManagementDatabase** thông qua **TimecardController**.

---

### **2.4 Refine the Flow of Events Description**  

#### **Flow of Events: Run Payroll**
1. **SystemClock** kiểm tra thời điểm thực thi.
2. **PayrollController** lấy danh sách nhân viên từ **Employee**.
3. Với mỗi nhân viên:
   - Lấy dữ liệu bảng chấm công từ **Timecard**.  
   - Tính toán lương dựa trên loại nhân viên (**HourlyEmployee**, **SalariedEmployee**, hoặc **CommissionedEmployee**).  
   - Tạo đối tượng **Paycheck**.
   - Dựa vào phương thức thanh toán:
     - Thanh toán qua **BankSystem**.
     - In phiếu lương qua **PrintService**.

---

### **2.5 Unify Classes and Subsystems**  
#### **Tổ chức các lớp và hệ thống con**:
- **BankSystem**:
  - Interface: **IBankSystem**.
  - Chức năng: Quản lý giao dịch ngân hàng.  

- **PrintService**:
  - Interface: **IPrintService**.
  - Chức năng: Xử lý in phiếu lương.

- **ProjectManagementDatabase**:
  - Chức năng: Lưu trữ bảng chấm công và mã dự án.  

Các lớp như **Employee**, **Timecard**, **Paycheck** được tổ chức thành nhóm theo hệ thống con tương ứng để tối ưu hóa cấu trúc thiết kế.

---

## **3. Ưu điểm của thiết kế**

1. **Tính mô-đun**: Các **subsystem** độc lập giảm độ phức tạp và dễ bảo trì.  
2. **Khả năng tái sử dụng**: Các lớp và giao diện có thể sử dụng lại trong các hệ thống khác.  
3. **Bảo mật**: Dữ liệu nhạy cảm được lưu trữ và xử lý an toàn.  
4. **Khả năng mở rộng**: Dễ dàng thêm tính năng mới nhờ sử dụng **interface** và **subsystem**.

# **Tài liệu giải thích lý do thiết kế hệ thống Payroll System**
Tài liệu này giải thích chi tiết lý do đưa ra các thiết kế cho hệ thống **Payroll System**. Các thiết kế được xây dựng dựa trên các yêu cầu chức năng, kỹ thuật và thông tin từ phân tích các ca sử dụng trong **Lab 2 (Use Case Analysis)** và **Lab 3 (Identify Design Elements)**. Mục tiêu của thiết kế là đảm bảo hệ thống dễ bảo trì, mở rộng và có khả năng tái sử dụng.

---

## **1. Nguyên tắc thiết kế**

### **1.1 Hướng đối tượng (OOAD)**

Thiết kế của hệ thống sử dụng các nguyên tắc của **Object-Oriented Analysis and Design (OOAD)**, với các khái niệm cơ bản như **class**, **interface**, và **subsystem**. Những nguyên tắc này giúp tổ chức và tách biệt các chức năng, làm cho mã nguồn dễ bảo trì và mở rộng.

**Lý do sử dụng OOAD**:
- **Modularity (Tính mô-đun)**: Giúp chia nhỏ hệ thống thành các phần độc lập, dễ quản lý và phát triển.
- **Reusability (Tính tái sử dụng)**: Các lớp và giao diện như **IBankSystem** và **IPrintService** cho phép tái sử dụng mã nguồn trong các dự án khác.

---

### **1.2 Tính mô-đun**

Hệ thống được chia thành các **subsystem** (hệ thống con) độc lập như **BankSystem**, **PrintService**, và **ProjectManagementDatabase**. Mỗi subsystem này quản lý một phần riêng biệt của hệ thống, giúp giảm độ phức tạp và tăng khả năng bảo trì.

**Lý do phân chia mô-đun**:
- **Giảm độ phức tạp**: Việc chia nhỏ hệ thống thành các subsystem giúp giảm độ phức tạp của từng phần, giúp lập trình viên dễ dàng hiểu và làm việc với các phần riêng biệt.
- **Dễ bảo trì và mở rộng**: Các subsystem có thể được sửa chữa hoặc mở rộng mà không ảnh hưởng đến các phần còn lại của hệ thống.

---

### **1.3 Khả năng tái sử dụng**

Các interface như **IBankSystem** và **IPrintService** được thiết kế để có thể tái sử dụng trong các ứng dụng khác.

**Lý do tái sử dụng**:
- **Giảm chi phí phát triển**: Các module như **IBankSystem** có thể được tái sử dụng trong các hệ thống thanh toán khác, giảm thiểu thời gian và chi phí phát triển.
- **Tính linh hoạt cao**: Các lớp và giao diện này có thể dễ dàng thay đổi hoặc mở rộng mà không làm gián đoạn các tính năng hiện tại của hệ thống.

---

### **1.4 Bảo mật và tin cậy**

Hệ thống sử dụng các biện pháp bảo mật để đảm bảo dữ liệu nhạy cảm của nhân viên, như **Employee**, **Timecard**, và **Paycheck**, được xử lý và lưu trữ an toàn. Mọi thông tin nhạy cảm được mã hóa và truy cập được kiểm soát nghiêm ngặt.

**Lý do bảo mật**:
- **Bảo vệ dữ liệu nhạy cảm**: Dữ liệu như thông tin tài khoản ngân hàng và bảng chấm công cần phải được bảo vệ tránh khỏi rủi ro bị lộ thông tin hoặc tấn công.
- **Tuân thủ quy định**: Hệ thống phải tuân thủ các quy định về bảo mật dữ liệu, đặc biệt là đối với các dữ liệu cá nhân và tài chính.

---

## **2. Giải thích thiết kế từng ca sử dụng**

### **2.1 Ca sử dụng: Login**

- **Mục tiêu**: Xác thực người dùng để truy cập hệ thống.
- **Lý do thiết kế**: 
  - **Tách biệt giao diện và logic**: Việc phân tách giữa **LoginForm** (giao diện) và **LoginController** (logic xác thực) giúp tăng khả năng mở rộng và bảo trì hệ thống. Nếu cần thay đổi phương thức xác thực (ví dụ: thêm xác thực hai lớp), chỉ cần thay đổi trong **LoginController** mà không cần tác động đến giao diện người dùng.
  
### **2.2 Ca sử dụng: Maintain Timecard**

- **Mục tiêu**: Nhân viên có thể quản lý giờ làm việc của mình.
- **Lý do thiết kế**: 
  - **Chia nhỏ logic nghiệp vụ**: **TimecardController** quản lý toàn bộ logic nghiệp vụ, giảm bớt sự phức tạp cho **TimecardForm**. Giao diện người dùng chỉ cần hiển thị và nhận dữ liệu, trong khi tất cả xử lý nghiệp vụ được chuyển giao cho controller.

### **2.3 Ca sử dụng: Run Payroll**

- **Mục tiêu**: Tính toán và xử lý thanh toán cho nhân viên.
- **Lý do thiết kế**: 
  - **Tách biệt các phương thức thanh toán**: Phương thức thanh toán có thể thay đổi mà không ảnh hưởng đến các chức năng khác của hệ thống, nhờ vào việc sử dụng các interface như **IBankSystem** và **IPrintService**. Điều này giúp dễ dàng thay đổi hoặc bổ sung phương thức thanh toán trong tương lai (ví dụ, thêm hình thức thanh toán qua ví điện tử).
  
---

## **3. Ưu điểm của thiết kế**

1. **Tính mô-đun**: Việc phân chia thành các **subsystem** giúp giảm độ phức tạp của hệ thống và làm cho việc bảo trì trở nên dễ dàng hơn.
2. **Khả năng mở rộng**: Hệ thống được thiết kế để có thể dễ dàng mở rộng trong tương lai mà không ảnh hưởng đến các tính năng hiện tại. Các **interface** như **IBankSystem** và **IPrintService** cho phép mở rộng thêm các phương thức thanh toán hoặc in ấn mà không thay đổi logic chính của hệ thống.
3. **Bảo mật**: Hệ thống đảm bảo an toàn và bảo mật cho các thông tin nhạy cảm của nhân viên, tuân thủ các tiêu chuẩn bảo mật hiện hành.
4. **Tái sử dụng**: Các module có thể tái sử dụng trong các hệ thống khác, giảm thiểu chi phí phát triển và tăng tính linh hoạt của hệ thống.

---

## **4. Kết luận**
Thiết kế hệ thống **Payroll System** dựa trên phân tích và các nguyên tắc hướng đối tượng, đảm bảo tính linh hoạt, dễ bảo trì, và sẵn sàng mở rộng trong tương lai. Hệ thống đáp ứng nhu cầu quản lý tiền lương và tối ưu hóa hiệu quả hoạt động.

Thiết kế hệ thống **Payroll System** sử dụng các nguyên tắc hướng đối tượng (OOAD) để đảm bảo tính mô-đun, bảo mật, khả năng tái sử dụng và mở rộng. Hệ thống đáp ứng đầy đủ yêu cầu quản lý tiền lương, dễ bảo trì và có thể mở rộng trong tương lai. Các thiết kế được áp dụng giúp tối ưu hóa hiệu suất và giảm thiểu sự phức tạp trong quá trình phát triển và bảo trì hệ thống.

---
