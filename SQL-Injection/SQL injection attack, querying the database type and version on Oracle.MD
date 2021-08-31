## SQL injection attack, querying the database type and version on Oracle

Lab này đã cho biết sẵn database là Oracle, nhưng vấn đề là chúng ta sẽ không biết bảng tên gì để truy vấn.

Truy vấn NULL, NULL như Lab 1,2 sẽ bị error nên chúng ta sẽ sử dụng câu truy vấn đặc biệt của Oracle

Để truy vấn Database Type chúng ta sẽ sử dụng bảng DUAL (bảng DUAL là bảng có sẵn trong Oracle)

> Tương tự như các schemas của MySQL thì bảng DUAL trong Oracle là 1 bảng giả dùng để truy vấn ra các trị như ngày tháng hệ thống, tính các phép tính, blabla,...

![](/imgs/SQL-Injection/16.png?raw=true)

Khi truy vấn như thế này **' UNION SELECT 'a', 'b' FROM DUAL--** chúng ta sẽ nhận được

![](/imgs/SQL-Injection/15.png?raw=true)

Để select ra được version chúng ta sẽ sử dụng câu lệnh trong [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) là **SELECT banner FROM v$version**

Câu query chúng ta sử dụng sẽ là 

```markdown
**' UNION SELECT banner,NULL FROM v$version--**
```

![](/imgs/SQL-Injection/17.png?raw=true)