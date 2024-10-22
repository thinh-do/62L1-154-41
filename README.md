# The Time Sheet

**The Time Sheet** là một ứng dụng web giúp nhân viên quản lý thời gian làm việc thông qua chức năng check-in và check-out. Ứng dụng cung cấp thông báo khi nhân viên thiếu giờ làm việc và hiển thị lịch sử làm việc của nhân viên, bao gồm ngày làm đủ giờ hoặc thiếu giờ.

## Mục lục

1. [Giới thiệu](#giới-thiệu)
2. [Tính năng](#tính-năng)
3. [Cài đặt](#cài-đặt)
4. [Sử dụng](#sử-dụng)
5. [Đóng góp](#đóng-góp)
6. [Giấy phép](#giấy-phép)

## Giới thiệu

**The Time Sheet** giúp nhân viên theo dõi giờ làm việc hàng ngày thông qua tính năng check-in (khi vào làm) và check-out (khi tan ca). Hệ thống sẽ gửi thông báo nếu nhân viên thiếu giờ làm việc và cung cấp lịch để xem ngày nào đã đủ giờ hoặc thiếu giờ.

Ứng dụng được xây dựng với các công nghệ:
- **Ngôn ngữ lập trình**: Java 8
- **Máy chủ ứng dụng**: WildFly 10
- **Cơ sở dữ liệu**: PostgreSQL 14
- **ORM**: Hibernate (Sử dụng để ánh xạ cơ sở dữ liệu với đối tượng Java thông qua ORM)

## Tính năng

- Đăng nhập/Đăng xuất tài khoản nhân viên.
- Check-in khi bắt đầu ca làm việc và check-out khi kết thúc ca.
- Thông báo cho nhân viên nếu thiếu giờ làm.
- Lịch làm việc để kiểm tra số giờ làm trong ngày.
- Quản lý lịch sử giờ làm việc.

## Cài đặt

### Yêu cầu hệ thống:

- Java 8
- WildFly 10
- PostgreSQL 14
- Maven 3.x
- Hibernate (đã tích hợp trong dự án)

### Các bước cài đặt:

1. Clone repo:
    ```bash
    git clone https://github.com/thinh-do/62L1-154-41
    ```

2. Chuyển vào thư mục dự án:
    ```bash
    cd TheTimeSheet
    ```

3. Cấu hình cơ sở dữ liệu PostgreSQL:
    - Tạo một cơ sở dữ liệu mới trong PostgreSQL:
    ```sql
    CREATE DATABASE time_sheet_db;
    ```
    - Tạo người dùng và cấp quyền:
    ```sql
    CREATE USER timesheet_user WITH ENCRYPTED PASSWORD 'password';
    GRANT ALL PRIVILEGES ON DATABASE time_sheet_db TO timesheet_user;
    ```

4. Cập nhật file `src/main/resources/application.properties` với thông tin kết nối PostgreSQL của bạn:
    ```
    spring.datasource.url=jdbc:postgresql://localhost:5432/time_sheet_db
    spring.datasource.username=timesheet_user
    spring.datasource.password=password
    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
    ```

5. Xây dựng và triển khai ứng dụng lên WildFly:
    - Build dự án với Maven:
    ```bash
    mvn clean install
    ```
    - Triển khai tệp `.war` lên WildFly:
    - Copy file `.war` vào thư mục `standalone/deployments` của WildFly hoặc sử dụng giao diện quản lý WildFly.

6. Khởi động WildFly và truy cập trang web:
    ```bash
    ./wildfly-10.1.0.Final/bin/standalone.sh
    ```

## Sử dụng

1. Sau khi khởi chạy ứng dụng trên WildFly, truy cập trang web tại địa chỉ:
    ```
    http://localhost:8080/the-time-sheet
    ```
2. Đăng nhập với tài khoản nhân viên.
3. Sử dụng nút **Check-in** để ghi lại thời gian bắt đầu làm việc và nút **Check-out** để ghi lại thời gian kết thúc.
4. Hệ thống sẽ thông báo cho nhân viên nếu thiếu giờ làm việc trong ngày.
5. Nhân viên có thể xem lịch làm việc để kiểm tra ngày nào đã làm đủ giờ hoặc thiếu giờ.

## Đóng góp

Chúng tôi luôn hoan nghênh sự đóng góp từ cộng đồng. Để đóng góp:

1. Fork dự án này.
2. Tạo một nhánh mới cho tính năng hoặc sửa lỗi của bạn (`git checkout -b tên-nhánh`).
3. Commit thay đổi của bạn (`git commit -m 'Thêm tính năng mới'`).
4. Push lên nhánh của bạn (`git push origin tên-nhánh`).
5. Tạo một Pull Request và mô tả những thay đổi của bạn.

## Giấy phép

Dự án này được cấp phép dưới giấy phép MIT - xem tệp [LICENSE](./LICENSE) để biết thêm chi tiết.
