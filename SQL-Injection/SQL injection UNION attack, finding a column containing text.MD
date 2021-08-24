## SQL injection UNION attack, finding a column containing text

Vẫn xác định số trường trả lại như Lab 1, nhưng lab này sẽ cho chúng ta 1 giá trị string để SELECT trong query.
Thay giá trị NULL bằng chuỗi string đã cho lần lượt từng vị trí cho đến khi load được web

https://ac091f0d1fd4ba3480018e330031000b.web-security-academy.net/filter?category=Pets’+UNION+SELECT+NULL,’giá_trị_lab_cho’,NULL--

Về cơ bản, lab này giúp chúng ta xác định được trường nào chứa lỗi thôi.

![](imgs/5.png?raw=true)
