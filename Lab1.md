# Phân Tích Kiến Trúc Microservices (MNV)

## Đề Xuất Kiến Trúc

Microservices sẽ chia hệ thống thành các dịch vụ độc lập, mỗi dịch vụ có một chức năng chuyên biệt như:

- **User Service**: Quản lý thông tin người dùng và quyền truy cập.
- **Payroll Service**: Tính toán và xử lý bảng lương.
- **Timecard Service**: Quản lý thông tin chấm công của nhân viên.
- **Payment Service**: Thực hiện xử lý thanh toán tự động cho nhân viên.

## Lý Do Lựa Chọn

- **Scalability**: Microservices cho phép mở rộng các thành phần riêng lẻ mà không ảnh hưởng đến toàn bộ hệ thống.
- **Decoupling**: Các dịch vụ tách biệt giúp dễ bảo trì và cập nhật tính năng mà không ảnh hưởng đến hệ thống.
- **Flexibility in Technology**: Có thể chọn công nghệ khác nhau cho từng microservice tùy thuộc vào yêu cầu của nó.

## Biểu Đồ Package cho Microservices

![diagram](https://www.planttext.com/api/plantuml/png/X5AzJW916EplARvSOyKBM1XG35gG49HO2CMwREusBD_2_gXeh2riz16CbPqrn510U8zx0b_1NUuWYm7SufATcszclid-JAPbROWojY-Y0vY_PfCNJ06JTFv9eCUpyHJ1gDcOGfrJ9JLJjvmo3JILa6QJPp3k-uO936qs_a0GisyGYw_5EoPHD22qHn86SQLn3ZLYs1qPnV0OWJlN0TQ9dWBoHU6nPhQSAnHe1qgbeyrXE8IuAQrngHGRMgQDZlF11XafASIUsPntoVkC4jNzb-W4-mpDFbwuIPKOSaFqtrMgnvtDV6jW7IIaB1qzuAItTR7Iz3tK2Nfd3xMnOatgPZabXalCxrBnX-KrZdRK4uJoYYT4K2lSTb3yQ6ED8LC5eWKVEAaT3ORx1F5Mi6vZQz3rIbTIzU1CMgNpN5jQ3fhmKgVtZDeyWuVRM6YlQ4r6fNE8epB3hd_Tlm000F__0m00)

---

# Cơ Chế Phân Tích

## Danh Sách Các Cơ Chế Cần Thiết và Lý Do Lựa Chọn

### Access Control (Kiểm Soát Truy Cập)

- **Lý do**: Đảm bảo an toàn dữ liệu lương và chấm công. Vì hệ thống lưu trữ thông tin nhạy cảm về nhân viên và lương, nên cần cơ chế xác thực (authentication) và phân quyền (authorization) mạnh mẽ. Điều này giúp đảm bảo chỉ người dùng được ủy quyền mới có quyền truy cập vào các thông tin quan trọng.
- **Áp dụng**: Được thực hiện trong User Service để xác thực và phân quyền cho tất cả các dịch vụ khác qua API Gateway.

### Payroll Calculation (Tính Toán Lương)

- **Lý do**: Đảm bảo tính chính xác và nhất quán trong tính toán lương cho nhân viên, dựa trên giờ làm và các yếu tố bổ sung như thuế và phụ cấp.
- **Áp dụng**: Xây dựng trong Payroll Service để xử lý toàn bộ nghiệp vụ tính toán lương, từ bảng lương hàng tháng đến tạo phiếu lương cá nhân.

### Timecard Management (Quản Lý Bảng Chấm Công)

- **Lý do**: Hỗ trợ theo dõi thời gian làm việc của nhân viên nhằm cung cấp dữ liệu đầu vào cho việc tính toán lương.
- **Áp dụng**: Tạo một Timecard Service quản lý và cập nhật giờ làm của nhân viên, dữ liệu này được chuyển đến Payroll Service để tính lương.

### Automated Payments (Thanh Toán Tự Động)

- **Lý do**: Tự động hóa quá trình thanh toán giúp giảm thiểu thời gian xử lý và lỗi thủ công trong quá trình chuyển khoản lương.
- **Áp dụng**: Được tích hợp trong Payment Service để thực hiện thanh toán cho nhân viên, sử dụng dữ liệu từ Payroll Service.

### Integration with Legacy Systems (Tích Hợp Với Hệ Thống Cũ)

- **Lý do**: Cho phép hệ thống mới có thể tương tác và đồng bộ dữ liệu với các hệ thống quản lý lương hiện có (nếu có), đảm bảo quá trình chuyển đổi diễn ra suôn sẻ mà không làm gián đoạn hoạt động.
- **Áp dụng**: Cần tích hợp một cơ chế trong API Gateway hoặc các dịch vụ liên quan để xử lý các yêu cầu từ các hệ thống cũ, đảm bảo không ảnh hưởng đến hiệu suất của các microservice hiện tại.

---

# Phân Tích Ca Sử Dụng Payment

## Mô Tả Hành Vi Thông Qua Biểu Đồ Sequence

![diagram](https://www.planttext.com/api/plantuml/png/P951Zi8m34NtEON5dWjqWM0g5kog6N40A_L8rgH9I5oadeq5H-8AasQQ3e5TOZzzFoUFstqV1OECWr6enGKu3jwuYKZvL6RD7gt0fiCfE6FWYyALDMq08oorDt2WT7W1vreDVg3zWKDtoiHyKQgCXkskX4C3dtGPAGfudA9XhqgdWbeqUZGeD6FPgiQoKvEiR5y8w55GbLx2ib439yl2IrBMplLjbTCw-yrXM94rfP8w-_x92D93onZ_nHAxRjn05zoLUofh0YPJ_JS6XPrL--G-VzCl0000__y30000)

## Các Lớp Phân Tích Cho Ca Sử Dụng "Payment"

### PayrollService

- **Nhiệm vụ**: Tính toán tổng lương cho nhân viên dựa trên dữ liệu chấm công và các khoản bổ sung hoặc khấu trừ.
- **Thuộc tính chính**:
  - `employeeId: String`
  - `baseSalary: Double`
  - `deductions: Double`
  - `bonuses: Double`
- **Phương thức**:
  - `calculatePayroll()`: Tính toán tổng lương cho từng nhân viên.
  - `getPayrollData()`: Lấy dữ liệu để gửi đến PaymentService.

### PaymentService

- **Nhiệm vụ**: Quản lý quá trình thanh toán lương tự động cho nhân viên.
- **Thuộc tính chính**:
  - `paymentId: String`
  - `amount: Double`
  - `status: String`
- **Phương thức**:
  - `initiatePayment(payrollData)`: Bắt đầu quá trình thanh toán dựa trên dữ liệu bảng lương.
  - `confirmPayment()`: Xác nhận khi thanh toán thành công.

### BankAPI

- **Nhiệm vụ**: Kết nối với hệ thống ngân hàng để thực hiện chuyển khoản lương.
- **Thuộc tính chính**:
  - `transactionId: String`
  - `bankAccount: String`
- **Phương thức**:
  - `processTransaction(amount)`: Xử lý giao dịch chuyển khoản dựa trên số tiền được yêu cầu.
  - `confirmTransaction()`: Xác nhận giao dịch thành công hoặc thất bại.

## Biểu Đồ Lớp Mô Tả Các Lớp Phân Tích

![diagram](https://www.planttext.com/api/plantuml/png/R991RiCW44NtFiKitOKlu4MLHjba5yczm1Yc4Ie62uP8LjIJTT4ZzGh5DOuDBJluyvat7xu_lmwUqN4OT2KqUWyNd9pLkYDtKuBWNa5S3T0mQZiHdMKB7JjbhadeqLE76jtKmic6NbCI9CaWM5dZ2w6t9dZAJm44QX4qCYM0-gaek18dwOICixpRLX_LnZ-GuP9_N8x_uEDWW-62C4R2mMUL0CeeLWlVV5CzRjqpb0XsiqgkOrdpfjomcg9uj5OJcetuYERzvN9-eB93u_4tkd_IZhL2BCmPtkYi8EzVDtETpxPhdQ7j7JbUyHMQvhbCjmLFHaAA0kJy4aN9x5edR1yXhkzH7Q9__dm_0000__y30000)

## Giải Thích

- PayrollService tính toán bảng lương và gửi dữ liệu đến PaymentService để thực hiện thanh toán.
- Payment
# Hợp Nhất Kết Quả Phân Tích

## Tài Liệu Mô Tả Hệ Thống Quản Lý Lương
**Tên Hệ Thống**: Hệ thống Quản lý Lương của Acme, Inc.

**Mục tiêu**: Cung cấp một giải pháp hoàn chỉnh cho việc quản lý lương, chấm công và thanh toán cho nhân viên, đảm bảo tính chính xác, bảo mật và tự động hóa trong quy trình.

### Các Ca Sử Dụng Chính
#### Payment:
- **Mô tả**: Ca sử dụng này xử lý quá trình thanh toán lương cho nhân viên. Sau khi tính toán lương từ dữ liệu chấm công, hệ thống sẽ thực hiện thanh toán qua ngân hàng.
- **Các lớp liên quan**:
  - **PayrollService**: Tính toán tổng lương và gửi dữ liệu cho PaymentService.
  - **PaymentService**: Quản lý quá trình thanh toán và tương tác với ngân hàng qua BankAPI.
  - **BankAPI**: Thực hiện giao dịch ngân hàng và xác nhận thanh toán.
- **Biểu đồ Sequence**:
![Biểu đồ Sequence Payment](https://www.planttext.com/api/plantuml/png/P951Zi8m34NtEON5dWjqWM0g5kog6N40A_L8rgH9I5oadeq5H-8AasQQ3e5TOZzzFoUFstqV1OECWr6enGKu3jwuYKZvL6RD7gt0fiCfE6FWYyALDMq08oorDt2WT7W1vreDVg3zWKDtoiHyKQgCXkskX4C3dtGPAGfudA9XhqgdWbeqUZGeD6FPgiQoKvEiR5y8w55GbLx2ib439yl2IrBMplLjbTCw-yrXM94rfP8w-_x92D93onZ_nHAxRjn05zoLUofh0YPJ_JS6XPrL--G-VzCl0000__y30000)

#### Maintain Timecard:
- **Mô tả**: Ca sử dụng này quản lý dữ liệu chấm công của nhân viên. Nhân viên sẽ nhập dữ liệu chấm công, và hệ thống sẽ xác thực và cập nhật dữ liệu.
- **Các lớp liên quan**:
  - **UserService**: Cung cấp thông tin nhân viên và xác thực quyền truy cập.
  - **TimecardService**: Quản lý thông tin chấm công, xác thực và cập nhật dữ liệu chấm công.
- **Biểu đồ Sequence**:
![Biểu đồ Sequence Maintain Timecard](https://www.planttext.com/api/plantuml/png/ZD112i9030NG_PmYkEy5kf22U05htSUP286PTina1C_cmYDv1Tk1bXOtRlz_2I6Vrxj9Yg8vU8DM1u5ZY7vu4fauncmvOg-mEtCWY-AW9NcmfHrWWZdSqYwHRDWK63FlXMfV4gZXHFTCIO7cof4Y-sHANurm6PgmPkb_xNhlScKDRRu6Lj0vSQXebdvhB-XvxEa_tSLYXUmWBgtKzjx3qDzO0kJ2JKEzcvxy1G00__y30000)

### Kết Hợp Các Lớp và Mối Quan Hệ
**Mối quan hệ giữa các lớp**:
- **PayrollService** và **PaymentService**: 
  - **PayrollService** tính toán lương dựa trên dữ liệu chấm công và gửi dữ liệu đó đến **PaymentService**.
  - **PaymentService** xử lý quá trình thanh toán cho nhân viên, sử dụng thông tin từ **PayrollService**.
- **PaymentService** và **BankAPI**: 
  - **PaymentService** gọi **BankAPI** để thực hiện các giao dịch ngân hàng, đảm bảo thanh toán được thực hiện một cách tự động và chính xác.
- **UserService** và **TimecardService**: 
  - **UserService** xác thực quyền truy cập của nhân viên và cung cấp thông tin cần thiết cho **TimecardService**.
  - **TimecardService** ghi lại và quản lý dữ liệu chấm công, liên kết với thông tin người dùng từ **UserService**.

## Kết Luận
Hệ thống quản lý lương của Acme, Inc. dự kiến sẽ cải thiện quy trình quản lý lương, tăng cường bảo mật và tự động hóa thanh toán. Việc áp dụng kiến trúc Microservices cho phép dễ dàng mở rộng và bảo trì hệ thống trong tương lai. Các dịch vụ độc lập như User Service, Payroll Service, Timecard Service và Payment Service sẽ làm việc cùng nhau để cung cấp giải pháp hiệu quả cho việc quản lý lương và chấm công.
