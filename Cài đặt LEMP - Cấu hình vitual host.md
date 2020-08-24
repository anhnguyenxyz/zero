# Install LEMP - Vitual host for CentOS 7

# **Mục Lục**
## I. LEMP là gì?
## II. Install LEMP
## III. Vitual host

#I. LEMP là gì?

**LEMP** : là chữ viết tắt thường được dùng để chỉ sự sử dụng các phần mềm Linux, Nginx, MySQL/MariaDB và PHP/PHP-FPM để tạo nên một môi trường máy chủ Web giúp triển khai các website trên môi trường Internet.

#II. Install LEMP

- Update OS CentOS 7
```yum install update
```

##1. Install nginx

' yum install epel-release -y  
  yum install nginx -y'

Sau khi cài đặt xong nginx chúng ta tiến hành Start nginx
'systemctl start nginx'

Kiểm tra trạng thái của nginx
'systemctl status nginx'
```Output:
    ● nginx.service - A high performance web server and a reverse proxy server
    Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
    Active: active (running) since Fri 2018-07-01 16:08:19 UTC; 1 days ago
    Docs: man:nginx(8)
    Main PID: 2369 (nginx)
    Tasks: 2 (limit: 1153)
    CGroup: /system.slice/nginx.service
        ├─2369 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
        └─2380 nginx: worker process
  ```      

Cho phép nginx khởi động cùng OS

```
systemctl enable nginx
```

Cấu hình firewall cho phép HTTP và HTTPS

```
firewall-cmd --zone=public --permanent --add-service=http
 firewall-cmd --zone=public --permanent --add-service=https
 firewall-cmd --reload
  ```
Chúng ta có thể kiểm tra kết quả trên trình duyệt
```
http://IP máy chủ nginx của bạn
```


##2.  Install Mariadb

Cài đặt mariaDB
```
yum install mariadb-server mariadb -y
```

Start mariadb
```
systemctl start mariadb
```

Cho phép mariaDb khởi đông cùng OS
 ```
 systemctl enable mariadb'
```
Cấu hình mariaDb
```
mysql_secure_installation'
```
```
1.	The next prompt will ask if you want to set a root password. Enter Y and follow the instructions:
2.	Enter current password for root (enter for none):
3.	OK, successfully used password, moving on…
4.	
5.	Setting the root password ensures that nobody can log into the MariaDB
6.	root user without the proper authorization.
7.	
8.	New password:
9.	Re-enter new password:
10.	Password updated successfully!
11.	Reloading privilege tables..
... Success!

```
Chọn Yes các mục sau
```
Remove anonymous users? [Y/n]
Disallow root login remotely? [Y/n]
Remove test database and access to it? [Y/n]
Reload privilege tables now? [Y/n]

```
##3. Cài đặt PHP73

Download và cài đặt các gói repository
```
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm
```
Cho phép PHP 73
```
yum install yum-utils -y
yum-config-manager --enable remi-php73
```
Cài đặt các gói PHP
```
      yum --enablerepo=remi,remi-php73 install php-fpm php-common
```
Cài đặt module PHP
```
      yum --enablerepo=remi,remi-php73 install php-opcache php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml
```
##4. Cấu hình Nginx với php

- Tạo mới cà cấu hình file
```
vi /etc/nginx/conf.d/default.conf
```
Copy và paste nội dung sau vào file

```
server {  
    listen   80;
    server_name  SERVER_IP_OR_DOMAIN;

    # note that these lines are originally from the "location /" block
    root   /usr/share/nginx/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}

```
#### Chú ý : Thay thế your_server_ip với IP server của bạn.
- Sau khi lưu file cấu hình, restart nginx
```
systemctl restart nginx
```
- Cấu hình PHP-FPM
```
nano /etc/php-fpm.d/www.conf
```
Tìm các dòng sau và thay đổi:
```
user = apache to user = nginx
group = apache to group = nginx
listen.owner = nobody to listen.owner = nginx
listen.group = nobody to listen.group = nginx
```
- Đổi listen = 127.0.0.1:9000
```
listen = /var/run/php-fpm/php-fpm.sock
```

- Start PHP-FPM
```
systemctl start php-fpm.service
systemctl enable php-fpm.service
```
#III. Vitual host
##1. Cấu hình /var/www/
- Tạo thư mục chứa dữ liệu website1.com
```
sudo mkdir -p  /var/www/website1.com/public_html
```
- Phân quyền cho thư mục public_html
```
sudo chmod -R 755 /var/www/website1.com/public_html
```
-  Tạo file web page cho website1.com
```
sudo nano /var/www/example.com/public_html/index.html
```
- Sau đó tạo nội dung cho page
```
<html>
  <head>
    <title>Sample web page on website1.com website</title>
  </head>
  <body>
    <h1>Nginx server block 1</h1>
    This sample web page confirms that the first Nginx virtual host 
   or server block is working for example.com
  </body>
</html>
```
Lưu file.
Làm tương tự với website 2

##2. Tạo virtual host file với định đạng .conf

- Website 1
```
sudo nano /etc/nginx/conf.d/website1.com.conf
```
- Sau đó copy nội dung sau vào file
```
server {
    listen  80;
    server_name website1.com;
    location / {
        root  /var/www/website1.com/public_html;
        index  index.html index.htm;
    }
    error_page  500 502 503 504  /50x.html;
    location = /50x.html {
        root  /usr/share/nginx/html;
    }
}
```
- Làm tương tự với website 2

- Restart Nginx web server
```
systemctl restart nginx
```
###3. Tiến hành kiểm tra
- Kiểm tra kết quả qua trình duyệt windows, ta cần chỉnh sửa file host

Mở file host theo đường dẫn sau
```
C:\Windows\System32\drivers\etc\hosts
```
- Thêm nội dung vào file host
```
IP máy chủ nginx website1.com
IP máy chủ nginx website2.com
IP máy chủ nginx website3.com
```
Kiểm tra kết quả trên trình duyệt.
Chú ý tiến hành ping tới từng website để xác minh tất cả có chung 1 địa chỉ IP Nginx server hay không.

Chúc các bạn thành công





