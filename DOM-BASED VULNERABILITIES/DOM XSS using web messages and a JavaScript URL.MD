## DOM XSS using web messages and a JavaScript URL

> Ở Lab này chúng ta vẫn sẽ trigger 1 web message trên exploit server để throw ra thông báo lỗi.

Web này sử dụng 1 hàm js là addEventListener để lắng nghe sự kiện message và check https và 
http

![](/imgs/DOM-BASED-VULNERABILITIES/3.png?raw=true)

Nếu ta vào bằng http thì sẽ show lỗi như sau:

![](/imgs/DOM-BASED-VULNERABILITIES/4.png?raw=true)

Ta sẽ làm cho web hiện lỗi khi gửi tới targetOrigin (mọi url) là http của hàm postMessage (lab yêu cầu hàm print)

Hàm này vừa chạy web vào sẽ load thông báo in máy in ra

![](/imgs/DOM-BASED-VULNERABILITIES/5.png?raw=true)
![](/imgs/DOM-BASED-VULNERABILITIES/6.png?raw=true)

### Tài liệu tham khảo
- [DOM-based Vuln: ](https://portswigger.net/web-security/dom-based)
- [PostMesage to Iframe: ](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)