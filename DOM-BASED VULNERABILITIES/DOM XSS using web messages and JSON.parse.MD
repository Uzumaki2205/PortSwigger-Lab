## DOM XSS using web messages and JSON.parse

> Lab chỉ ra rằng sẽ sử dụng web message là json để show lỗi, chúng ta vẫn phải tìm cách gọi được hàm print() để solve Lab.

![](/imgs/DOM-BASED-VULNERABILITIES/7.png?raw=true)

Check source sẽ thấy được hàm addEventListener, message hình như sẽ được tạo ra từ 1 iframe và parse sang json, rồi từ json mới lấy ra được url để đưa vào src (biến d) nếu type lọt vào case load-channel

![](/imgs/DOM-BASED-VULNERABILITIES/8.png?raw=true)

Cho nên payload chúng ta phải xài sẽ như này

![](/imgs/DOM-BASED-VULNERABILITIES/9.png?raw=true)

```html
<iframe src=https://ac861fce1f2beb8b80840c260057006a.web-security-academy.net/ onload='this.contentWindow.postMessage("{\n\"type\": \"load-channel\",\n\"url\": \"javascript:print()\"\n}", "*")'>
```

Inject đoạn iframe này vào server exploit thì request gửi đúng theo hàm và chạy vào case load-channel để load hàm print() lên.

![](/imgs/DOM-BASED-VULNERABILITIES/10.png?raw=true)

### Tài liệu tham khảo
- DOM-based Vuln: [https://portswigger.net/web-security/dom-based](https://portswigger.net/web-security/dom-based)
- PostMesage to Iframe: [https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)