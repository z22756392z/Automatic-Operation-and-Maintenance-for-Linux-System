## Mail

```
vim /etc/mail.rc
```



```
set smtp-use-starttls
set ssl-verify=ignore
set nss-config-dir=/etc/pki/nssdb/
#設定寄件者信箱
set from=smallko@gmail.com
#設定Gmail_Smtp端口
set smtp=smtp://smtp.gmail.com:587
#設定Gmail_Smtp認證帳號
set smtp-auth-user=xxxx@gmail.com
#設定Gmail_Smtp認證帳號之密碼(請使用Google應用程式密碼)
set smtp-auth-password=xxxxxx
set smtp-auth=login
```



```
echo "hello world" | mail -v -s "Test1234" xxx@abc.com
```

![image-20230609144252520](./image/螢幕擷取畫面 2023-06-09 144256.png)
