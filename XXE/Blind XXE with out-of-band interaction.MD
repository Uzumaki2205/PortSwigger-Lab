## Blind XXE with out-of-band interaction

> Lab này sẽ chỉ cho chúng ta cách xác định lỗi dạng blind XXE

Ở lab này chúng ta vẫn bắt lại request checkStock
Nếu như chúng ta vẫn xài các cách như ở Lab 1 Lab2 thì sẽ không còn khả thi nữa

![](/imgs/XXE/11.png?raw=true)

> Vậy chắc không có lỗi rồi :v

> À không, đây là dạng blind xxe (có nghĩa lỗi ẩn không thể nhìn thấy được) tương tự như ở XSS.

Khi test thử lỗi ẩn chúng ta sẽ sử dụng phương pháp như đã làm với XSS đó là gửi request đến BurpCollaborator để xác định.

![](/imgs/XXE/12.png?raw=true)

Vẫn invalid như nhau NHƯNG MÀ khi pool request trong BurpCollaborator chúng ta sẽ thấy được có request được gửi đến.

![](/imgs/XXE/13.png?raw=true)

Vậy là solve lab

![](/imgs/XXE/14.png?raw=true)

### Tài Liệu Tham Khảo
- Một số CheatSheet: [https://web-in-security.blogspot.com/2016/03/xxe-cheat-sheet.html](https://web-in-security.blogspot.com/2016/03/xxe-cheat-sheet.html)
