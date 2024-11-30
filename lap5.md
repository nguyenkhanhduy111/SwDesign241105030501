# Thiết kế hệ thống con Login
### 1.Distribute Subsystem Behavior to Subsystem Element
Phân rã hành vi hệ thống con:
User Interface Subsystem:
- Nhận thông tin đăng nhập từ người dùng (username, password).
- Hiển thị thông báo lỗi hoặc chuyển hướng sau khi xác thực.
  
Authentication Subsystem:
- Kiểm tra thông tin đăng nhập từ cơ sở dữ liệu.
- Mã hóa và giải mã mật khẩu.

Database Subsystem:
- Truy xuất thông tin người dùng từ cơ sở dữ liệu (username, password hash).
- Lưu trữ hoặc cập nhật dữ liệu phiên đăng nhập (session data).

Authorization Subsystem:
- Gán vai trò (role) và quyền hạn (permissions) cho người dùng sau khi đăng nhập.
### 2. Document Subsystem Elements
#### User Interface Subsystem 
Chức năng:
- Giao diện nhập tên đăng nhập và mật khẩu.
- Hiển thị thông báo lỗi hoặc chuyển hướng sau khi đăng nhập thành công.
Thành phần:
- LoginForm: Biểu mẫu đăng nhập.
- ErrorMessage: Hiển thị thông báo lỗi khi đăng nhập thất bại.
#### Authentication Subsystem 
Chức năng:
- Xác thực thông tin người dùng.
- Mã hóa và kiểm tra mật khẩu.
Thành phần:
- Authenticator: Kiểm tra thông tin người dùng với cơ sở dữ liệu.
- PasswordHasher: Xử lý mã hóa mật khẩu.
#### Database Subsystem 
Chức năng:
- Lưu trữ thông tin người dùng và phiên đăng nhập.
- Truy xuất thông tin dựa trên tên đăng nhập.
Thành phần:
- UserTable: Bảng dữ liệu chứa thông tin người dùng.
- SessionTable: Bảng dữ liệu chứa thông tin phiên.
#### Authorization Subsystem 
Chức năng:
- Xác định vai trò và quyền hạn của người dùng sau khi đăng nhập.
Thành phần:
- RoleManager: Quản lý vai trò của người dùng.
- PermissionChecker: Xác định quyền truy cập dựa trên vai trò.
### 3. Describe Subsystem Dependencies
Các mối phụ thuộc giữa các hệ thống con:
User Interface → Authentication

Hệ thống giao diện gọi Authenticator để xác thực thông tin người dùng.
Authentication → Database

Authenticator yêu cầu dữ liệu từ UserTable trong hệ thống cơ sở dữ liệu.
Authentication → Authorization

Sau khi xác thực, Authenticator yêu cầu RoleManager trong Authorization để gán vai trò.
Authorization → Database

RoleManager có thể truy cập UserTable để lấy thông tin vai trò người dùng.
User Interface → Authorization

Sau khi gán vai trò, thông tin vai trò được gửi lại User Interface để hiển thị quyền hạn.
### 4. Checkpoints
Các bước kiểm tra hoàn thiện:
Input Validation:
Đảm bảo hệ thống con User Interface xác thực đầu vào (username, password không rỗng, định dạng hợp lệ).

Authentication:
Authenticator kiểm tra mã hóa mật khẩu và xác thực thông tin từ UserTable.

Session Handling:
Đảm bảo SessionTable trong Database lưu trữ dữ liệu phiên đăng nhập đúng.

Role Assignment:
RoleManager xác định chính xác vai trò dựa trên thông tin trong UserTable.

Error Handling:
Hệ thống hiển thị thông báo lỗi khi người dùng nhập sai thông tin.
### Sơ đồ phụ thuộc giữa các hệ thống con Login
![Dependency - Login](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3XTNGM9oTc9wgeAIJtvwPfv2S6bISMLnIMgkaa8rbu92T6XnQf62Prv9Qb5QOd8gGZfMGLVNJY7QiRGa8pMl93CviIGp7qbtB4WlJac8NfV4aiIanE9KqdG5fnONWyHz4_E0piu5gaJJZrS1n0omfmAAyjCoSr1ihqKA3apNGKC4YxEHJ8N9eXg6pqrGOubmDam9YXqEgNafe8W40000__y30000)


# Thiết kế hệ thống con Run Payroll
### 1.Distribute subsystem behavior to subsystem elements:
#### Payroll Calculation Subsystem: 
Xử lý tất cả các tính toán liên quan đến việc tính toán tiền lương của nhân viên, bao gồm việc tính toán lương cơ bản, các khoản phụ cấp, thuế, và các khoản trừ.
#### Tax Calculation Subsystem: 
Tính toán các khoản thuế phải trả dựa trên dữ liệu của nhân viên và quy định thuế.
#### Employee Database Subsystem: 
Lưu trữ thông tin về nhân viên như mức lương, số giờ làm việc, các khoản phụ cấp, thuế phải trả, v.v.
#### Payment Processing Subsystem: 
Xử lý việc thanh toán tiền lương cho nhân viên, có thể bao gồm việc chuyển tiền qua ngân hàng hoặc các hình thức thanh toán khác.
#### Notification Subsystem: 
Thông báo cho nhân viên về thông tin liên quan đến tiền lương và các khoản thanh toán.

### 2.Document subsystem elements:
#### Payroll Calculation Subsystem: 
Xử lý tính toán các khoản chi trả, bao gồm lương cơ bản, phúc lợi, thuế và bảo hiểm.

#### Employee Data Subsystem:
Quản lý và cung cấp thông tin nhân viên cần thiết để tính toán lương, chẳng hạn như mức lương cơ bản, các khoản phụ cấp, giờ làm việc.

#### Payment Subsystem:
Quản lý việc thanh toán lương cho nhân viên thông qua các phương thức thanh toán (chuyển khoản ngân hàng, séc, tiền mặt).

#### Tax Calculation Subsystem: 
Tính toán các khoản thuế cần thiết phải trừ từ lương của nhân viên.

#### Accounting Subsystem:
Đảm bảo việc ghi chép và báo cáo các khoản thanh toán đúng đắn

### 3.Describe Subsystem Dependencies:
Payroll Calculation Subsystem phụ thuộc vào Employee Data Subsystem để có thông tin về nhân viên.

Payroll Calculation Subsystem cũng phụ thuộc vào Tax Calculation Subsystem để tính toán thuế thu nhập.

Payment Subsystem phụ thuộc vào Payroll Calculation Subsystem để thực hiện các khoản thanh toán sau khi tính toán lương.

Accounting Subsystem phụ thuộc vào Payment Subsystem để lưu trữ các giao dịch thanh toán.

### 4.Checkpoints
Đảm bảo thông tin về nhân viên được cập nhật đầy đủ trong Employee Data Subsystem.

Tính toán chính xác các khoản thuế và bảo hiểm từ Tax Calculation Subsystem.

Kiểm tra rằng các khoản thanh toán được thực hiện chính xác từ Payment Subsystem.


### Sơ đồ phụ thuộc giữa các hệ thống con Run Payroll
![Dependency - Run Payroll](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3XTNGM9oTc9wge9IK6cUGa1YPL1-JewIGZMNWa8qa5S4v2au9-Oab-OabcJcvoa4boOLLnQNfER6AkZgsYb4k-OMvEHNfgOgk2IM92B94gi_9B42XppKXDpKl18CNVXD1kbqJ4xEByqhoSnBnwOPpL2kMW00003__mC0)


# Thiết kế hệ thống con Maintain Purchase Order
### 1.Distribute subsystem behavior to subsystem elements:
#### Purchase Order Management Subsystem:
Quản lý các đơn đặt hàng từ khi bắt đầu đến khi hoàn thành, bao gồm tạo, sửa, và theo dõi đơn hàng.

#### Inventory Subsystem:
Quản lý kho hàng, kiểm tra tình trạng kho để đảm bảo khả năng cung cấp cho đơn hàng.

#### Supplier Subsystem: 
Quản lý thông tin nhà cung cấp, bao gồm các điều kiện giao hàng và thanh toán.

#### Payment Subsystem: 
Quản lý việc thanh toán cho nhà cung cấp.

#### Approval Subsystem: 
Xử lý phê duyệt các đơn hàng trước khi chúng được hoàn thành.


### 2.Document subsystem elements:

#### Purchase Order Management Subsystem: 
Chịu trách nhiệm tạo, sửa đổi, và theo dõi các đơn đặt hàng.

#### Inventory Subsystem: 
Đảm bảo kho hàng có đủ nguyên vật liệu để cung cấp cho các đơn hàng.

#### Supplier Subsystem: 
Quản lý các nhà cung cấp, các điều khoản thanh toán, và thời gian giao hàng.

#### Payment Subsystem: 
Quản lý các khoản thanh toán cho nhà cung cấp.

#### Approval Subsystem:
Quản lý quy trình phê duyệt đơn hàng từ các cấp có thẩm quyền.


### 3.Describe Subsystem Dependencies:

Purchase Order Management Subsystem phụ thuộc vào Inventory Subsystem để đảm bảo có đủ hàng hóa để cung cấp cho đơn hàng.

Purchase Order Management Subsystem phụ thuộc vào Supplier Subsystem để chọn nhà cung cấp phù hợp cho các đơn hàng.

Payment Subsystem phụ thuộc vào Purchase Order Management Subsystem để thanh toán cho nhà cung cấp.

Approval Subsystem phụ thuộc vào Purchase Order Management Subsystem để phê duyệt các đơn đặt hàng.

### 4.Checkpoints:
Kiểm tra tình trạng kho hàng để đảm bảo có đủ nguyên vật liệu (phụ thuộc vào Inventory Subsystem).

Đảm bảo các đơn hàng được phê duyệt qua Approval Subsystem trước khi được xử lý.

Thanh toán chính xác cho nhà cung cấp qua Payment Subsystem.

### Sơ đồ phụ thuộc giữa các hệ thống con Maintain Purchase Order
![Dependency - Maintain Purchase Order](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3XTNGM9oTc9wgeAIRs9cNWaGAmIK5YLd91QdAlWNfQGMAIbKSoaeHACAAlWcvW4rvQRcbIW4boOLLnQNfER6AkZgsYb4U-QL0ONpYogHP4Wp8RYqe20d4wW6pO34IgpAYJ4OfD-neA0elomnXpm3QhaSKlDIW4460000__y30000)
