## SQL injection attack, listing the database contents on non-Oracle databases

Tiếp tục thực hiện inject query vào sau url **' order by 2--** (tới 3 là lỗi) do web load bình thường ta biết được database vẫn có 2 trường.

Tiếp tục truy vấn ra tên cơ sở dữ liệu từng lệnh như trong cheatsheet để xác định cơ sở dữ liệu nào.  

> **' union select version(),NULL--**

![](/imgs/SQL-Injection/22.png?raw=true)

Lab yêu cầu ta phải đăng nhập bằng tài khoản trong bảng user nên ta phải biết bảng user tên là gì trong database
Câu query list tất cả các table trong Postgres: SELECT * FROM information_schema.tables
Nhưng chúng ta không thể select * để lấy tất cả được vì sẽ bị lỗi trên url => cho nên chúng ta sẽ sử dụng các column name đặc biệt trong Postgres.

(https://www.postgresql.org/docs/9.5/infoschema-columns.html)



