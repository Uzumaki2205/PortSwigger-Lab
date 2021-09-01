## CSRF where token is duplicated in cookie

Description nói rằng ***“This lab's email change functionality is vulnerable to CSRF. It attempts to use the insecure "double submit" CSRF prevention technique.”***

=> Lab sẽ sẽ sử dụng 2 cái token trùng nhau để chặn csrf (??? ơ nhưng ai đời lại làm thế)

Nếu bắt request change email và test thử, và nếu chúng ta xóa 1 trong 2 csrf thì POST sẽ lỗi nhưng nếu cả 2 csrf ở cookie và ở param trùng nhau thì sẽ ok.

![](/imgs/CSRF/28.png?raw=true)

Generate ra form csrf và thêm vào thẻ img để set lại cookie trùng với csrf trong form.

![](/imgs/CSRF/29.png?raw=true)

Sau khi exploit xong ta sẽ nhận được email từ session user đang dùng.

![](/imgs/CSRF/30.png?raw=true)