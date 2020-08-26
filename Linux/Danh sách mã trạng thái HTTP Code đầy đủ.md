# Danh mục mã trạng thái HTTP

Mã trạng thái HTTP là các số nguyên có ba chữ số. Chữ số đầu tiên được sử dụng để xác định mã trong một danh mục cụ thể nằm trong năm danh mục sau:

- 1XX – Thông tin: Yêu cầu được chấp nhận hoặc quá trình tiếp tục.

- 2XX – Thành công: Xác nhận rằng hành động đã hoàn tất thành công hoặc đã được hiểu.

- 3XX – Chuyển hướng: Client phải thực hiện hành động bổ sung để hoàn thành yêu cầu.

- 4XX – Lỗi từ client chỉ ra rằng yêu cầu không thể hoàn thành hoặc chứa cú pháp sai. Mã lỗi 4xx sẽ hiện ra khi có lỗi từ phía người dùng, chủ yếu là do không đưa ra một yêu cầu hợp lệ.

- 5XX – Lỗi từ phía máy chủ: Cho biết máy chủ không thể hoàn tất yêu cầu được cho là hợp lệ. Khi duyệt web và bắt gặp các lỗi 5xx, bạn chỉ có thể chờ đợi, vì lúc này lỗi xuất phát từ phía máy chủ của dịch vụ web, không có cách nào can thiệp để sửa lỗi ngoài việc ngồi chờ bên máy chủ xử lý xong.

Các ứng dụng hiểu mã trạng thái HTTP không cần phải biết tất cả các mã, nghĩa là mã không xác định cũng có cụm từ chỉ lý do không xác định. Cụm từ này không cho người dùng nhiều thông tin. Tuy nhiên, các ứng dụng HTTP này phải được hiểu là thuộc một trong các danh mục được nêu ở trên.

# Dòng trạng thái HTTP (Mã trạng thái HTTP + Cụm từ chỉ lý do)

| Mã trạng thái  |           Cụm từ chỉ lý do             |                        Giải thích lỗi| 
|-|-|-|
|       100      | Continue                               | Yêu cầu đã được hoàn thành và phần còn lại của tiến trình có thể tiếp tục. |
|       101      | Switching Protocols                               |Khi yêu cầu một trang, trình duyệt có thể nhận được mã trạng thái 101, theo sau là header “Upgrade”, cho thấy máy chủ đang thay đổi sang phiên bản HTTP khác.|
|       102      | Processing                               |  |
|       200      | OK                               | 	Phản hồi tiêu chuẩn cho các yêu cầu HTTP thành công. |
|       201      | Created                               |Khi các trang mới được tạo bởi dữ liệu biểu mẫu đã đăng hoặc bởi tiến trình CGI, đây là dấu hiệu xác nhận rằng trang đó đã hoạt động. |
|       202      | Accepted| Yêu cầu của client đã được chấp nhận, nhưng chưa được xử lý. |
|       203      | Non-Authoritative Information                              | Thông tin chứa trong tiêu đề thực thể không phải từ trang web gốc, mà là từ máy chủ của bên thứ ba. |
|       204      | No Content                               | Nếu nhấp vào một liên kết không có URL mục tiêu, phản hồi này được máy chủ suy ra và không cảnh báo người dùng về bất cứ điều gì. |
|       205      | Reset Content                               | Điều này cho phép máy chủ reset lại bất kỳ nội dung nào được CGI trả về.|
|       206      | Partial Content                               | Các file được yêu cầu không được tải xuống hoàn toàn. Ví dụ, mã trạng thái này xuất hiện khi người dùng nhấn nút dừng trước khi trang được load. |
|       207      | Multi-Status                               | Yêu cầu đã được hoàn thành và phần còn lại của tiến trình có thể tiếp tục. |
|       300      | Multiple Choices                               |Địa chỉ được yêu cầu đề cập đến nhiều hơn một file. Tùy thuộc vào cách máy chủ được cấu hình, bạn sẽ gặp lỗi hoặc được lựa chọn trang nào mong muốn. |
|       301      | Moved Permanently                               | Nếu máy chủ được thiết lập đúng cách, nó sẽ tự động chuyển hướng người đọc đến vị trí mới của file. |
|       302      | 	Found                               | Trang đã được di chuyển tạm thời và URL mới có sẵn. Bạn sẽ được máy chủ điều hướng đến đó. |
|       303      | See Other                               | Dữ liệu ở một nơi khác và phương thức GET được sử dụng để truy xuất nó. |
|       304      | Not Modified                               | Nếu header yêu cầu bao gồm tham số ‘if modified since’, mã trạng thái này sẽ được trả về, trong trường hợp file không thay đổi kể từ ngày đó. |
|       305      | Use Proxy                               | 	Người nhận dự kiến sẽ lặp lại yêu cầu thông qua proxy. |
|       307      | Temporary Redirect                               | Yêu cầu đã được hoàn thành và phần còn lại của tiến trình có thể tiếp tục. |
|       308      | Permanent Redirect	                               | Yêu cầu đã được hoàn thành và phần còn lại của tiến trình có thể tiếp tục. |
|       400      | 	Bad Request                               |Có một lỗi cú pháp trong yêu cầu và yêu cầu bị từ chối. |
|       401      | 	Unauthorized                               |Header yêu cầu không chứa mã xác thực cần thiết và client bị từ chối truy cập. |
|       402      |Payment Required                               | Việc thanh toán là bắt buộc. Code này vẫn chưa hoạt động. |
|       403      | Forbidden                               | 	Client không được phép xem một file nhất định. Mã trạng thái này cũng được trả lại vào những thời điểm mà máy chủ không muốn có thêm khách truy cập. |
|       404      | 	Not Found                               | 	Các file được yêu cầu không có trên máy chủ. Có thể bởi vì những file này đã bị xóa, hoặc chưa từng tồn tại trước đây. Nguyên nhân thường là do lỗi chính tả trong URL. |
|       405      | Method Not Allowed                               | Phương pháp đang sử dụng để truy cập file không được cho phép. |
|       406      | Not Acceptable                               | File được yêu cầu tồn tại nhưng không thể được sử dụng, vì hệ thống client không hiểu định dạng mà file được cấu hình. |
|       407      | Proxy Authentication Required                               | Yêu cầu phải được cho phép trước khi diễn ra. |
|       408      | Request Time-out                               | Máy chủ mất quá nhiều thời gian để xử lý yêu cầu. Lỗi này thường gây ra bởi lưu lượng truy cập mạng cao. |
|       409      | Conflict                               | Quá nhiều yêu cầu đồng thời cho một file. |
|       410      | Gone                               | Các file đã được sử dụng ở vị trí này, nhưng không còn nữa. |
|       411      | 	Length Required                               | Yêu cầu thiếu header Content-Length. |
|       412      | 	Precondition Failed                               |Một cấu hình nhất định được yêu cầu để chuyển file này, nhưng client chưa thiết lập cấu hình đó. |
|       413      | 	Request Entity Too Large                             | Các file được yêu cầu là quá lớn để xử lý. |
|       414      | 	Request-URI Too Large                               | Địa chỉ đã nhập quá dài cho máy chủ. |
|       415      | Unsupported Media Type                               | Loại file của yêu cầu không được hỗ trợ.|
|       416      | Request Range Not Satisfiable                               | |
|       417      | 	Expectation Failed	                             | |
|       421      | 	Misdirected Request                               | |
|       422      | Unprocessable Entity                               | |
|       423      | 	Locked                               |  |
|       424      | 	Failed Dependency	                               |  |
|       425      | Unordered Collection                               | |
|       426      | Upgrade Required                               ||
|       428      | 	Precondition Required                               |  |
|       429      | 	Too Many Requests	                              ||
|       431      | 	Request Header Fields Too Large                               | |
|       451      | 	Unavailable For Legal Reasons                               | |
|       500      | Internal Server Error                               |Phản hồi khó chịu thường xảy ra do sự cố trong code Perl, khi chương trình CGI, suPHP chạy. |
|       501      | Not Implemented| Yêu cầu không thể được máy chủ thực hiện. |
|       502      | 	Bad Gateway                               |	Máy chủ cố truy cập đang gửi lại lỗi.|
|       503      | 	Service Unavailable                               |Service hoặc file đang được yêu cầu hiện không có sẵn.|
|       504      | Gateway Time-out                               |Cổng đã hết thời gian. Giống như 408 timeout error, nhưng lỗi này xảy ra tại cổng của máy chủ. |
|       505      | HTTP Version Not Supported                            |Giao thức HTTP yêu cầu không được hỗ trợ.|
|       506      | Variant Also Negotiates                               |  |
|       507      | 	Insufficient Storage                             ||
|       508      | Loop Detected                               | |
|       510      | Not Extended                            | |
|       511      | Network Authentication Required	                               | |

# Dòng trạng thái HTTP không chính thức

Các dòng trạng thái HTTP bên dưới có thể được dùng để phản hồi lỗi trong một số dịch vụ của bên thứ ba, nhưng không được chỉ định bởi bất kỳ RFC nào (RFC là viết tắt của Request For Comment, là tập hợp những tài liệu về kiến nghị, đề xuất và những lời bình luận liên quan trực tiếp hoặc gián tiếp đến công nghệ, nghi thức mạng INTERNET).

| Mã trạng thái  |           Cụm từ chỉ lý do             |                        Giải thích lỗi| 
|-|-|-|
|       103      | Checkpoint                               |  |
|       420      | Method Failure                              ||
|       420      | 	Enhance Your Calm                               |  |
|       440      | Login Timeout                               |  |
|       449      | 	Retry With                               ||
|       450      | 	Blocked by Windows Parental Controls                              ||
|       451      | Redirect                               |  |
|       498      | 	Invalid Token                               ||
|       499      | Token Required                               |  |
|       499      | Request has been forbidden by antivirus                               ||
|       509      | Bandwidth Limit Exceeded                               |  |
|       530      | 	Site is frozen                               | |

## Node: Cần nhớ là nhiều mã trạng thái HTTP có thể cùng có một thông báo lỗi giống nhau ở các hoàn cảnh khác nhau, như với mã lỗi Device Manager, nhưng những trường hợp này không hề liên quan đến nhau.