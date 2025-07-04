**Để xem phiên bản Tiếng Việt, vui lòng [truy cập vào đây](README.md).**

3S eShop is a project for the Design Patterns course, including a Winforms software to manage electronic component sales integrated with design patterns.

The project is for academic purposes and internal non-commercial use. For commercial use, please ensure full compliance with copyright for images used and citations in the project.

---
# Team Member Information:

| Member Name       | Student ID | Note |
| ----------------- | ---------- | ---- |
| Đặng Văn Trọng    | Censored   | PM   |
| Nguyễn Thành Tiến | Censored   |      |
| Nguyễn Vĩnh Hưng  | Censored   |      |

---
# Brief Product Information:

- The group's initial product is software to support managing electronic component sales. However, the admin can add categories as desired.
- The main goal of the project is to integrate at least 10 design patterns into the software.
- Features include:
  - Login and register accounts.
  - Custom product search with filters.
  - View product information and place orders without an account.
  - Chat with Customer Service (basic use case is admin account replying).
  - Account management functions (unfinished), category, manufacturer, product management (unfinished), admin order management (not available).
  - Support multiple databases: MySQL, SQL Server (not fully stable yet).
- Technologies applied:
  - Google Cloud API.
  - MySQL database.
  - Distributed Redis database.
  - Simple one-way AES-256 encryption (in production, this would be implemented on the backend).
- The group decided to build a product of moderate scale to apply design patterns, focusing on product workflow. Therefore, the architecture only has the client-side connecting directly to the database and data storage, without a server. The group acknowledges this architecture is extremely insecure because the client needs the secret to operate (by standard, the secret MUST be on the server). However, the product's purpose is to apply operational processes, so this is acceptable for internal use only. For product expansion and production deployment, a separate backend should be built to handle data-related logic.

---
# Instructions to run and continue development:

1. Create a Google Console project:
    - Create an OAuth Client for Desktop applications.
    - Enable DriveAPI.
    - Download `GDriveCredentials.json` and `GOathCredentials.json` files and move them into the `secret_data` folder, overwriting the existing json files.
    - Access the Drive service with the account managed by the Google Console project, create a folder to store the current application's data, copy the folder ID and fill it into the `GDRIVE_FOLDER_ID` key in the `.env` file (inside the `secret_data` folder).
2. Create a MySQL database on any platform (local or hosting):
    - Create schema `3S_eShopDb`.
    - Restore data using the `3S-eShop-MySql-dump.sql` file.
        - Note: This dump file contains some data but excludes image data stored on Google.
    - Fill in the database connection info in the `.env` file:
        - `DB_HOST`: database server address.
        - `DB_PORT`: database port number.
        - `DB_USER`: database user with access rights.
        - `DB_PASS`: database password.
        - `DB_NAME`: database schema name.
        - `DB_CONN`: connection string with structure: `Server=DB_HOST;Port=DB_PORT;Database=DB_NAME;Uid=DB_USER;Pwd=DB_PASS;`
        - `DB_TYPE`: keep as `mysql`.
    - Note: You may switch to SQL Server but compatibility is not fully guaranteed (then set `DB_TYPE` to `sqlserver`).
3. Create a Redis database on any platform, then fill in the access info in the `.env` file:
    - `REDIS_HOST`: Redis server address.
    - `REDIS_PORT`: Redis port number.
    - `REDIS_USER`: Redis access user.
    - `REDIS_PASS`: Redis access password.
4. Open the project in Microsoft Visual Studio and run in Debug or Release mode; the program will automatically load necessary data from the `secret_data` folder to connect to the database and Google Cloud API.

---
# Screenshots

| ![screenshot-1](https://github.com/user-attachments/assets/dd9c8bee-f27b-43ce-89e2-d3f55f4c5fe6) | ![screenshot-2](https://github.com/user-attachments/assets/a6639667-9c9a-4ee4-94f2-63b5821d06d9) | ![screenshot-3](https://github.com/user-attachments/assets/c9a65f2e-64df-49e2-8186-0a23cd45d8ef) | ![screenshot-4](https://github.com/user-attachments/assets/c3a27638-1481-4922-802e-1c0b26c420f9) |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| ![screenshot-5](https://github.com/user-attachments/assets/31373a0b-5404-4112-af17-09a46d08116e) | ![screenshot-6](https://github.com/user-attachments/assets/3ad62e38-d990-4a02-a925-2dae41ea1c66) | ![screenshot-7](https://github.com/user-attachments/assets/260f790c-855e-4901-89f5-b67c83c0a059) | ![screenshot-8](https://github.com/user-attachments/assets/417f3730-0f20-4d46-a20f-8ca1a4f399cc) |

---
# Accounts

Default admin account provided in the database:

- admin@admin.com
- 123123

Note: Many other pre-created accounts in the database also have the password 123123.

---
# Project folder structure:

```
3S eShop/
 │
 ├── BLL/                         Business logic layer.
 │   ├── DTOs/                    Folder containing data attribute storage classes.
 │   │   ├── BaseDTO.cs           Basic interface for data object classes, which must implement this interface.
 │   │   └── *DTO.cs              Data attribute storage classes used for data transfer.
 │   └── *BLL.cs                  Classes containing business logic, called by UI layer. Acts as intermediary between UI and data access layers.
 ├── CustomControls/              Folder containing custom controls.
 │   └── *.cs                     Custom control classes.
 ├── DAL/                         Data access layer.
 │   ├── DAOs/                    Folder containing abstract classes for data access from the database.
 │   │   ├── ICrusRepository.cs   Interface defining minimum required methods for different data objects.
 │   │   └── *DAO.cs              Data access classes interacting directly with database connection classes, implementing the above interface.
 │   └── Database/                Folder containing classes to create database connections and basic data handling functions.
 │       └── *.cs                 Classes for connecting to databases (MySQL, SQL Server, Redis).
 ├── GUI/                         User interface layer.
 │   └── *                        UI classes and files.
 ├── Other/                       Folder for classes and files of unclear classification (if any).
 │   └── *                        Miscellaneous classes and files.
 ├── PatternDistinctive/          Folder containing distinctive classes for design patterns.
 │   └── */*                      Design pattern-specific classes stored in folders named after the pattern.
 ├── Resources/                   Folder containing software resources.
 │   └── *                        Static resource files.
 ├── Utilities/                   Folder containing utility classes.
 │   └── *.cs                     Utility files and classes.
 └── *                            Other files and folders.
```

---
# Credits & Author Contributions

## 1. Resource Images, Icons

- [Author Attributes](Resources/Author%20Attributes.md)

## 2. Packages used

| Package Name                               | Version | Purpose                                                               | License     |
| ------------------------------------------ | ------- | --------------------------------------------------------------------- | ----------- |
| BouncyCastle.Crypto                        | 2.3.1   | Encryption library providing security algorithms                      | MIT License |
| Microsoft.NETCore.Platforms                | 3.1.0   | .NET Core platform support, hardware architecture info                | MIT License |
| Microsoft.Win32.Registry                   | 4.3.0   | Access and manipulate Windows Registry                                | MIT License |
| Microsoft.Windows.Compatibility            | 6.0.0   | Compatibility for .NET Core apps on Windows                           | MIT License |
| Newtonsoft.Json                            | 9.0.1   | JSON processing, serialization and deserialization                    | MIT License |
| System.Data.SqlClient                      | 4.8.3   | Connect and operate with SQL Server                                   | MIT License |
| System.Security.Cryptography.ProtectedData | 4.3.0   | Encrypt and decrypt data based on Windows Data Protection API (DPAPI) | MIT License |
| System.ValueTuple                          | 4.0.3   | Support for tuple data types                                          | MIT License |

## 3. References

- Custom Toast Message:
    - https://laptrinhvb.net/bai-viet/devexpress/---Csharp----Hien-thi-thi-thong-bao-Toast-Message-trong-lap-trinh-Winform/956187c4983d410c.html
- Custom Controls by RJ Code Advance:
    - https://www.youtube.com/watch?v=m7Iv6xfjnuw&list=PLwG-AtjFaHdMQtyReCzPdEe6fZ57TqJUs