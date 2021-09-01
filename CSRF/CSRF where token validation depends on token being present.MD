## CSRF where token validation depends on token being present

***Function Change Email lần này vẫn bị CSRF, để solve lab thì chúng ta vẫn phải cần change email bằng CSRF attack.***

Vẫn request cũ khi thay đổi csrf thì sẽ lỗi không GET hay POST được

![](/imgs/CSRF/10.png?raw=true)

Ta sẽ giải quyết bằng cách xóa hẳn param csrf luôn, request vẫn được chấp nhận

![](/imgs/CSRF/11.png?raw=true)

Tiếp tục sử dụng CSRF Generate Tool và copy vào Exploit Server, lần này chúng ta sẽ không có csrf nữa.

![](/imgs/CSRF/12.png?raw=true)
![](/imgs/CSRF/13.png?raw=true)
