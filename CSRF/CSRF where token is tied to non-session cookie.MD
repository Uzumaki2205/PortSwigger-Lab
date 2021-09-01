## CSRF where token is tied to non-session cookie

Description của Lab có nói là web sử dụng csrf để chặn tấn công nhưng lại không được xử lý hoàn toàn ở session.

Vẫn bắt 2 request change email của 2 user, ta thấy ngoài token được gửi đi ở param còn có session và csrfkey ở cookie.

![](/imgs/CSRF/22.png?raw=true)

Ở trên là user wiener, còn ở dưới là Carlos

![](/imgs/CSRF/23.png?raw=true)

Ở đây nếu thay đổi session hoặc csrfKey sẽ bị lỗi không gửi được POST

Bây giờ mình sẽ thay 2 cái csrf ở user Carlos thành csrf của user Wiener

![](/imgs/CSRF/24.png?raw=true)

Request vẫn chấp nhận

![](/imgs/CSRF/25.png?raw=true)

Chúng ta sẽ send 1 request change email mới và tạo form CSRF

Ta sẽ tạo ra thêm 1 thẻ img để submit khi csrfKey ở token bị error (cái link ở image là cái link khi search nha + thêm set-cookie là csrf token) thì form sẽ tự động submit.

![](/imgs/CSRF/26.png?raw=true)
![](/imgs/CSRF/27.png?raw=true)

