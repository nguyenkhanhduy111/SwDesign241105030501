# Phân tích ca sử dụng trong hệ thống Pay roll

## 1. Thiết kế ca sử dụng Login

### 1.1 Describe interaction among design objects

  Mục tiêu: Mô tả sự tương tác giữa các đối tượng thiết kế chính trong Use Case.

  Các đối tượng chính bao gồm:

  - User (Người dùng): Gửi thông tin đăng nhập.
  - Authentication System (Hệ thống xác thực): Xử lý logic xác thực.
  - Database (Cơ sở dữ liệu): Lưu trữ thông tin tài khoản và kiểm tra thông tin đăng nhập.

  Sơ đồ tuần tự (Sequence Diagram):

  ![Diagram](https://www.planttext.com/api/plantuml/png/T90nJWCn44Lxd-8hLI8HqM-1mceb2XeabWCuni9MOcTPpo8eKKw0k02hY88Y1HBLRf5YSn6VW2imZb0a2ZhF_F_V7_cxtyq2oPeQjnHIqQh6JT2rg7XbbQsa9upE6pBQyop9hZokdm9fDu8CICfVRo59pcNG1xd8XKWuJCyErWmNiTzQa1c-_1t8UknVzcj-UXExROMnTj8kJ-1u8Ynu-T5CH8ecH95dkBInNpjGBV-bY2B7zDXOrh7Ru27sprZ4RaUuRzBYSMWL4sB_gNxvd4YtPhXYoiQ3jLS-bUDjQZ53Qp4kpV3c3LHgFYtP-4wOiyDEn4pxM_x57m000F__0m00)

  Giải thích:

  - Người dùng gửi thông tin đăng nhập (email và mật khẩu) đến hệ thống xác thực.
  - Hệ thống xác thực gửi yêu cầu kiểm tra thông tin đến cơ sở dữ liệu.
  - Cơ sở dữ liệu trả về kết quả xác thực (hợp lệ hoặc không hợp lệ).
  - Hệ thống xác thực phản hồi người dùng với trạng thái đăng nhập (thành công hoặc thất bại).
  ### 1.2. Simplify sequence diagrams using subsystems

  Mục tiêu: Đơn giản hóa sơ đồ tuần tự bằng cách sử dụng các phân hệ (subsystems).

  Trong Use Case Login:

  - Nhóm các chức năng liên quan đến giao diện người dùng vào UI Subsystem.
  - Nhóm các chức năng xử lý xác thực vào Authentication Subsystem.
  - Nhóm các chức năng lưu trữ dữ liệu vào Database Subsystem.

  Sơ đồ tuần tự với phân hệ (Subsystems):

  ![Diagram](https://www.planttext.com/api/plantuml/png/T94nQWCn44LxdUBZtXVO8ZZBGc828U3i0UIro8favRKq6v8ok4mLV8B5jOj0gbNXOdqHdI1NoCYO49kuasRU_F-7-VRRaIDfgQcUX2neRf4xPKND9LteMXh281zZqapTgoDL3I0Tyl4nSDbGgGp_9UcvEO5ZynZF9CcfTEe4p58XeZc65-oGuBOCtQO6bVsNUG1fWzt7RibFisy8ZiLab4zm5Vn6dqSZ5E4iJN2ZWrzM82lFyrcAuQ_slGtT6i_1l-4nT5l2eec5bxujM27up-AWVyXznnfh0-wiE18Fjz6Zx5lzpm9nXdTES1rZcRtW-ryVCL9cnjVv0G00__y30000)

  Giải thích:

  - UI Subsystem: Nhận thông tin từ người dùng và hiển thị kết quả.
  - Authentication Subsystem: Xử lý logic xác thực.
  - Database Subsystem: Lưu trữ và kiểm tra thông tin tài khoản.
### 1.3. Describe persistence-related behavior

  Mục tiêu: Mô tả hành vi liên quan đến lưu trữ dữ liệu.

  Trong Use Case Login:

  - Hệ thống cần lưu trữ thông tin tài khoản người dùng (email và mật khẩu) trong cơ sở dữ liệu.
  - Khi người dùng đăng nhập, hệ thống xác thực cần truy vấn cơ sở dữ liệu để kiểm tra thông tin.

  Sơ đồ lớp liên quan đến lưu trữ:

  ![Diagram](https://www.planttext.com/api/plantuml/png/LPBDIiD058NtWRp3fQk46heFKhfGeQ0Wb3x0RUSs6KncwlnKH7mNmHTmuSfjmVVmJRoPP6YIJM1EpdVlEPcLTMYSRviqsJTeBMmj6NXB4-2d02bAaCh1z5aiOAlaioVMIJbva6IYWrgKJGaRPwIgnexRJW1lIS116sXq9LKq7NdoYpPYwcFJuo10Pclj6m4xWXfjJI8Vl4N_daD5RYsoFEmxEWjZk-EUF58YUoo-fqaiuWOTxj1IB6CE5a-KSG1JXfROTj9Iz8jkMEl26HxFyLfqKYjm6bnD80PK11sa4jcagBn7TgGx5W5xrkwrxtEQjG3hjC6AIdZ0utLFk0g0PKTOAqT6OHC_u_9awnjqP1aSbyc7j65kKImlWKkOtVz-ULxz_Ct_maaESlwGy5JhlvzF1La8Y_kzzdmrkhpvB4rMf4IuH_y0)

  Giải thích:

  - Lớp User đại diện cho thông tin tài khoản người dùng, bao gồm id, email, và password.
  - Lớp Database cung cấp các phương thức để lưu trữ (save) và truy xuất (find) thông tin tài khoản.
### 1.4. Refine the flow of events description
  
 Mục tiêu: Định nghĩa rõ cả luồng chính và luồng thay thế.

- *Luồng chính*:

- Người dùng nhập thông tin đăng nhập.
- Hệ thống xác thực kiểm tra thông tin.
- Thông tin hợp lệ, người dùng được đăng nhập thành công.
- *Luồng thay thế*:

- Người dùng nhập sai email hoặc mật khẩu.
- Hệ thống xác thực trả về thông báo lỗi (e.g., "Sai mật khẩu" hoặc "Tài khoản không tồn tại").

  - Luồng chính: Người dùng gửi thông tin đăng nhập, thông tin được xác thực và phản hồi trạng thái đăng nhập.
  - Luồng thay thế: Nếu thông tin không hợp lệ, hệ thống trả về thông báo lỗi.

  Sơ đồ tuần tự với luồng thay thế:

  ![Diagram](https://www.planttext.com/api/plantuml/png/b94nJWCn44Lxd-8hVIwm1GhHIXIKX0DC5YksikjTx5aaIfI25YfQejJfgDP5Ykn5V0AkW9qWI10fqbZZcV_dVMa-_MRac2otLIceuDhYraahcjZIXMx8C0QNBIjfufzOrmOtZuvbDG0vfCcnDYUcAJcv6-TZ8T8w32zsqWnNmQyrM6q_p0oi3VhNVX5BeqAtRaGI9N4-pd2jWrzKO4kdzLGo9hz35VogGHdyiq3SWU4FTs93jy93y4-OXsx3k6zJuyYmXqTBYfoXVpaWfGZlHg58B25B9m-vytrvDlu_tvyKtvJfTbadnPiMqjo9KNpYnRu0003__mC0)

  Giải thích:

  Sử dụng khối alt để mô tả hai luồng sự kiện:

  - Luồng chính: Thông tin hợp lệ, người dùng được đăng nhập.
  - Luồng thay thế: Thông tin không hợp lệ, người dùng nhận thông báo lỗi.
### 1.5. Unify classes and subsystems

 - *UI Subsystem*:

- Lớp LoginPage: Giao diện người dùng.
- Lớp LoginController: Quản lý sự kiện giao diện.
- *Authentication Subsystem*:

- Lớp AuthService: Xử lý logic xác thực.
- Lớp Validator: Kiểm tra tính hợp lệ của dữ liệu (format email, độ dài mật khẩu, v.v.).
- *Database Subsystem*:

- Lớp UserRepository: Kết nối với cơ sở dữ liệu, thực hiện lưu trữ và truy vấn dữ liệu.
- Lớp Database: Quản lý kết nối với cơ sở dữ liệu.

  Sơ đồ lớp hợp nhất với phân hệ:

  ![Diagram](https://www.planttext.com/api/plantuml/png/VLN1Rjim3BqNw3yGEJd8ZDoDeIYmjbiF0ueQtLsnQLUOBNcId2qOzkyZ9QUH72T6W3WY-KW-FYhtrWdZnhwxlHb4zLEq2Ait9Hk9DNmNYdxtg1oK1-kmNy7VsnkWf-g4jV1cqHnF-Cb1rWL8Sa-VxHO8yjU8P2Sm1ZTn5FP2TWMKpaZLnb6FR83HKYsDDg07DC99hMmSNGidpeAddBuDTe1iCBf2Ir3hA3W_lM-WHVTSPslVmUpS5yAca6PcVQ04oqOx6UCQoN6lPHtS_eMlX5Kkk_9zbcZsiiAOumsCP3zuL2B657uAXBdJkaEXJks_X8P1g3h412AOIC6ScXXqBpf9Pln2v4eQjQeEo_04_6FoXUha3Bhnc3x7HslqYMHLEctufHntTb5EOLxSsaxOMTTMx36jY4ay5rf9VhvTdholI2fgkVTyne2DL7MMA6yTe6U0J-Gt4GQxGz3gie9oiA73WZPd-1n0FtdCknJpMJaqIdJ70CYixCUEEBMSAj8j4x6-A1McwXlDjqltS0EqA3oPwuInHe9VIjXfX07C87M2HFyrjWZiTV9BqLBEpaJnYeCsZbVtaYo2nrTKlFnwrcWRZcVIEBz9fd0aUet7WyRe_dhV-8STiw2UsVR6s8_UxuZhDELevHuLXCYqyONjplExC-qNT0jRKWDlgr_RyHIt8XIkzoCkXQFG5y4N7PTotEkjlm4eCfRCXSHUdQ9o5dvBzqunymbSJlo4hdgdicC9UwO9vHvLxVzd_WC0)

  Giải thích:

  - UI Subsystem: Chịu trách nhiệm giao tiếp với người dùng (nhận thông tin và hiển thị kết quả).
  - Authentication Subsystem: Xử lý logic xác thực (kiểm tra thông tin đăng nhập).
  - Database Subsystem: Lưu trữ và quản lý thông tin người dùng.
