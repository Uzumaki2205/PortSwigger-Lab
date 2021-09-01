## CSRF where Referer validation depends on header being present

Description của lab là ***“This lab's email change functionality is vulnerable to CSRF. It attempts to block cross domain requests but has an insecure fallback.”***

> Có nghĩa là dù đã block cross domain nhưng fallback trả về là không an toàn.

Bắt request change email, nếu thay đổi referer thì sẽ bị chặn, còn nếu xóa đi trường referer ta vẫn gửi request đi được (do fallback trả về no-referer).

![](/imgs/CSRF/31.png?raw=true)

Từ đó, ta sẽ tiến hành generate ra csrf form và thêm phần head là **no-referer**

Hoặc có thể thêm head từ Server Exploit là Referrer-Policy: no-referrer

![](/imgs/CSRF/32.png?raw=true)

Exploit từ Server -> Solve

![](/imgs/CSRF/33.png?raw=true)
