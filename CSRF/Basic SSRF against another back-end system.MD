## Basic SSRF against another back-end system

Lab này sẽ lấy data từ internal system nhưng sẽ có thay đổi IP như phần desciption.
Ta sẽ bắt lại request checkStock và thay bằng địa chỉ 192.168.0.x

![](/imgs/CSRF/5.png?raw=true)

Ta phải brute ra đó là địa chỉ nào bằng cách đưa sang Intruder và Brute theo từ 1->255 ta sẽ thấy có 1 request status 200 tương ứng với ip 192.168.0.183:8080

![](/imgs/CSRF/6.png?raw=true)

Tiến hành xóa user carlos bằng stockApi=http://192.168.0.183:8080/admin/delete?username=carlos

![](/imgs/CSRF/7.png?raw=true)