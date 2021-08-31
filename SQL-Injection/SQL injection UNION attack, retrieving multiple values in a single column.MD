## SQL injection UNION attack, retrieving multiple values in a single column

Từ lab này, chúng ta chúng ta sẽ chuyên nghiệp lên bằng cách làm theo thứ tự xác định có bao nhiêu trường trong bảng trước rồi mới SELECT sau.

### Cách 1:

Chúng ta sẽ sử dụng 1 kỹ thuật khác để xác định số trường mà không phải select nhiều NULL nữa, chã nhẽ bây giờ có 100 trường chúng ta phải select 100 lần NULL :v

Ở đây chúng ta sẽ sử dụng ORDER BY để xác định có bao nhiêu bảng được order by lại
Chúng ta sẽ thử lần lượt từ 1,2,3 xem web bị error ở đâu => kết quả là 3

(Vì không có 3 trường trong bảng nên web sẽ bị error, từ đó ta xác định có 2 trường.)

![](/imgs/SQL-Injection/9.png?raw=true)

Ta bắt đầu sử dụng câu lệnh UNION để nối thêm 1 câu query nữa để SELECT ra các giá trị trong bảng.

Đoạn query đằng sau sẽ là **' UNION SELECT NULL, NULL--**

Chúng ta sẽ thử thay tên trường vào từng chỗ NULL để xem web sẽ load như nào

Khi thử tới đoạn query **' UNION SELECT NULL, ‘son’--** thì web sẽ load như sau (nó đã có thêm 1 hàng nữa ở list product) => chúng ta sẽ select ở trường NULL thứ 2 để lấy ra các data cần tìm.

![](/imgs/SQL-Injection/10.png?raw=true)

Bắt đầu thử dò username (password cũng làm tương tự)
```markdown
**‘ UNION SELECT NULL, username from users--**
```

![](/imgs/SQL-Injection/11.png?raw=true)

### Cách 2:

Ta sẽ xác định cơ sở dữ liệu của đối tượng tấn công sử dụng là gì rồi sẽ sử dụng phép nối chuỗi của cơ sở dữ liệu để select 1 lần ra hết luôn.

Select ra cơ sở dữ liệu của đối tượng bằng cách thử ở trường NULL số 2 các lệnh để show ra tên cơ sở dữ liệu như trong [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet).

Sau khi thử tới **' UNION SELECT NULL, version()--** chúng ta sẽ xác nhận đây là csdl Portgresql

![](/imgs/SQL-Injection/12.png?raw=true)

Chúng ta có thể truy vấn kiểu nối chuỗi để có thể lấy được các dữ liệu cần.

![](/imgs/SQL-Injection/13.png?raw=true)

Áp dụng để truy vấn cả username và password

```markdown
**' UNION SELECT NULL, username || '-' || password from users--**
```

(Ta sẽ nhận được data theo format username-password)

![](/imgs/SQL-Injection/14.png?raw=true)

Chúng ta đã có thể login xác nhận lab thành công.

## Tài liệu
- [SQL CheatSheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)

