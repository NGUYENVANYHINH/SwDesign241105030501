
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
  ### Biểu đồ phân tích

   ![](https://www.planttext.com/api/plantuml/png/b5BBQiCm4BphAnQVqj8SUZN1X3Q55feIIA7djRKuRlG8aXmmfL_MGp-flr0faModBwWEHjx7xCoiFjxUvzQXSQqKp6uR1KPROfL0Q-56xeJkYE25WJzJK2WfXxKpZQfZY6BD7Jz905I6qD5Z8wb2moU78GiVoI5yBu0K7txFSaYLiTssfMnSt-xYPQZpBNlTSFRA8jkKwDb-6Pa8Z-V6s4QtnZvfioK_O8cxsP7YGhUbe2B17HYvK7AbjI1KaIfoVXi09dmaxm2PHuZ4TInjyat02ZkZXLXtrf6CAW1g6bn8PkVzQdum3lVq7zjMHZzJvPQei2P9AZY69LeQCxZUeAdfePKbUPqUuxwnRdRSTn6m-gUINMOmdHQGdMS3irDb8Vr7Aa6nVg4X-YjDnkP-fU7vVW800F__0m00)

  ### Biểu đồ tuần tự (Sequence Diagram) cho Maintain Timecard
    
 ![](https://www.planttext.com/api/plantuml/png/Z59BJiGm3Dtd5DRivm9Te5d04Wa9Bk0cLXicds8xC-hPM70aha0AAf11Kx7s-_dPxwzl1r5aBJ4OEVe4d8KCMiqCTt4AUIOoKmLuwoTC2WyuSmxXSHQbs4oUV2IBx5euvsUoUey91ugKz1OLUwmUPfM7_KshsW7JIo5Hq5MocI-4rQm3ouHAKFCoANiwqGRjQfmE1bAm8_90a4hiYSLSHSF-R-QM2y6BNlfNqhfq1pBcytTImEGktPk2VlP5vs3CfLgSCn_9RVKefO_-VpLANRz-WXO1pR3xOYgvtHRfXC6xfVtFG9lo-Fikva39BI_t0G00__y30000)

    
### 2. Run Payroll
### Tác nhân liên quan:
+System Clock

+Bank System

+Payroll Administrator

### Mô tả:
Chạy quá trình tính lương định kỳ vào mỗi thứ Sáu và ngày làm việc cuối tháng, trả lương cho nhân viên dựa trên dữ liệu thời gian làm việc và các quy định về mức lương, hoa hồng (nếu có).

### Quy trình:
Hệ thống được kích hoạt vào ngày chạy lương.-->
Hệ thống lấy danh sách nhân viên cần thanh toán cho kỳ hiện tại
#### Đối với từng nhân viên:
Tính lương dựa trên thẻ chấm công, dữ liệu mức lương và các khấu trừ.-->
Nếu có phương thức thanh toán là chuyển khoản, hệ thống tạo giao dịch và gửi đến hệ thống ngân hàng.-->
Nếu phương thức thanh toán là gửi qua bưu điện hoặc lấy tại văn phòng, hệ thống in phiếu lương.-->
Lưu các giao dịch và trạng thái thanh toán cho nhân viên

### Biểu đồ lớp phân tích:

PayrollSystem: Quản lý quá trình tính lương, tạo và gửi giao dịch thanh toán.

Payment: Lưu thông tin giao dịch, bao gồm phương thức thanh toán, ngày thanh toán, trạng thái.

BankSystem: Xử lý các giao dịch qua ngân hàng.

![](https://www.planttext.com/api/plantuml/png/R5BBQiCm4BphA_ReGlm3feHGN6WEWK0AFQlIDZ7Hm-XHCALVraC_gRzGgLtvaSGtxypEpExgv-jxumDt8Mh5_BapuAn79XJt7Xvrh-o021yCqbS3Kc4h6pW4rvaZ0JqVD9gmmt2oImpWYA48RSsRhUuQcF-pJqPspvr6mPqSxKusElzYtHcJvextzoqFk8BMnbU5wqd-QU9bzMlcQB7dWxDA7GOVK9CFW8k6WDp-RZj9WE1AH9Ma4boLuQVuYIp_78ZUEolG-_t_Ccuqh81h6qqeVSLjdY-tZXjOqgaeKw06yeHKI0SCqL-idS9KLnuFt9ml5a3SjdCeGekzzLsewAPD2JKJ6Xz6NQ_7ix7bSZDKU3SW4cLbuboRaZ6sGIFpc_m5003__mC0)

### Biểu đồ tuần tự 
![](https://www.planttext.com/api/plantuml/png/V59BJiGm3Dtd5Bx0NA0BD6B47Wak42LcnceIHuwBrBEnu4XSOT9E2YrJo2fwVX_RyjV7vx6e5HrYCAMd1C85ZNNA0YzZKOodmAutkNB8KRP9uTcEmY7SoflAKyo1HyGD-4eHdHN_soDYqWtsQ5FVJCqg6muFsyWELEXyHe5yWyscFF6NHZeGh6HyHy065L2UXFUYfT6LI1i4RpodGKOXzly5EXlS4ApYVaWRlF846sbUX0sw_26YNjW35V0aw1GyPYwa1kfh1fFNpy8woC8Eovq2Gy4TtsWfm3GIkVumvCNuZrQpK9gxSnUiju1fPm7Vv27xrLnGhqk7OionggOZkm800F__0m00)
### 3. Maintain Employee Information
### Tác nhân liên quan: 

+Payroll Administrator

### Mô tả:
+Quản trị viên lương quản lý thông tin nhân viên, bao gồm thêm, chỉnh sửa và xóa thông tin nhân viên.

### Quy trình:
Quản trị viên chọn chức năng quản lý thông tin nhân viên.-->
Hệ thống yêu cầu nhập mã nhân viên và chức năng cụ thể (thêm, cập nhật hoặc xóa):

Thêm: Hệ thống yêu cầu nhập thông tin chi tiết nhân viên như họ tên, địa chỉ, loại hợp đồng, phương thức thanh toán, mức lương, và các khấu trừ.

Cập nhật: Hệ thống lấy thông tin nhân viên từ mã và cho phép chỉnh sửa các trường dữ liệu.

Xóa: Hệ thống xác nhận và đánh dấu xóa nhân viên, lưu lại cho lần chạy lương tiếp theo.

--> Hệ thống lưu lại thay đổi và cập nhật vào cơ sở dữ liệu.

### Biểu đồ lớp phân tích:
+Employee: Lưu trữ thông tin nhân viên.

+Payroll Administrator: Tác nhân có quyền truy cập và thay đổi thông tin nhân viên.
![](https://www.planttext.com/api/plantuml/png/V59BJiGm3Dtd5Bx0NA0BD6B47Wak42LcnceIHuwBrBEnu4XSOT9E2YrJo2fwVX_RyjV7vx6e5HrYCAMd1C85ZNNA0YzZKOodmAutkNB8KRP9uTcEmY7SoflAKyo1HyGD-4eHdHN_soDYqWtsQ5FVJCqg6muFsyWELEXyHe5yWyscFF6NHZeGh6HyHy065L2UXFUYfT6LI1i4RpodGKOXzly5EXlS4ApYVaWRlF846sbUX0sw_26YNjW35V0aw1GyPYwa1kfh1fFNpy8woC8Eovq2Gy4TtsWfm3GIkVumvCNuZrQpK9gxSnUiju1fPm7Vv27xrLnGhqk7OionggOZkm800F__0m00)
### Biểu đồ tuần tự 
![](https://www.planttext.com/api/plantuml/png/d99DJWCn38NtFaMMi43Tiq2j17ian06inADQpS_8yRIQix7WI5m1DyDeMccGe5bauVXxxpd9ryVdjYgA3Yb2FN1sKYe1UYtYNd6K4kCk9CvSLT2Aq5ipU-unwzpmDbQbT7NoalfOHYA0DH7ty7JDFZg_BsRikY5xvPBTtIw4pNiVK6dpJ96KxW6ZEYiluixM7_NHEFhX7EUkNC9JqvcQfIsGa7cxJAU54_950b2qf5Escx8C4_glE48gJCSBAf0Ynzh0kUztinFhlWtJpDe4qxNUD46OK5f1ry8dbCCIl3F99c3l39G3mDRsymVy1W00__y30000)
### 4. Create Reports
### Tác nhân liên quan:
+Employee

+Payroll Administrator

### Mô tả:
+Nhân viên và quản trị viên có thể tạo báo cáo về giờ làm việc, lương nhận được, và các thông tin liên quan đến dự án hoặc ngày nghỉ.

### Quy trình:
Tác nhân chọn chức năng báo cáo.-->
Hệ thống yêu cầu nhập các tiêu chí báo cáo như loại báo cáo (giờ làm việc, lương, số giờ làm việc trên dự án, nghỉ phép) và khoảng thời gian.-->
Nếu báo cáo liên quan đến dự án, hệ thống truy cập vào cơ sở dữ liệu dự án để lấy mã số dự án.-->
Hệ thống tạo báo cáo theo yêu cầu.-->
Tác nhân có thể chọn lưu hoặc chỉ xem báo cáo.-->
### Biểu đồ lớp phân tích:
+Report: Lưu trữ thông tin về báo cáo như loại, thời gian, nội dung chi tiết.

+Employee và Payroll Administrator liên kết với Report để xem hoặc tạo báo cáo.
![](https://www.planttext.com/api/plantuml/png/h95D3i8W48Ntd6AMDMalq8MfYUwDUW7IJXeYXMOOJOZnP2uyabUGKlohBcK16HxplWVSBjVAiIG-T5gulJ90rg6ejNGELbslhKU4au0uQaB9kC7U4cSKbvtliOGjap9j3j5g6SwKCCmve6bUvQo4iLUSHKAifIUhzQBfb56EIRAb2Ivg_sIETQ8KyEsPX8bnslrmJq5RD1YYOnPeHwkQWVLylAAOFoBylEsRBghWFlp47G00__y30000)
### Biểu đồ tuần tự 
![](https://www.planttext.com/api/plantuml/png/V94n3i8m34NtdC8ZIC01Eg0o835Mm0MYnaA1D0cEC_Hi31o9Av2e15IfPOfil_zaAw_7imuiYMDdHBXf2-G22jco8zXtthWUIzd8dfmnEzLfgmEJJ4tXKrQtsalB1JZrWR4RJOxe7R4GnGZhxPYkWF0UCN1wCmgBisDfuE0YXHKqvAxOSYcHsyrIJEtpHompzz6B4PD3muOLND1YCc41X_wabYFPBwzcp2bOZgv0wU2DxEVHgPD-iT45eaQhyg-z0G00__y30000)
### 5. Select Payment Method
### Tác nhân liên quan:
+Employee
#### Mô tả:
+Nhân viên lựa chọn phương thức thanh toán lương theo sở thích (lấy trực tiếp, gửi qua bưu điện hoặc chuyển khoản ngân hàng).

#### Quy trình:
Nhân viên chọn chức năng thay đổi phương thức thanh toán.-->
Hệ thống yêu cầu nhân viên chọn một trong ba phương thức:

--> Lấy trực tiếp: Không yêu cầu thêm thông tin.

--> Gửi qua bưu điện: Yêu cầu địa chỉ nhận.

--> Chuyển khoản ngân hàng: Yêu cầu tên ngân hàng và số tài khoản.

Hệ thống cập nhật phương thức thanh toán vào hồ sơ nhân viên.

### Biểu đồ lớp phân tích:
+Employee: Lưu trữ phương thức thanh toán.

+BankSystem: Liên kết với Employee khi lựa chọn phương thức thanh toán là chuyển khoản.
![](https://www.planttext.com/api/plantuml/png/R91D2i9038NtSuei5PmBT25Lwj8YU8BfDEZG-IcJL2ZYoLnu9A_W-4DfrMm2oUDxBxbVRpcnYjmvAwWn7c8W5Deg8jYureOU4Su2KabeLU_GynRv6EeCzXoDFxns08GMDU_6YfcR2ESPd8AfnKLy-6lbcvNMeVCyM5HfLYg74xe4zPQLdQim_ZXpOM8oBx0DP59ZPIpDlb6B_vHHhE5WAPVZT4BawEldYnu0003__mC0)
### Biểu đồ tuần tự 
![](https://www.planttext.com/api/plantuml/png/Z94zZW8n38Lxdy8bI7012WGhRRyI9p29LqIJFyMUOiwsnHw9A-0CEn8ZKMmA5ydxtelj-y_lIPIQZYc2325ZAy90Jal3prHZcPYXcY2uK2ahVj7KIeoNIPJJwkM3yd1shenP0HOMzySrSa3Xo4wnqfJOiCHwAnutDRXXFzOT9WfnXpwqhl9SYmJT0aL3dX90EolJdh8a7j2L_1rQMkH_2S1HU3R_Bz-rIDut5ddIwq-zztaPG-zLyMeNXgYvoOoyADwCPqcVCUEjNyuUu6IrR-a1003__mC0)
### 6. Maintain Purchase Order
### Tác nhân liên quan:
+CommissionedEmployee: Nhân viên nhận hoa hồng, người có thể tạo, cập nhật và xóa các đơn hàng mua.

### Mô tả:
+Nhân viên nhận hoa hồng có thể tạo mới, cập nhật, hoặc xóa đơn hàng mua của mình. Đơn hàng mua lưu thông tin về khách hàng, địa chỉ thanh toán, sản phẩm và ngày mua. Các đơn hàng này sẽ được lưu trữ trong hệ thống và có thể được truy xuất để tính toán hoa hồng cho nhân viên.

### Quy trình:
#### Tạo mới đơn hàng mua:
Nhân viên chọn chức năng "Create Purchase Order".-->
Hệ thống hiển thị form để nhập thông tin đơn hàng mua.-->
Nhân viên nhập các chi tiết cần thiết, bao gồm: người liên hệ khách hàng, địa chỉ thanh toán, sản phẩm mua, và ngày mua.-->
Hệ thống tạo và lưu lại một đơn hàng mua mới với ID duy nhất.-->

#### Cập nhật đơn hàng mua:
Nhân viên chọn chức năng "Update Purchase Order".-->
Hệ thống yêu cầu mã đơn hàng để truy xuất đơn hàng cần cập nhật.-->
Nhân viên chỉnh sửa các thông tin cần thiết của đơn hàng (ví dụ: thay đổi sản phẩm, ngày mua).-->
Hệ thống lưu lại các thay đổi.-->
#### Xóa đơn hàng mua:

Nhân viên chọn chức năng "Delete Purchase Order".-->
Hệ thống yêu cầu mã đơn hàng để xác định đơn hàng cần xóa.-->
Hệ thống yêu cầu nhân viên xác nhận xóa đơn hàng.-->
Khi nhân viên xác nhận, hệ thống đánh dấu đơn hàng đã bị xóa và không còn có thể chỉnh sửa hay truy xuất trong tương lai.
### Biểu đồ lớp phân tích:
+PurchaseOrder: Lưu trữ thông tin đơn hàng, bao gồm mã đơn hàng, người liên hệ khách hàng, địa chỉ thanh toán, sản phẩm và ngày mua.

+CommissionedEmployee: Liên kết với nhiều PurchaseOrder (1-n), cho phép nhân viên tạo, cập nhật và xóa các đơn hàng của mình.

+PayrollSystem: Quản lý lưu trữ và xử lý đơn hàng mua, bao gồm chức năng truy xuất, cập nhật và xóa đơn hàng trong hệ thống.
![](https://www.planttext.com/api/plantuml/png/b5DBJiCm4Dtd5AEi2Y8BjX6gYbeMI4XKz0HkPWGMTXpDs9KYnCbOS2IkGD8ufGuL7oyiUTwycNdFziVR-qAyOX-ioUHPry1EAAkC4e6birQBQ5SJtjZ6k9O8NZBeLW4K0xTOmiQphXyZK1rO3yfJ2UZ2rj0U1AYOkk0wSFMaXEuPYMUktqj8WcSbx9p6o0eDdcPzDRy09A-qaHyB8HdwfT18UCsY2qdsGVw4DMeFufqbNhhQgyfFqAqsfZjT8pA9JC267ORAhqOLTrhyrP0nF-wvsflQxr6JGbmFt5ciCPLoREAW-UzU3VdVJL4jEsCshNYoqHG0KRj_torJDokTv2MNak3z82TVPtwPGr7C8J_F9unquZudnRC5rTZ_Way0003__mC0)
### Biểu đồ tuần tự 
![](https://www.planttext.com/api/plantuml/png/f99DJWCn38NtFeMNi43Tiq15m1ean06YnDL4pPyS3zMShOiUYIlW9XHrgY8Lo68KUTxxdfzcFhQxPHN3CiO0TUqJSgu4nafcVCWn-bfzJkIUOWbv8eAYOczzCKdmnKoSGtYTgb2SlndP3gRICpjYW7CalBcR0sxH3bdJKTDLYLVtpYtUYZD2YqSA9FIDnSQz1XC4LNKo1zHpOQHHTpcuyzwDFgroGyoapNlSIjTbqjqmqUOKmMJr0XHqqXlyOyMn0_ww9PEmf_U3pv4O7sgt7Yj_Jjvu6LhBbjbAdVqUlodbEc1Uwg8-qV3wgyigSmTf6b1o04jzxd_bJm000F__0m00)

## Code Java mô phỏng ca sử dụng Maintain Timecard.

import java.util.ArrayList;

import java.util.Date;

import java.util.HashMap;

import java.util.Map;

class Timecard {

    private Date startDate;
    private Date endDate;
    private Map<Date, Double> hoursWorked = new HashMap<>();
    private boolean submitted;

    public Timecard(Date startDate, Date endDate) {
        this.startDate = startDate;
        this.endDate = endDate;
        this.submitted = false;
    }

    public void addHours(Date date, double hours) throws Exception {
        if (submitted) {
            throw new Exception("Cannot modify submitted timecard.");
        }
        if (hours < 0 || hours > 24) {
            throw new IllegalArgumentException("Invalid hours");
        }
        hoursWorked.put(date, hours);
    }

    public void submit() {
        this.submitted = true;
    }

    public boolean isSubmitted() {
        return submitted;
    }

    @Override
    public String toString() {
        return "Timecard{" +
                "startDate=" + startDate +
                ", endDate=" + endDate +
                ", hoursWorked=" + hoursWorked +
                ", submitted=" + submitted +
                '}';
    }
}

class Employee {
    private String name;
    private ArrayList<Timecard> timecards = new ArrayList<>();

    public Employee(String name) {
        this.name = name;
    }

    public Timecard createTimecard(Date startDate, Date endDate) {
        Timecard timecard = new Timecard(startDate, endDate);
        timecards.add(timecard);
        return timecard;
    }

    public void submitTimecard(Timecard timecard) {
        timecard.submit();
    }

    public ArrayList<Timecard> getTimecards() {
        return timecards;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", timecards=" + timecards +
                '}';
    }
}

public class PayrollSystem {

    public static void main(String[] args) {
        try {
            Employee employee = new Employee("John Doe");
            Date startDate = new Date(); // giả định ngày hiện tại làm ngày bắt đầu
            Date endDate = new Date(); // giả định ngày kết thúc

            Timecard timecard = employee.createTimecard(startDate, endDate);
            timecard.addHours(startDate, 8.0); // thêm 8 giờ làm cho ngày bắt đầu

            System.out.println("Timecard before submission: " + timecard);
            employee.submitTimecard(timecard); // gửi thẻ chấm công
            System.out.println("Timecard after submission: " + timecard);
        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
