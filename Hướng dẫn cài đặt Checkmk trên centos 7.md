Ở bài này tôi sẽ chỉ hướng dẫn cách các bạn làm sao để cài đặt được một check_mk server để có thể giám sát hệ thống của riêng bạn.
# Các bước cài đặt
- Cài đặt gói wget
```
yum install wget -y
```
- Khai báo repo
```
yum install epel-release -y
```
- Sử dụng wget để download check_mk
```
wget https://mathias-kettner.de/support/1.5.0p12/check-mk-raw-1.5.0p12-el7-38.x86_64.rpm
```
- Cài đặt check_mk bằng link vừa download
```
yum install check-mk-raw-1.5.0p12-el7-38.x86_64.rpm -y 
```
- Cấu hình firewall và HTTPS
```
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --reload
```
-  Tắt selinux
```
setenforce 0 
```
- Tạo và khởi động site
```
omd create monitoring
omd start monitoring
```
- Đặt mật khẩu cho site
```
su - monitoring
htpasswd -m ~/etc/htpasswd omdadmin
```
- Đăng nhập vào trang web bằng tài khoản admin
```
http://208.100.26.25/monitoring
```
![](Image\check mk.PNG)

Chúc các bạn thành công!