## CSRF where token is not tied to user session

Đầu tiên lab đã đề cập đến việc web chỉ xử lý token để chặn csrf mà không quan tâm tới session => các session của các user khác nhau có thể sử dụng qua lại bình thường.

![](/imgs/CSRF/14.png?raw=true)

Ví dụ ở đây mình sẽ login bằng tài khoản wiener và sử dụng token của wiener sử dụng cho user carlos để đổi email.

Bắt 2 request change email của 2 user đưa đến Repeater

![](/imgs/CSRF/15.png?raw=true)
![](/imgs/CSRF/16.png?raw=true)

Mình sẽ sử dụng token của user wiener (k2850 …) để changed email cho user carlos

![](/imgs/CSRF/17.png?raw=true)

Ta có thể thấy có thể sử dụng token của user này sử dụng cho user kia, như trên hình là user carlos đã sử dụng token của user wiener để change email

![](/imgs/CSRF/18.png?raw=true)

Mình sẽ sử dụng 1 request change email mới ở bất kì user nào sẽ sinh ra token khác.

![](/imgs/CSRF/19.png?raw=true)

Sử dụng CSRF Tool để generate ra code và thay bằng token đã thu được trước đó. (Ở đây mình sử dụng lại cái token sOX… của session user carlos trước đó)

![](/imgs/CSRF/20.png?raw=true)
![](/imgs/CSRF/21.png?raw=true)