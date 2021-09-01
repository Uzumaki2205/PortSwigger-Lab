## DOM-based open redirection

> Ở phần description lab có nói web này còn tồn tại lỗ hổng DOM-based dạng open redirect, ta phải chuyển hướng sao cho tới exploit server

Khi bấm vào 1 post nào nó check source thì chúng ta sẽ thấy 1 thẻ a dùng để chuyển hướng ngược về post trước (nếu ta đã comment) hoặc là home dựa vào location đang đứng.

```html
<a href='#' onclick='returnUrl = /url=(https?:\/\/.+)/.exec(location); if(returnUrl)location.href = returnUrl[1];else location.href = "/"'>Back to Blog</a>
```

Vì thế ta chỉ cần chèn thêm trên link thêm 1 param là url (trên cái returnUrl của function) là đường link của exploit server là đã redirect được rồi.

```markdown
https://ac791f1a1f6e73d28056ca7d00140090.web-security-academy.net/post?postId=5&url=https://exploit-ac8a1f141fbf73b4808ecad301920020.web-security-academy.net/exploit
```

![](/imgs/DOM-BASED-VULNERABILITIES/11.png?raw=true)

### Tài liệu tham khảo
- DOM-based Vuln: [https://portswigger.net/web-security/dom-based](https://portswigger.net/web-security/dom-based)