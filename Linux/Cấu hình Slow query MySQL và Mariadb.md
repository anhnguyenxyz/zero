# Enable Slow query Log for Mysql or MariaDb


### -  Enable Slow query MySQL® hoặc MariaDB có thể là một công cụ hữu ích để chẩn đoán các vấn đề về hiệu suất và hiệu quả ảnh hưởng đến máy chủ.

 ### - Bằng cách xác định các truy vấn đặc biệt chậm trong quá trình thực thi của chúng, bạn có thể giải quyết chúng bằng cách cấu trúc lại ứng dụng kích hoạt các truy vấn.

## Bật Low Query Log

### 1. Chúng ta SSH vào server với quyền root
### 2. Mở file my.cnf 
```
vi /etc/my.cnf
```
Chỉnh sửa text như bên dướivà lưu file
```
slow_query_log = 1
long_query_time = 1
slow_query_log_file = /var/log/mysql/slow-query.log
log_queries_not_using_indexes
```

Note:
Từ SQL 5.6 trở lên , hãy sử dụng **log-slow-queries** thay cho biến **slow-query_log_file**.

### 3. Tạo file /var/log/mysql-slow.log và cài đặt sử dụng mysql
```
touch /var/log/slow-query.log
chown mysql:mysql /var/log/slow-query.log
```
### 4. Restart MySQL or MariaDB
```
sudo /etc/init.d/mysql restart
hoặc
sudo systemctl restart mysql
hoặc
sudo systemctl restart mysqld
```
### 5. Bắt đầu monitoring slow query logfile. Phân tích file, chạy lệnh " mysqldumpslow ". Ví dụ chúng ta muốn hiển thị tất cả các bản ghi Slow query:
```
mysqldumpslow -a /var/log/slow-query.log
```
View slow query
```
sudo tail -f /var/log/mysql/slow-query.log
```


Chúc các bạn thành công!