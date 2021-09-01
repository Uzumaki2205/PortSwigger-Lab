## Blind XXE with out-of-band interaction via XML parameter entities

> Lab này sẽ hướng dẫn chúng ta check được blind XXE qua XML parameter entities

Bắt lại request checkStock và gửi đến BurpCollaborator, chúng ta sẽ nhận được lỗi Enties không cho phép truy cập vào.

![](/imgs/XXE/15.png?raw=true)

Các chữa cháy nhanh nhất là chúng ta sẽ không sử dụng entites ở productId nữa mà sẽ thực thi 1 lần ở bước khai báo luôn.

> Sử dụng payload parameter entities (cú pháp là khai báo biến đầu tiên là % <tên> và ở cuối là %<tên>;)

![](/imgs/XXE/16.png?raw=true)
![](/imgs/XXE/17.png?raw=true)

Tuy báo là parsing error nhưng mà Burp Collaborator có phát hiện request gửi tới

![](/imgs/XXE/18.png?raw=true)
![](/imgs/XXE/19.png?raw=true)

### Tài Liệu Tham Khảo
- Một số CheatSheet: [https://web-in-security.blogspot.com/2016/03/xxe-cheat-sheet.html](https://web-in-security.blogspot.com/2016/03/xxe-cheat-sheet.html)
