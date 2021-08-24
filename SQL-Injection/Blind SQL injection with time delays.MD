## Blind SQL injection with time delays

Ở lab này chúng ta sẽ xác định SQLI bằng time delay.

Tương tự như cách xác định time delay của xss, ta sẽ lợi dụng hàm dùng để set time delay của csdl để set 1 khoảng thời gian trả về data, do đó reponse sẽ trả về lâu hơn.

Thử từng lệnh time delay trong [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet), lệnh nào có thời gian trả về reponse đúng như thời gian đã đặt thì ok.
> **TrackingId=YPzl4f5P3M6JEeMS'||pg_sleep(10)--** (đặt thời gian trả lại là 10s)

Sau đúng 10s, chúng ta sẽ nhận được reponse :v

![](/imgs/SQL-Injection/59.png?raw=true)
![](/imgs/SQL-Injection/60.png?raw=true)

