**🇬🇧 To view the English version, please [visit here](README-en.md).**

3S eShop là một dự án phục vụ cho môn học Mẫu Thiết Kế (Design Patterns), bao gồm phần mềm Winforms quản lý bán linh kiện điện tử có tích hợp các mẫu thiết kế.

Dự án phục vụ cho mục đích học thuật và sử dụng nội bộ phi thương mại. Để sử dụng cho mục đích thương mại, vui lòng đảm bảo tuân thủ đầy đủ bản quyền về quyền tác giả của các hình ảnh sử dụng, trích dẫn trong dự án.

---
# Thông tin thành viên nhóm:

| Tên thành viên    | MSSV     | Note |
| ----------------- | -------- | ---- |
| Đặng Văn Trọng    | Censored | PM   |
| Nguyễn Thành Tiến | Censored |      |
| Nguyễn Vĩnh Hưng  | Censored |      |

---
# Thông tin sơ lược về sản phẩm:
- Sản phẩm của nhóm ban đầu là một phần mềm hỗ trợ quản lý bán linh kiện điện tử. Mặc dù vậy, quản trị viên có thể thêm các danh mục (category) tùy ý.
- Mục đích chính của project là tích hợp tối thiểu 10 design patterns vào phần mềm. 
- Các chức năng sẽ có như:
	- Đăng nhập và đăng ký tài khoản.
	- Tìm kiếm sản phẩm tùy chỉnh theo bộ lọc.
	- Xem thông tin sản phẩm và đặt hàng mà không cần tài khoản.
	- Chat với bộ phận CSKH (usecase cơ bản là dùng tài khoản admin để trả lời).
	- Các chức năng quản lý tài khoản (chưa hoàn thiện), danh mục, nhà sản xuất, sản phẩm (chưa hoàn thiện), đơn hàng của admin (chưa có).
	- Hỗ trợ đa CSDL: MySQL, SQL Server (chưa tương thích ổn định hoàn toàn).
- Các công nghệ áp dụng:
	- Google Cloud API.
	- Cơ sở dữ liệu MySQL
	- Cơ sở dữ liệu phân tán Redis.
	- Mã hóa AES-256 đơn giản một chiều (triển khai production đương nhiên sẽ nằm ở backend).
- Nhóm quyết định rằng chỉ làm một sản phẩm ở quy mô vừa đủ áp dụng các pattern, tập trung vào flow hoạt động của sản phẩm. Do đó, kiến trúc ứng dụng sẽ chỉ có client-side kết nối trực tiếp đến cơ sở dữ liệu cũng như nơi lưu dữ liệu, không thông qua server. Nhóm cần phải thừa nhận rằng kiến trúc này là cực kỳ thiếu an toàn vì client cần có secret để có thể hoạt động (theo như quy chuẩn là secret PHẢI được đặt ở server). Tuy nhiên, mục đích của sản phẩm là áp dụng quy trình hoạt động nên việc này là chấp nhận được khi chương trình chỉ được sử dụng nội bộ. Về vấn đề mở rộng sản phẩm và triển khai lên production thì cần phải xây dựng riêng back-end để tách xử lý các logic liên quan đến dữ liệu.

---
# Các mẫu thiết kế áp dụng trong đồ án:

| STT | Tên              | Công dụng                                                                                                                                                                                                                                                             |
| --- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Singleton        | - Ghi log ra file.<br>- Cung cấp duy nhất một instance truy cập vào CSDL.                                                                                                                                                                                             |
| 2   | Strategy         | Kiểm tra tính hợp lệ của nội dung trong TextBox bằng cách tạo một Custom TextBox.                                                                                                                                                                                     |
| 3   | Command          | Chức năng enable và disable các button của hệ thống                                                                                                                                                                                                                   |
| 4   | Simple Factory   | Tạo các User Control cho MainForm                                                                                                                                                                                                                                     |
| 5   | Abstract Factory | Cung cấp chức năng kết nối đa CSDL cho phần mềm (MySQL, SQL Server).                                                                                                                                                                                                  |
| 6   | Observer         | Cập nhật trạng thái chờ đếm ngược của hệ thống gửi mã OTP, theo dõi tiến trình tạo/cập nhật sản phẩm.                                                                                                                                                                 |
| 7   | Decorator        | Lọc dữ liệu hiện lên cho người dùng.                                                                                                                                                                                                                                  |
| 8   | Facade           | Đóng gói các hành vi thông dụng nhất như thêm, xóa, sửa vào trong một class, sự phức tạp khi này sẽ do class Facade quản lý.                                                                                                                                          |
| 9   | Builder          | Tách biệt quá trình khởi tạo đối tượng khỏi cấu trúc lớp, giúp mã nguồn trở nên dễ đọc, dễ bảo trì và tránh được việc phải viết nhiều constructor hoặc các phương thức khởi tạo phức tạp.                                                                             |
| 10  | Template Method  | Giúp giảm thiểu trùng lặp mã nguồn khi các thao tác chia sẻ cùng một luồng logic, đồng thời tăng tính bảo trì vì các thay đổi đối với quy trình chung chỉ cần thực hiện tại một nơi duy nhất, đáp ứng nguyên lý mở rộng–đóng kín (Open/Closed Principle) trong SOLID. |
| 11  | Flyweight        | Tối ưu hóa việc sử dụng bộ nhớ và tăng tốc độ tải khi tải nhiều ảnh trùng lặp trên màn hình.                                                                                                                                                                          |
| 12  | State            | Quản lý trạng thái của nút xác nhận cần nhấn 2 lần.                                                                                                                                                                                                                   |

---
# Hướng dẫn chạy chương trình và tiếp tục phát triển chương trình:
1. Tạo một dự án Google Console:
	- Tạo Oath Client dành cho ứng dụng Desktop.
	- Kích hoạt DriveAPI.
	- Tải các file `GDriveCredentials.json` và `GOathCredentials.json` về và di chuyển vào trong thư mục `secret_data` và ghi đè lên 2 file json hiện có.
	- Truy cập vào dịch vụ Drive với tài khoản mà dự án Google Console có quyền quản lý, sau đó tạo một thư mục để chứa dữ liệu của ứng dụng hiện tại, sao chép id thư mục và điền vào key `GDRIVE_FOLDER_ID` của file `.env` (trong thư mục `secret_data`).
2. Tạo CSDL MySQL trên bất kỳ nền tảng nào (kể cả local lẫn hosting).
	- Tạo schema `3S_eShopDb`.
	- Khôi phục dữ liệu bằng file `3S-eShop-MySql-dump.sql`
		- Ghi chú: File dump này đã có một lượng dữ liệu nhất định, nhưng đã loại bỏ dữ liệu ảnh ở trên Google .
	- Lấy thông tin kết nối của CSDL và điền vào file `.env:
		- `DB_HOST`: là địa chỉ máy chủ của CSDL.
		- `DB_PORT` là số cổng mạng của CSDL.
		- `DB_USER` là tên người dùng có quyền truy cập vào CSDL.
		- `DB_PASS` là mật khẩu của CSDL.
		- `DB_NAME` là tên schema của CSDL.
		- `DB_CONN` là chuỗi kết nối của CSDL, có cấu trúc:  `Server=DB_HOST;Port=DB_PORT;Database=DB_NAME;Uid=DB_USER;Pwd=DB_PASS;`
		- `DB_TYPE`: giữ nguyên `mysql`.
	- Ghi chú: Có thể chuyển sang SQL Server nhưng sẽ không đảm bảo tương thích hoàn toàn (khi này thì `DB_TYPE` chuyển thành `sqlserver` ).
3. Tạo CSDL Redis trên bất kỳ nền tảng nào, sau đó lấy thông tin truy cập và nhập vào file `.env`:
	- `REDIS_HOST`: là địa chỉ máy chủ của CSDL Redis.
	- `REDIS_PORT`: là số cổng mạng của CSDL Redis.
	- `REDIS_USER`: là thông tin người dùng truy cập Redis.
	- `REDIS_PASS`: là thông tin mật khẩu truy cập Redis.
4. Mở dự án trong Microsoft Visual Studio và chạy chương trình ở chế độ Debug (hoặc Release), chương trình sẽ tự động lấy dữ liệu cần thiết trong thư mục `secret_data` để kết nối đến CSDL cũng như Google Cloud API.

---
# Ảnh chụp

| ![screenshot-1](https://github.com/user-attachments/assets/dd9c8bee-f27b-43ce-89e2-d3f55f4c5fe6) | ![screenshot-2](https://github.com/user-attachments/assets/a6639667-9c9a-4ee4-94f2-63b5821d06d9) | ![screenshot-3](https://github.com/user-attachments/assets/c9a65f2e-64df-49e2-8186-0a23cd45d8ef) | ![screenshot-4](https://github.com/user-attachments/assets/c3a27638-1481-4922-802e-1c0b26c420f9) |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| ![screenshot-5](https://github.com/user-attachments/assets/31373a0b-5404-4112-af17-09a46d08116e) | ![screenshot-6](https://github.com/user-attachments/assets/3ad62e38-d990-4a02-a925-2dae41ea1c66) | ![screenshot-7](https://github.com/user-attachments/assets/260f790c-855e-4901-89f5-b67c83c0a059) | ![screenshot-8](https://github.com/user-attachments/assets/417f3730-0f20-4d46-a20f-8ca1a4f399cc) |

---
# Tài khoản 
Tài khoản Admin mặc định được cung cấp trong CSDL:
- admin@admin.com
- 123123
Ghi chú: Nhiều tài khoản khác được cấp sẵn trong CSDL cũng có mật khẩu là 123123.

# Thư mục tổ chức đồ án:
```
3S eShop/
 │
 ├── BLL/						Tầng logic nghiệp vụ.
 │   ├── DTOs/					Thư mục chứa các lớp đối tượng lưu trữ thuộc tính dữ liệu
 │   │   ├── BaseDTO.cs			Interface cơ bản của lớp đối tượng, các lớp đối tượng cần implements interface này.
 │   │   └── *DTO.cs			Các lớp đối tượng lưu trữ thuộc tính dữ liệu, dùng để truyền dữ liệu.
 │   └── *BLL.cs				Các lớp chứa logic nghiệp vụ, được gọi bởi lớp UI. Là trung gian giữa tầng UI và truy cập dữ liệu.
 ├── CustomControls/			Thư mục chứa các Control tùy chỉnh.
 │   └── *.cs					Các control tùy chỉnh.
 ├── DAL/						Tầng truy cập dữ liệu.
 │   ├── DAOs/					Thư mục chứa các lớp trừu tượng để truy cập dữ liệu từ CSDL.
 │   │   ├── ICrusRepository.cs	Interface chuẩn chứa các phương thức tối thiểu cần cài đặt trên các đối tượng dữ liệu khác nhau
 │   │   └── *DAO.cs			Các lớp truy cập dữ liệu, tương tác trực tiếp đến lớp kết nối CSDL, cần implements interface trên.
 │   └── Database/				Thư mục chứa các lớp tạo kết nối đến CSDL và các hàm xử lý dữ liệu ở mức thô sơ nhất.
 │       └── *.cs				Các lớp tạo kết nối đến CSDL (MySQL, SQL Server, Redis).
 ├── GUI/						Tầng giao diện.
 │   └── *						Các lớp và file giao diện.
 ├── Other/						Thư mục chứa các lớp và file chưa rõ phân loại (nếu có).
 │   └── *						Các lớp và file chưa rõ phân loại (nếu có).
 ├── PatternDistinctive/		Thư mục chứa các lớp đặc thù của mẫu thiết kế.
 │   └── */*					Các lớp đặc thù của từng mẫu thiết kế được lưu tại đây trong từng folder có tên của mẫu thiết kế.
 ├── Resources/					Thư mục chứa tài nguyên phần mềm.
 │   └── *						Các file tài nguyên tĩnh của phần mềm.
 ├── Utilities/					Thư mục chứa các các tiện ích.
 │   └── *.cs					Các file và lớp tiện ích.
 └── *							Các file thư mục khác.
```

---
# Trích nguồn & đóng góp của tác giả
## 1. Ảnh tài nguyên, icon

- [Author Attributes](Resources/Author%20Attributes.md)
## 2. Package sử dụng
| Tên Package                                | Phiên bản | Công dụng                                                              | Giấy phép   |
| ------------------------------------------ | --------- | ---------------------------------------------------------------------- | ----------- |
| BouncyCastle.Crypto                        | 2.3.1     | Thư viện mã hóa, cung cấp các thuật toán bảo mật                       | MIT License |
| Microsoft.NETCore.Platforms                | 3.1.0     | Hỗ trợ nền tảng .NET Core, thông tin về kiến trúc phần cứng            | MIT License |
| Microsoft.Win32.Registry                   | 4.3.0     | Truy cập và thao tác Registry của Windows                              | MIT License |
| Microsoft.Windows.Compatibility            | 6.0.0     | Tương thích cho ứng dụng .NET Core trên Windows                        | MIT License |
| Newtonsoft.Json                            | 9.0.1     | Xử lý JSON, serialize và deserialize dữ liệu JSON                      | MIT License |
| System.Data.SqlClient                      | 4.8.3     | Kết nối và thao tác với SQL Server                                     | MIT License |
| System.Security.Cryptography.ProtectedData | 4.3.0     | Mã hóa và giải mã dữ liệu dựa trên Windows Data Protection API (DPAPI) | MIT License |
| System.ValueTuple                          | 4.0.3     | Hỗ trợ kiểu dữ liệu tuple                                              | MIT License |

## 3. Trích dẫn
- Custom Toast Message:
	- https://laptrinhvb.net/bai-viet/devexpress/---Csharp----Hien-thi-thong-bao-Toast-Message-trong-lap-trinh-Winform/956187c4983d410c.html
- Custom Controls by RJ Code Advance:
	- https://www.youtube.com/watch?v=m7Iv6xfjnuw&list=PLwG-AtjFaHdMQtyReCzPdEe6fZ57TqJUs