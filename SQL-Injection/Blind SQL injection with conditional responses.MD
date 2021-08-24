## Blind SQL injection with conditional responses

Ca này hơi khó nên chúng ta nên dùng BurpSuite nhé :v

Lab có bảo ***“The application uses a tracking cookie for analytics, and performs an SQL query containing the value of the submitted cookie”***

Nôm na có nghĩa là ***web sử dụng tracking cookie để thực hiện truy vấn với giá trị cookie gửi lên***

Để ý kĩ, sử dụng cookie editor chúng ta có thể thấy được, nếu mình xóa tracking id đi thì sẽ không có chữ welcome ở menu, còn để lại thì lại có lại chữ welcome.

![](/imgs/SQL-Injection/34.png?raw=true)
![](/imgs/SQL-Injection/35.png?raw=true)

Chúng ta sẽ thực hiện truy vấn ở tracking cookie này
Bắt bất kì 1 request nào có TrackingId và inject vào 1 đoạn query.

> **TrackingId=WMT4K2EYUiELrvdl'+and+1=1--** có thể hiểu nôm na nghĩa là **select tracking-id from tracking-table where trackingId = ‘WMT4K2EYUiELrvdl’ and 1=1--**
> (1=1 ở vế sau sẽ trả về là True luôn đúng với mọi trường hợp cho nên sẽ trả về có chữ Welcome back)

![](/imgs/SQL-Injection/36.png?raw=true)

Vậy nếu thử 1=0 sẽ luôn sai với mọi trường hợp cho nên sẽ không xuất hiện welcome ở đây nữa

![](/imgs/SQL-Injection/37.png?raw=true)

Chúng ta sẽ bắt đầu select từ bảng users như trong phần description của Lab
Nếu select như này để truy vấn ra user (có nghĩa là nếu đúng thì sẽ trả về có welcome và ngược lại như ở bên trên) 
> **TrackingId=WMT4K2EYUiELrvdl' and (select 'sondeptrai' from users limit 1)='sondeptrai'--** có phải là vế sau sẽ trả về sondeptrai => là luôn đúng

![](/imgs/SQL-Injection/38.png?raw=true)

Nhưng chúng ta sẽ sử dụng để kiểm tra xem admin có tồn tại hay không
> **TrackingId=WMT4K2EYUiELrvdl' and (select username from users where username='administrator')='administrator'--**

Nếu đã học qua SQL cơ bản thì chúng ta sẽ biết nếu đoạn query từ ***(select username from users where username='administrator')*** nếu có user với username là administrator rồi so sánh với đoạn cuối query là ‘administrator’ thì đoạn lệnh này sẽ đúng => sẽ trả về có chữ Welcome

![](/imgs/SQL-Injection/39.png?raw=true)

Vậy có phải là nếu truy vấn đoạn lệnh như sau: 
> **TrackingId=WMT4K2EYUiELrvdl' and (select password from users where username='administrator')=<pass_ở_đây>--** thì vẫn áp dụng như trường hợp ở trên. Nhưng mà password gồm 1 mã hash, đâu phải dống như administrator :v

Trường hợp này chúng ta sẽ bruteforce ra từng chữ cái có trong password (nhưng đầu tiên ta phải xác định được password có chiều dài bao nhiêu đã)
> **TrackingId=WMT4K2EYUiELrvdl' and (select username from users where username='administrator' and LENGTH(password)>1)='administrator'--**

Đoạn query này cũng đoán ra là chúng ta sẽ so sánh thêm 1 trường hợp nữa là chiều dài password nếu mà lớn hơn 1 thì sẽ trả ra kết quả.

Tiến hành bruteforce bằng cách đưa request sang intruder và đặt dấu đô la vào ngay số 1 ($1$) để chúng ta sẽ thay bằng những con số tăng dần nhằm xác định độ dài mà password có thể có. 

![](/imgs/SQL-Injection/40.png?raw=true)

Phần payload chúng ta sẽ dò từ 1->30 và payloadtype sẽ là số

![](/imgs/SQL-Injection/41.png?raw=true)

Start attack khi chạy đến 19 thì length sẽ thay đổi, vì mất chữ welcome back rồi (có thể send lại qua repeater để xem thử).

![](/imgs/SQL-Injection/42.png?raw=true)

Bây giờ ta sẽ biết được password có chính xác 20 kí tự
Ta sẽ sử dụng hàm có sẵn trong sql để so sánh chuỗi.

Đầu tiên sẽ Test thử 1 trường hợp

Hàm substring ai xài qua python chắc cũng biết rồi nhỉ (ví dụ ở bên dưới mình sẽ lấy kí tự đầu của password rồi so sánh với x)
> **TrackingId=43RCZtvUB1HhMJxD'+AND+(SELECT+SUBSTRING(password,1,1)+FROM+users+WHERE+username%3d'administrator')%3d'x'--** (x là để so sánh với chữ cái đầu tiên bằng substring(password,1,1))

Từ đây chúng ta sẽ bruteforce thêm 1 lần nữa để lấy được các chữ cái có trong password

![](/imgs/SQL-Injection/43.png?raw=true)

Payload sẽ chọn bruteforce bằng bảng chữ cái và số

![](/imgs/SQL-Injection/44.png?raw=true)

Chúng ta sẽ thu được 1 request có chiều dài thay đổi và tồn tại Welcome back, chứng tỏ là có kí tự đó là kí tự đầu tiên trong password

![](/imgs/SQL-Injection/45.png?raw=true)

Vậy là yên tâm rồi, chúng ta sẽ xét tới lần bruteforce tiếp theo sẽ cho ra password hoàn chỉnh bằng cách thêm 2 biến đô la vào chỗ substring và chuỗi để so sánh.

Đổi Attack type lại thành Cluster bomb để có thể chọn xem được 2 giá trị payload đã thêm đô la. 
> Payload sử dụng vẫn như cũ nhưng payload set 1 sẽ là number từ 1 đến 20 còn payload set 2 thì như cũ (brute forcer)

![](/imgs/SQL-Injection/46.png?raw=true)
![](/imgs/SQL-Injection/47.png?raw=true)

Sau khi tấn công ta sẽ sắp xếp độ dài từ cao tới thấp và liệt kê ra các giá trị từ 2 payload tương ứng như sau

![](/imgs/SQL-Injection/48.png?raw=true)

Dò muốn mỏi con mắt thì ta được password như ở dưới, xóa khoảng trắng đăng nhập bằng administrator là solve.

1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20

h d p k 5 w s c d j f x 6 l q  k 0 5 n 4

![](/imgs/SQL-Injection/49.png?raw=true)



