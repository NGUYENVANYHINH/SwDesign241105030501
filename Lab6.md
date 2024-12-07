# **Thiết kế chi tiết các lớp trong Payroll System**

## **1. Xác định  các operations và methods**

### **1.1 Operations và methods chính**

#### **Lớp BankSystem**
- **Chức năng**: Thực hiện các giao dịch ngân hàng cho phiếu lương.
- **Methods**:
  - `deposit(paycheck: Paycheck, bankInfo: BankInformation): void`  
    Chuyển khoản phiếu lương vào tài khoản ngân hàng của nhân viên.

#### **Lớp PrintService**
- **Chức năng**: Hỗ trợ in phiếu lương.
- **Methods**:
  - `print(paycheck: Paycheck): void`  
    In phiếu lương cho nhân viên.
  - `addToQueue(paycheck: Paycheck): void`  
    Thêm phiếu lương vào hàng đợi để xử lý in.

#### **Lớp ProjectManagementDatabase**
- **Chức năng**: Quản lý bảng chấm công và mã dự án.
- **Methods**:
  - `getChargeNumbers(criteria: String): List<ChargeNum>`  
    Lấy danh sách mã dự án phù hợp với tiêu chí tìm kiếm.
  - `getTimecard(employee: Employee): Timecard`  
    Truy xuất bảng chấm công của một nhân viên.
  - `saveTimecard(timecard: Timecard): void`  
    Lưu bảng chấm công sau khi chỉnh sửa.

#### **Lớp PayrollController**
- **Chức năng**: Điều phối việc tính toán lương và xử lý thanh toán.
- **Methods**:
  - `runPayroll(): void`  
    Thực hiện quy trình tính lương.
  - `calculatePay(employee: Employee, timecard: Timecard): float`  
    Tính toán lương dựa trên bảng chấm công và thông tin nhân viên.
  - `generatePaycheck(employee: Employee, amount: float): Paycheck`  
    Tạo phiếu lương cho nhân viên.

#### **Lớp Employee**
- **Chức năng**: Quản lý thông tin cá nhân và phương thức thanh toán của nhân viên.
- **Methods**:
  - `getPaymentMethod(): String`  
    Trả về phương thức thanh toán của nhân viên (e.g., "bank" hoặc "print").

#### **Lớp Timecard**
- **Chức năng**: Lưu trữ và quản lý giờ làm việc theo mã dự án.
- **Methods**:
  - `getTotalHours(): float`  
    Tính tổng số giờ làm việc từ tất cả các dự án.
  - `addHours(chargeNum: ChargeNum, hours: float): void`  
    Thêm số giờ làm việc vào mã dự án tương ứng.

---

## **2. Xác định đúng các trạng thái và mô tả sự thay đổi trạng thái**

### **2.1 Lớp Paycheck**
**Trạng thái chính**:
1. **Created**: Phiếu lương vừa được tạo.
2. **Pending**: Phiếu lương đang chờ xử lý thanh toán qua ngân hàng.
3. **Paid**: Thanh toán thành công qua ngân hàng.
4. **Printing**: Phiếu lương được gửi đến hệ thống in.
5. **Printed**: Phiếu lương đã in thành công.

**Biểu đồ trạng thái**:

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWdDHQc99QWeNb0QB1QJcfMJcfIjOAGGaLkQcvfKevAQMPEIdADWgA3abvcKheQekoimhmQKSBAd41JCHh3unCmMeDgGeCQyuCRaaCpzFeRWqEJcrk3YjD8SBRXhSw5IGQZ0BMPq3q4IWFm00003__mC0)
### **2.2 Lớp Timecard**
**Trạng thái chính**:
1. **Initialized**: Bảng chấm công vừa được tạo.
2. **InProgress**: Nhân viên đang nhập giờ làm việc.
3. **Submitted**: Bảng chấm công đã được gửi để lưu vào hệ thống.

**Mô tả sự thay đổi trạng thái**:
- **Initialized → InProgress**: Khi nhân viên bắt đầu nhập giờ làm việc vào bảng chấm công.
- **InProgress → Submitted**: Khi nhân viên hoàn tất nhập liệu và gửi bảng chấm công để lưu vào hệ thống.

**Biểu đồ trạng thái**:

![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWcTUPabcOavcLMeA5n8RAXTGb9zUb5fSh62bu9fRa9DVcPgga9YIKgoGaLzQLCo5f02aFhWqAJUpf0IesqeX93CtDJcnA4MXEB4CQBH3QbuAo5e00000__y30000)


---

## **3. Xác định đúng các thuộc tính và mô tả rõ ràng**

### **3.1 Các thuộc tính chính**

#### **Lớp BankSystem**
- `transactionList: List<BankTransaction>` - Danh sách các giao dịch đã thực hiện.

#### **Lớp PrintService**
- `printerName: String` - Tên máy in được chỉ định.  
- `printQueue: Queue<Paycheck>` - Hàng đợi các phiếu lương cần in.  

#### **Lớp ProjectManagementDatabase**
- `chargeNumbers: List<ChargeNum>` - Danh sách mã dự án.  
- `timecards: Map<Employee, Timecard>` - Bảng chấm công của từng nhân viên.  

#### **Lớp PayrollController**
- `paycheckList: List<Paycheck>` - Danh sách phiếu lương đã tạo.  

#### **Lớp Employee**
- `employeeID: String` - Mã số nhân viên.  
- `name: String` - Tên nhân viên.  
- `paymentMethod: String` - Phương thức thanh toán của nhân viên.  

#### **Lớp Timecard**
- `hoursWorked: Map<ChargeNum, float>` - Số giờ làm việc theo mã dự án.  

---

## **4. Xác định đúng các phụ thuộc và quan hệ kết hợp**

### **4.1 Quan hệ kết hợp**
- **PayrollController** kết hợp với **BankSystem** và **PrintService** để xử lý thanh toán và in phiếu lương.  
- **PayrollController** sử dụng **Timecard** và **Employee** để tính toán lương.  
- **Timecard** kết hợp với **ChargeNum** để lưu thông tin giờ làm việc theo mã dự án.  

### **4.2 Quan hệ phụ thuộc**
- **PayrollController** phụ thuộc vào **ProjectManagementDatabase** để lấy thông tin bảng chấm công và mã dự án.  
- **PrintService** phụ thuộc vào **Paycheck** để xử lý in.  
- **BankSystem** phụ thuộc vào **BankInformation** để xử lý giao dịch.  

---

## **5. Biểu đồ lớp (Class Diagram)**

![](https://www.planttext.com/api/plantuml/png/X5HBRjim4Dth55pAW7q1mJ22E0KQe0vSs43NOsfYinP9WHmP48AUh8iUgLSeAP6Y52lfHfJclPbvyw7-_lxpO0aCDRBAU0NMiaTGrqDh2ILxonXRCJAWB70IMdqJbWhcdsjFEoPauwYCbLXhAoYleUKNvDU2xSFRafsSmxDwrKMNmRyP2TvrKR2R5cNsAmiAzaOeEg2v2Ov1G-rDQ5v0Oi4EvBxEoVwzmSQPksCT4_Q2Edn6JipfEL2MHzqvVq8SYTC_aTCE59nHeg8d83Y1ZKhv1SmPNnfvGcD3hxRHjkaRAYHoCAM3Tr2llyYwqYtYaXq3q6i_8st7mN9kXEk1WDY1nLpupYy6oZ74BbZCufmYsh4jt72WHsM9Sry_j4PNrLOhyYUQEA7GiD6AJ4TX6XLyyt7tELIygO3GWJDobsnMqskbWKAr2atltYMRZG5IDug2so9DDvKLkQ6Q6EJvQR9kwcx_eFKxi4Eww7A4T5FOZq5VT827fB6WaFIY6sD_Q7F5ij-COR3BNdcQhoQeldfwFcc6M-NUEcnXmKP1kWIf2t6menk_McrISzxPtrtRR79D9uxtE-BXOUtcuJY13-0K_CCBw6b3jV_XfMoVqWRDmwYcIHvGbVxN-Gy00F__0m00)



