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

![]()
