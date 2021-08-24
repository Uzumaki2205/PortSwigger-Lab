## Blind SQL injection with out-of-band interaction

Với dạng lab out of band này chúng ta sẽ phải trigger lệnh dùng để DNS tới Burp Collaborator.

Tham khảo [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) chúng ta sẽ nhận được 1 đoạn lệnh như sau dùng trong Oracle (lợi dụng EXTRACT VALUE trong SQL để sử dụng XXE attack để trigger đoạn query lookup DNS)

(https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions052.htm)

![](/imgs/SQL-Injection/66.png?raw=true)

Mở Burp collabor copy link vào YOUR-SUBDOMAIN-HERE

![](/imgs/SQL-Injection/67.png?raw=true)

Sau khi send request và pool xuống chúng ta sẽ nhận được các request được được gửi tới Burp Collabor

![](/imgs/SQL-Injection/68.png?raw=true)
![](/imgs/SQL-Injection/69.png?raw=true)