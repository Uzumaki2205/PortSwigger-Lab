## SQL injection attack, querying the database type and version on MySQL and Microsoft

Chúng ta sẽ thực hiện kiểm tra số trường trong bảng.

Mình đã thực hiện câu query **‘ Order By 1--** nhưng web trả về error chứng tỏ ở đây cơ sở dữ liệu đã bị thay đổi. Ta sẽ thay dấu comment ở cuối bằng các dấu comment ở các cơ sở dữ liệu khác (và ở lab này là SQLServer hoặc MySQL)

> Thay vì sử dụng -- chúng ta sẽ xài # để comment

![](imgs/18.png?raw=true)

Sau đó ta sẽ xác định lỗi khi hiển thị SELECT sẽ xuất hiện ở đâu (ở cuối)

![](imgs/19.png?raw=true)

Sau khi đã xác định được lỗi hiển thị ở đâu ta tiến hành SELECT version của database (đối với MYSQL hoặc SQLSERVER thì sử dụng @@version như ở [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet))

> **‘ UNION SELECT @@version,NULL#**

![](imgs/20.png?raw=true)

Thay lại url ở web và Solve

![](imgs/21.png?raw=true)





