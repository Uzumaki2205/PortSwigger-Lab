## SSRF with blacklist-based input filter

Ở lab này nếu sử dụng các value ở param stockApi như các lab trước sẽ bị block đi nên chúng ta sẽ thay bằng 127.1 (có nghĩa là 127.0.0.1)

Hoặc có thể encode bằng Ip Obfuscation

![](/imgs/SSRF/8.png?raw=true)

Xài 1 trong 2 ngay chỗ IP đều được

![](/imgs/SSRF/9.png?raw=true)

Nhưng mà nếu /admin tiếp thì sẽ bị error không load được nữa.

Mình đã tiến hành encode url /admin 2 lần và web sẽ load được bình thường (bởi vì lab này sẽ có blacklist để chặn những url không lệ)

**stockApi=http://127.1/%25%36%31%25%36%34%25%36%64%25%36%39%25%36%65**

![](/imgs/SSRF/10.png?raw=true)
![](/imgs/SSRF/11.png?raw=true)

Ok sửa lại value thành như này là solve lab 

```markdown
**stockApi=http://127.1/%25%36%31%25%36%34%25%36%64%25%36%39%25%36%65/delete?username=carlos**
```

![](/imgs/SSRF/12.png?raw=true)