## CSRF where token validation depends on request method

Description Lab vẫn đề cập tới function change email bị bug CSRF, nhưng mà đã có phương pháp để block tấn công csrf bằng cách thêm 1 token để verify.

Bắt lại request như cũ và check param sẽ có thêm 1 giá trị là **csrf**, giá trị này sẽ generate sau mỗi lần khởi tạo nhằm tránh tấn công **csrf**, nếu thay đổi giá trị này và gửi POST sẽ bị lỗi.

![](/imgs/CSRF/6.png?raw=true)

Chúng ta thay đổi lại phương thức GET, và kết quả vẫn send trả về cùng response như POST dù đã thay đổi csrf => do token không được thực hiện bởi GET mà chỉ được làm ở POST

![](/imgs/CSRF/7.png?raw=true)

Đưa request này sang CSRF Generate Tool và generate ra html, sau đó chúng ta sẽ copy đoạn code đã generate sang Exploit Server và thay đổi lại value email bất kì.

![](/imgs/CSRF/8.png?raw=true)

Sau khi deliver exploit chúng ta sẽ solve lab

![](/imgs/CSRF/9.png?raw=true)