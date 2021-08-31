## Basic SSRF against the local server

Đối với lab này, ở phần description có bảo là sẽ lấy data ở internal system (tức là ở phần local).

khi truy cập vào đường dẫn /admin sẽ ra 1 thông báo dưới đây chứng tỏ phải login bằng tài khoản admin hoặc request được gửi từ localhost mới được chấp nhận.

![](/imgs/CSRF/1.png?raw=true)

Ta sẽ tiến hành bắt request checkStock và sẽ thấy là stockApi sẽ gọi tới địa chỉ xyz để lấy ra info của product.

![](/imgs/CSRF/2.png?raw=true)

Vậy nếu ta đổi địa chỉ stockApi lại thành địa chỉ local của trang Admin thì sẽ trả về như sau:

![](/imgs/CSRF/3.png?raw=true)

Search trong sourcecode sẽ có url xóa user như sau
**/admin/delete?username=carlos**

Áp dụng vào param stockApi
**stockApi=http://localhost/admin/delete?username=carlos**

![](/imgs/CSRF/4.png?raw=true)