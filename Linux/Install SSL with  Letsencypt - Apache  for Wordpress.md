# Hướng dẫn cài đặt SSL - lensencrypt cho Wordpress - Apache

## - Cài đặt mod_ssl
```
yum -y install mod_ssl
```
## - Định cấu hình Apache
Tạo một thư mục gốc tài liệu cho trang web của bạn:
```
mkdir /var/www/nguyenducanh.xyz
```
Tạo tệp cấu hình máy chủ ảo cho trang web của bạn bằng cách mở tệp đó bằng nano và sau đó dán các nội dung sau vào bên trong:
```
vi /etc/httpd/conf.d/nguyenducanh.xyz.conf
```
Chúng ta điều chỉnh nội dung như bên dưới
```
<VirtualHost *:80>

    ServerAdmin nguyenducanhtud@gmail.com
    
    DocumentRoot "/var/www/html"
    
    ServerName nguyenducanh.xyz
    
    ServerAlias www.nguyenducanh.xyz
    
    ErrorLog "/var/log/httpd/test.error_log"
    
    CustomLog "/var/log/httpd/test.access_log" common

</VirtualHost>
```
- Lưu tệp và thay đổi chủ sở hữu của tệp '/var/www/congphan' thành người dùng Apache để Apache có thể đọc tệp:
```
chown -R apache: apache /var/www/anhnguyen
```
- Để cài đặt certbot, trước tiên chúng ta cần đảm bảo rằng chúng ta đã bật kho lưu trữ EPEL, để thực hiện điều đó, hãy thực hiện lệnh sau:
```
yum -y install epel-release
```
- Đảm bảo rằng yum-utils đã được cài đặt:
```
yum -y install yum-utils
```
- Sau đó cài đặt certbot cho Apache:
```
yum -y install certbot-apache
```
- Bây giờ chúng ta đã cài đặt certbot, hãy chạy certbot bằng lệnh sau:
```
certbot --apache
```
Do cài đặt wordpress ta để source ở thư mục /var/www/anhnguyen, nhưng khi cài đặt lensencrypt ta để thư mục Documentroot là /var/www/html, nên cần chuyển các file từ /var/www/anhnguyen sang /var/www/html bằng câu lệnh sau:
```
cp -ra /var/www/html/* /var/www/anhnguyen/
```
Cấu hình hoàn tất, kiểm tra lại bằng cách truy cấp đường link
```
nguyenducanh.xyz
```
Chúc các bạn thành công!