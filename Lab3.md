# Lab 3: Identify Design Elements

## 1. Subsystem Context Diagrams

### 1.1. BankSystem Subsystem Context Diagram

![Diagram](https://www.planttext.com/api/plantuml/png/T9112W8n34NtFKKlu0LSYAZWIX173n3h7wrEKqoZC6TpuP6yWYquwC2u_SdxFp-lntEQb4HleJ7aD8hT9OW1gzVMhgcLs3HLcnIX4sV4bxwo5izQGUxUuQl5CvokYEc8aCK5AUqfmPYIO4UZIT_UZcq5FXInhDiDhZSaDVsbWdqFoCnMY5ET3J-S-PaEPNJsyyYrbq3g8mza_5RAr18C8KN1tGdkCeZyQLoQvS_2Rds08pcOQIvQFlu6003__mC0)


**Mô tả:**
- `BankSystem`: Hệ thống phụ trách xử lý các giao dịch thanh toán với ngân hàng.
- `PrintService`: Dịch vụ in ấn phiếu lương cho nhân viên.
- `ProjectManagementDatabase`: Cơ sở dữ liệu quản lý thông tin dự án và timecard của nhân viên.

### 1.2. PrintService Subsystem Context Diagram

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTgNabcIQL2G69bKNvEJd1bSKbgBbomA3El93Yrg2mpEHL5BBM8Ymj5XuAkhXsASWKhXQ3KmjBKuXA8C1UA95nrQX5G8PW5Sa5oHcfoDXTC0ekH49NE-Ra5EQabgLZCH76JbO9VVabcMcPoOabcVXwNGsfU2iZ700000F__0m00)


**Mô tả:**
- `PrintService`: Hệ thống chịu trách nhiệm in các phiếu lương dựa trên yêu cầu từ PayrollSystem.

### 1.3. ProjectManagementDatabase Subsystem Context Diagram
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTgNabcIQL2G69bKNvEJd1bSKbgBbomA3yhDRd4Dp4lCJqr5oZeabYIc9HOdCh5XQ9UGLVN3hTY1Ik5u9ByebI5aCpSrEJ4eXGkt4h11g4ORQKGb5fIb9bQXj2l05BEvP2QbmBo00000F__0m00)


**Mô tả:**
- `ProjectManagementDatabase`: Hệ thống cơ sở dữ liệu quản lý thông tin timecard, phục vụ cho việc tính lương.

## 2. Analysis Class to Design Element Map

| Analysis Class         | Design Element            |
|------------------------|---------------------------|
| LoginForm              | LoginForm                 |
| MaintainTimecardForm   | TimecardForm              |
| EmployeeController     | MainEmployeeForm          |
| TimecardController     | TimecardController        |
| SystemClockInterface   | SystemClockInterface      |
| PayrollController      | PayrollController         |
| Paycheck               | Paycheck                  |

## 3. Design Element to Owning Package Map

| Design Element         | Owning Package            |
|------------------------|---------------------------|
| LoginForm              | UI                        |
| TimecardForm           | UI                        |
| MainEmployeeForm       | UI                        |
| TimecardController     | Controller                |
| SystemClockInterface   | Interface                 |
| PayrollController      | Controller                |
| Paycheck               | Model                     |

## 4. Architectural Layers and Dependencies
![Diagram](https://www.planttext.com/api/plantuml/png/P9112i8m44NtEKKkq0jq8GLHA5WGr0E4PBIXIQOagLB4axdmI5x1nDYcuAnc_l_pcEJzV5NEC-i7hGXNp3bwgkcTq5Wxl4YpHQlJU9GQEBCYAmsJPgDxXIF0LtsG7sIDnbjK2km4cxQpa_Gz6-Eua6T8RJpOC-CmCGwZyw3N2datUpdUe00rHGEMjy2xQ8SN5SLgULD91mUEB9GOI82IoiXct3jwaxub-Om_Ic_nAaKWfTNevtH91VHWXADeI1MQ-CSV0000__y30000)


**Giải thích:**
- `UI`: Chứa các phần tử giao diện người dùng như form nhập liệu.
- `Controller`: Quản lý luồng dữ liệu và tương tác với model.
- `Interface`: Định nghĩa các giao diện cho hệ thống.
- `Model`: Chứa các lớp mô hình dữ liệu như `Paycheck`.
