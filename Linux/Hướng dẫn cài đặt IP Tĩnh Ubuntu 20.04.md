# Cấu hình IP tĩnh Ubuntu 20.04

- Kiểm tra IP hiện tại của máy
```
networkctl status
```
- Hoặc có thể check IP hiện tại và card mạng đang sử dụng. 
Cài thêm net-tools

```
sudo apt install net-tools
ifconfig
```
- Mở file cấu hình để add ip tĩnh
```
sudo nano /etc/netplan/01-network-manager-all.yaml
```
- Sửa theo mẫu sau:
```
network:
   ethernets:
      enss33:
         dhcp4: no
         dhcp6: no
         adresses: [208.100.26.29/24]
         gateway4: 208.100.26.2
         nameserver:
           adsesses: [8.8.8.8, 8.8.4.4]
    version: 2
```
- Dùng lệnh sau để restart card mạng
```
sudo service network-manager restart
```
Chúc các bạn thành công!

