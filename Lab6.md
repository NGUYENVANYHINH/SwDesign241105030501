# **Thiết kế chi tiết các lớp trong Payroll System**

## **1. Các lớp trong hệ thống**

### **1.1 Lớp BankSystem**
**Chức năng**: Thực hiện các giao dịch ngân hàng.

- **Thuộc tính**:
  - `transactionList: List<BankTransaction>` - Danh sách các giao dịch đã thực hiện.

- **Phương thức**:
  - `deposit(paycheck: Paycheck, bankInfo: BankInformation): void`  
    Thực hiện chuyển khoản dựa trên phiếu lương và thông tin ngân hàng.

- **Quan hệ**:
  - Kết hợp với **BankTransaction** và **BankInformation** để xử lý giao dịch.

---

### **1.2 Lớp PrintService**
**Chức năng**: Hỗ trợ in phiếu lương.

- **Thuộc tính**:
  - `printerName: String` - Tên máy in được chỉ định.
  - `printQueue: Queue<Paycheck>` - Hàng đợi các phiếu lương cần in.

- **Phương thức**:
  - `print(paycheck: Paycheck): void`  
    In phiếu lương trên máy in.
  - `addToQueue(paycheck: Paycheck): void`  
    Thêm phiếu lương vào hàng đợi.

- **Quan hệ**:
  - Kết hợp với **Paycheck** để tạo và in dữ liệu.

---

### **1.3 Lớp ProjectManagementDatabase**
**Chức năng**: Quản lý bảng chấm công và mã dự án.

- **Thuộc tính**:
  - `chargeNumbers: List<ChargeNum>` - Danh sách mã dự án.
  - `timecards: Map<Employee, Timecard>` - Bảng chấm công theo từng nhân viên.

- **Phương thức**:
  - `getChargeNumbers(criteria: String): List<ChargeNum>`  
    Lấy danh sách mã dự án dựa trên tiêu chí tìm kiếm.
  - `getTimecard(employee: Employee): Timecard`  
    Lấy bảng chấm công của một nhân viên.
  - `saveTimecard(timecard: Timecard): void`  
    Lưu bảng chấm công vào cơ sở dữ liệu.

- **Quan hệ**:
  - Phụ thuộc vào các lớp **ChargeNum**, **Employee**, và **Timecard**.

---

### **1.4 Lớp PayrollController**
**Chức năng**: Điều phối việc tính toán và xử lý lương.

- **Thuộc tính**:
  - `paycheckList: List<Paycheck>` - Danh sách phiếu lương đã tạo.

- **Phương thức**:
  - `runPayroll(): void`  
    Thực hiện toàn bộ quy trình tính lương và xử lý thanh toán.
  - `calculatePay(employee: Employee, timecard: Timecard): float`  
    Tính lương dựa trên bảng chấm công.
  - `generatePaycheck(employee: Employee, amount: float): Paycheck`  
    Tạo phiếu lương cho một nhân viên.

- **Quan hệ**:
  - Tương tác với **Timecard**, **Employee**, **Paycheck**, **BankSystem**, và **PrintService**.

---

### **1.5 Lớp Employee**
**Chức năng**: Đại diện cho một nhân viên.

- **Thuộc tính**:
  - `employeeID: String` - Mã số nhân viên.
  - `name: String` - Tên nhân viên.
  - `paymentMethod: String` - Phương thức thanh toán (e.g., "bank" hoặc "print").

- **Phương thức**:
  - `getPaymentMethod(): String`  
    Lấy phương thức thanh toán của nhân viên.

- **Quan hệ**:
  - Tương tác với **Timecard** và **Paycheck**.

---

### **1.6 Lớp Timecard**
**Chức năng**: Lưu trữ bảng chấm công.

- **Thuộc tính**:
  - `hoursWorked: Map<ChargeNum, float>` - Số giờ làm việc theo mã dự án.

- **Phương thức**:
  - `getTotalHours(): float`  
    Tính tổng số giờ làm việc.
  - `addHours(chargeNum: ChargeNum, hours: float): void`  
    Thêm giờ làm việc vào mã dự án.

- **Quan hệ**:
  - Kết hợp với **Employee** và **ChargeNum**.

---

## **2. Quan hệ giữa các lớp**

### **Biểu đồ lớp (Class Diagram)**

![](https://www.planttext.com/api/plantuml/png/X5HBRjim4Dth55pAW7q1mJ22E0KQe0vSs43NOsfYinP9WHmP48AUh8iUgLSeAP6Y52lfHfJclPbvyw7-_lxpO0aCDRBAU0NMiaTGrqDh2ILxonXRCJAWB70IMdqJbWhcdsjFEoPauwYCbLXhAoYleUKNvDU2xSFRafsSmxDwrKMNmRyP2TvrKR2R5cNsAmiAzaOeEg2v2Ov1G-rDQ5v0Oi4EvBxEoVwzmSQPksCT4_Q2Edn6JipfEL2MHzqvVq8SYTC_aTCE59nHeg8d83Y1ZKhv1SmPNnfvGcD3hxRHjkaRAYHoCAM3Tr2llyYwqYtYaXq3q6i_8st7mN9kXEk1WDY1nLpupYy6oZ74BbZCufmYsh4jt72WHsM9Sry_j4PNrLOhyYUQEA7GiD6AJ4TX6XLyyt7tELIygO3GWJDobsnMqskbWKAr2atltYMRZG5IDug2so9DDvKLkQ6Q6EJvQR9kwcx_eFKxi4Eww7A4T5FOZq5VT827fB6WaFIY6sD_Q7F5ij-COR3BNdcQhoQeldfwFcc6M-NUEcnXmKP1kWIf2t6menk_McrISzxPtrtRR79D9uxtE-BXOUtcuJY13-0K_CCBw6b3jV_XfMoVqWRDmwYcIHvGbVxN-Gy00F__0m00)

## **3. Biểu đồ trạng thái**
**Trạng thái của lớp Paycheck**

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWdDHQc99QWeNb0QB1QJcfMJcfIjOAGGaLkQcvfKevAQMPEIdADWgA3abvcKheQekoimhmQKSBAd41JCHh3unCmL9RN5fSd9gSN5QQGuNt2IuiQbWbI0MiZe7e6aWFm00003__mC0)

## **4. Kết luận**

Thiết kế  cung cấp chi tiết các lớp và quan hệ trong hệ thống **Payroll System**, bao gồm:  
- Các **thuộc tính** và **phương thức** của từng lớp.  
- Các mối **quan hệ** giữa các lớp, bao gồm quan hệ kết hợp và phụ thuộc.  
- **Biểu đồ lớp (Class Diagram)** mô tả rõ cấu trúc hệ thống.  
- **Biểu đồ trạng thái (State Diagram)** thể hiện các trạng thái chính của đối tượng quan trọng như **Paycheck**.

Với việc sử dụng **UML**, thiết kế trở nên:  
- **Dễ hiểu**: Mô hình hóa trực quan, rõ ràng.  
- **Rõ ràng**: Phân chia các trách nhiệm của lớp và mối quan hệ logic.  
- **Dễ triển khai**: Có thể dễ dàng chuyển đổi từ thiết kế sang mã nguồn khi thực hiện.  

Thiết kế tạo nền tảng vững chắc cho việc triển khai hệ thống, đảm bảo đáp ứng đầy đủ yêu cầu chức năng, bảo mật và khả năng mở rộng trong tương lai.

