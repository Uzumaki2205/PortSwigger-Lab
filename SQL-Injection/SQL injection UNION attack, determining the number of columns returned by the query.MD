## SQL injection UNION attack, determining the number of columns returned by the query
- Lab này sẽ hướng dẫn chúng ta xác định được số trường của bảng, thì đầu tiên sau khi bấm vào tra cứu 1 loại sản phẩm ta sẽ được thông tin url như sau:

> https://ac6d1f181e6cd76280e840750070009b.web-security-academy.net/filter?category=<tên_loại>

![](imgs/SQL-Injection/1.png?raw=true)

Thử sửa param category lại thành cái gì đó khác thử xem (ở đây mình thử là sondeptrai) và kết quả sẽ hiện lên trên web như này.

![](/imgs/SQL-Injection/2.png?raw=true)

Nhưng nếu đóng chuỗi ở cuối url chúng ta sẽ nhận "internal server error" vì giá trị ‘ không cho phép

![](/imgs/SQL-Injection/3.png?raw=true)

Chúng ta sẽ sử dụng câu query UNION để truy vấn ra tất cả giá trị
Giả sử ta có

```markdown
Table1 gồm
A | B
1 | 2
Table2 gồm
C | D
3 | 4

> Muốn truy vấn ra tất cả các giá trị chúng ta phải sử dụng câu truy vấn như sau:
> SELECT A, B from table 1 UNION SELECT C, D from table2
```

Ở đây chúng ta sẽ sử dụng câu query tương tự để lấy tất cả
Url sử dụng query cuối cùng sẽ là ***https://ac6d1f181e6cd76280e840750070009b.web-security-academy.net/filter?category=sondeptrai%27+UNION+SELECT+NULL,NULL,NULL--***

(Vì chúng ta không biết đó là trường nào nên chúng ta sẽ sử dụng NULL dần tăng lên để xác định có bao nhiu trường trong bảng => Có 3 columns trong bảng)

Thử giá trị NULL tăng lên cho đến khi nào load được trang web (xác định số lượng trường trong bảng bằng số lượng NULL)

![](/imgs/SQL-Injection/4.png?raw=true)
