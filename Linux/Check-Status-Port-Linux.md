# Kiểm tra trạng thái Port cho CentOs 

- Lệnh ss
```
ss -tuan
```
![a](Image/checkstatusport.PNG)

```
ss -tupln
```
![b](Image/checkstatusport1.PNG)

- Lệnh Nestat

```
netstat -tupln

```
![c](Image/checkstatusport2.png)

- Kiểm tra port TCP đang mở
```
netstat -ltnp
```
![b](Image/checkstatusport3.png)

- Kiểm tra port UDP đang mở
![c](Image/checkstatusport4.png)

