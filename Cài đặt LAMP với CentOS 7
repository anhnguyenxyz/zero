Mục lục
# I. LAMP là gì?
# II. Cài Đặt LAMP

# I.  LAMP là gì?
**LAMP** bao gồm :
Linux + Apache + MySQL + PHP.

- Linux: Linux là một hệ điều hành. 
Về mặt nguyên tắc hệ điều hành cũng là một software,
nhưng đây là một software đặc biệt được dùng để quản lý,
điều phối các tài nguyên (resource) của hệ thống (bao gồm cả hardware và các software khác).
Linux còn được gọi là Open Source Unix (OSU).

- Apache: là phần mềm máy chủ web phổ biến nhất trên mạng.
Nó rất an toàn, nhanh chóng, và đáng tin cậy.
Chúng ta có thể tùy chỉnh để Apache hỗ trợ các ngôn nhữ web khác nhau như PHP, CGI / Perl, SSL, SSI, ePerl, và thậm chí ASP.

- MySQL là hệ quản trị cơ sở dữ liệu nhanh nhất trên thế giới,
nó trở thành cơ sở dữ liệu nguồn mở phổ biến nhất trên thế giới vì hiệu suất cao,
độ tin cậy cao và dễ sử dụng. Nó rất tốt cho các ứng dụng dựa trên web.
Rất nhiều các công cụ hỗ trợ đã được phát triển cho MySQL với PHP,
chẳng hạn như phpMyAdmin là một công cụ quản trị web rất tốt cho MySQL, 
và giúp bạn có thể làm bất cứ điều gì mà bạn mong muốn với MySQL.

- PHP được phát triển như là một ngôn ngữ kịch bản trên máy chủ (server-side scripting language).
Nó được phát triển bởi Rasmus Lerdorf, và những người khác.
Hiện tại, các phiên bản của nó có nhiều lợi thế hơn các đối thủ cạnh tranh như ASP, Cold Fusion, Perl, Java,... 
chẳng hạn như về hướng đối tượng và khả năng nhúng vào ngôn ngữ HTML được xử lý rất nhanh,
tương thích với nhiều nền tảng hệ điều hành, hoạt động như một thành phần của Apache. 
Nó được cập nhật liên tục các kỹ thuật mới bằng cách vay mượn những tính năng tốt nhất từ nhiều ngôn ngữ lập trình khác.

# II. Cài đặt LAMP
 ## 1 . Cài đặt Apache
 - Cài cài đặt LAMP
 ```
 sudo yum -y install httpd
 ```
- Cài xong, tiến hành khởi động lại service:
```
systemctl start httpd
systemctl enable httpd
```
- Check li trang thái hoạt động của service:
```
systemctl status httpd
```
-  Kiểm tra kết quả trên trình duyệt

```
IP máy chủ LAMP của bạn
```

## 2. Cài đặt MariaDb
```
yum -y install mariadb mariadb-server
```
- Khởi động mariadb:
```
systemctl start mariadb
```
-  Cài đặt secure cho mariadb
```
mysql_secure_installation
```
Enter currret password for root (enter for none): enter

- Chọn Yes các mục sau:
```
Set root password? (Y/n)
Disablow root login remotely (Y/N)
Remove test database and access to it? (Y/N)
Reload privilege tables now (Y/N)
```
- Cho phép mariadb khởi động cùng OS
```
systemctl enable mariadb
```
## 3.Cài đặt PHP

- Update gói repo của CentOS
```
rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
- Cài yum-utils vì chúng ta cần tiện ích yum-config-manager để cài đặt:
```
sudo yum install php php-mysql
```
- Khởi động Apache
```
sudo systemctl restart httpd.service 
```
## 4. TEST PHP 
- Sử dụng PHP cơ bản script trong info.php
```
vi /var/www/html/info.php
```
- Chuyển nội dung sau vào file và lưu
```
<?php

phpinfo ();

?>

```
- Kiểm tra PHP đã làm việc chưa
```
http//IP_của bạn/info.php
```
- Cấu hình firewall cho phép HTTP và HTTPS
```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload	
```


Chúc các bạn thành công!