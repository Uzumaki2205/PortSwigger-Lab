## Blind SSRF with out-of-band detection

Lab này sử dụng referer để tham chiếu tới url khi tải trang như phần description, cho nên ta sẽ thay lại thành địa chỉ Burp Collaborator để xác định có request gửi tới không.

![](/imgs/CSRF/21.png?raw=true)

Ta sẽ bắt 1 request có referer và thay đổi thành địa chỉ Burp Collaborator, sau khi pool sẽ solve lab.

![](/imgs/CSRF/22.png?raw=true)
![](/imgs/CSRF/23.png?raw=true)
![](/imgs/CSRF/24.png?raw=true)