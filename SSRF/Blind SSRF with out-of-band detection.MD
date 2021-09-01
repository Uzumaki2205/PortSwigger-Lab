## Blind SSRF with out-of-band detection

Lab này sử dụng referer để tham chiếu tới url khi tải trang như phần description, cho nên ta sẽ thay lại thành địa chỉ Burp Collaborator để xác định có request gửi tới không.

![](/imgs/SSRF/21.png?raw=true)

Ta sẽ bắt 1 request có referer và thay đổi thành địa chỉ Burp Collaborator, sau khi pool sẽ solve lab.

![](/imgs/SSRF/22.png?raw=true)
![](/imgs/SSRF/23.png?raw=true)
![](/imgs/SSRF/24.png?raw=true)