## CSRF with broken Referer validation

Đối với lab này nếu thay đổi referer thì sẽ báo lỗi Error (đã được validation) không như các lab trước khi xóa hay sửa vẫn submit bình thường.

Vì thế trong form generate ta sẽ thêm vào trường referer bằng hàm history.pushState theo url của LAB như đã có generate sẵn (có nghĩa là sẽ set lại referer sau khi đã chạy referer đầu tiên).

Thêm vào Head trường Referrer-Policy: unsafe-url

> unsafe-url có thể cho phép gửi đi những url nguyên gốc của domain hoặc subdomain tương tự.

![](/imgs/CSRF/34.png?raw=true)

![](/imgs/CSRF/35.png?raw=true)

Exploit -> Solve

![](/imgs/CSRF/36.png?raw=true)
