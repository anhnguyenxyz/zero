# Tìm hiểu về SSH Key
- SSH Keys là một phương thức xác thực đăng nhập với máy chủ thông qua truy cập SSH bằng việc đối chiếu giữa một cặp keys (Private và Public Key)
# I. SSH key là gì
# II. SSH có những thành phần nào
# III. Nguyên tắc hoạt động của SSH key
# IV. Cách tạo SSH Key
# V. Cách upload public key lên server

# I. SSH Key là gì?
- SSH Keys là một phương thức xác thực đăng nhập với máy chủ thông qua truy cập SSH bằng việc đối chiếu giữa một cặp keys, bao gồm một khóa riêng tư (private key) và khóa công khai (public key) tương ứng. SSH Keys sử dụng giao thức xác thực hỏi và trả lời trong đó một bên trình bày một câu hỏi và một bên khác phải cung cấp một câu trả lời hợp lệ để được chứng thực.

- Thông thường, một người dùng đăng nhập VPS thông qua username root và password của user đó. Người dùng có thể mất quyền truy cập VPS nếu bị quên hoặc để lộ mật khẩu hay bị dò tìm mật khẩu qua Brute Force Attack. Do đó, việc sử dụng SSH Keys sẽ bảo mật hơn rất nhiều so với phương pháp đăng nhập dùng mật khẩu truyền thống.

- Một cách đơn giản ta có thể so sánh Private Key như là chìa khóa còn Public Key là ổ khóa.

# II. Các thành phần của SSH Key

### - Khi tạo ra một SSH Key , nó bao gồm 3 thành phần: 
- Public Key : Bạn sẽ copy ký tự key này sẽ bỏ vào file ~/.ssh/authorized_keys trên server của bạn.

- Public Key : Bạn sẽ lưu file này vào máy tính, sau đó sẽ thiết lập phiên ssh sử dụng key này để có thể login.

- Keypharse : Mật khẩu để mở private key, khi đăng nhập vào server nó sẽ hỏi cái này (Nếu không đặt pass cho private key thì có thể bỏ qua).

# III. Nguyên tắc hoạt động của SSH Key.
- Private key và Public key luôn có liên hệ chặt chẽ với nhau để nó có thể nhận diện lẫn nhau. Khi tạo một SSH Key thì người dùng sẽ có cả 2 loại key này. 
- Sau đó người dùng mang public key upload lên máy chủ của mình, còn cái private key của người dùng sẽ lưu ở máy và khi đăng nhập vào server, người dùng sẽ gửi yêu cầu đăng nhập kèm theo cái Private Key này để gửi tín hiệu đến server, server sẽ kiểm tra xem cái Private key của người dùng có khớp với Public key có trên server hay không, nếu có thì bạn sẽ đăng nhập được.

# IV.  Tạo SSH KEY
## 1. Windows
- Chúng ta sử dụng Puty-Gen.
Click vào nút : Generate

![SSHKey-Win](Image/SSH-Key-Window.PNG)

- Sau khi click vào genarate bạn di chuyển chuột quanh màn hình để tạo key.Sau khi tạo key xong ta click vào Save private key như hình bên dưới để lưu lại private key được tạo ra.

![SShKey-Win1](Image/SSH-Key-Window1.PNG)

- Sau đó ta lưu lại đoạn public key ra một file với nội dung copy đoạn mã như ảnh bên dưới.
![SSHkey-Win2](Image/SSH-Key-Window2.PNG)

## 2. Linux
- Trên server Linux chạy lệnh ssh-keygen -t rsa
- Sau khi bạn chạy lệnh trên màn hình sẽ hiện ra thông báo hiển thị đường dẫn lưu key được tạo ra, mặc định key public và private sẽ được lưu trong đường dẫn /root/.ssh/ (Trong bước này bạn có thể đặt pass cho private key nếu cần).
![SSHLINUX](Image/SSH-Key-Linux.PNG)

# V. Cách upload public lên server.
## 1. Truy cập SSH từ Windows
![AccSSHWin](Image/Access-SSH-Win.png)
- Ở mô hình này ta có thể upload public key (đã tạo ở phần trên bằng phần mềm putty-gen) lên server bằng cách sử dụng phần mềm winscp, sử dụng SFTP, FTP … Ở ví dụ này chúng ta tạm sử dụng phần mềm Winscp để upload.
- Chúng ta kết nối Winscp tới server linux với các thông tin đăng nhập như Host name (Địa chỉ IP server linux), User nam (root) , Password (password của user root).

![WinSCP](Image/WinSCP.png)

- Khi đã truy cập vào server linux bằng phần mềm winscp, ở khung bên trái giao diện ta tìm tới đường dẫn chứa public_key đã lưu (id_rsa.pub), ở khung bên phải giao diện ta tìm tới đường dẫn /root/.ssh và upload file id_rsa.pub lên sau đó rename file id_rsa.pub thành authorized_keys.

![WinSCPL](Image/SSH-Key-Linux1.PNG)
- Trong ảnh trên nhập thông tin IP của server Linux.

![SSH-Server](Image/SSH2.png)

- Trong ảnh trên ta cần Browse tới đường dẫn chứa file private key (privatekey.ppk) sau đó click vào open để kết nối.

## 2. Truy cập SSH giữa 2 server linux
![SSH2Server](Image/SSH-Server-Server.png)

- Chúng ta sử dụng lệnh copy key giữa 2 server linux như sau,Ví dụ nếu ta muốn copy Key từ server có IP là A lên server có IP là B thì ta ssh vào server A và gõ lệnh.

```
ssh-copy-id -i /root/.ssh/id_rsa.pub B
```
Với B là địa chỉ IP của server B, sau đó hiển thị thông báo nhập password của server B, bạn nhập pass root ssh của server B để copy key hoàn thành nhé.

- Tương tự ta thao tác ngược lại với server A để copy public key từ server B về server A và kết nối ssh từ server B tới server A để kiểm tra.

Chúc các bạn thành công.

Nguồn tham khảo : https://blog.cloud365.vn/other/su-dung-SSH-KEY/

