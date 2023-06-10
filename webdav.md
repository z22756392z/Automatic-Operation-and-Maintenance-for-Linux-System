[note/連接網路磁碟機.md at master · FUYUHSUAN/note (github.com)](https://github.com/FUYUHSUAN/note/blob/master/110-2自動化運維/2022_02_16/連接網路磁碟機.md)

[當您存取對應至 Web 共用的網路磁碟機機時，使用者尚未通過驗證錯誤 - Windows Client | Microsoft Learn](https://learn.microsoft.com/zh-tw/troubleshoot/windows-client/networking/error-access-network-drive-mapped-web-share)

![image-20230222104244893](./image/image-20230222104244893.png)

[Linux sed 字串取代用法與範例 | ShengYu Talk (shengyu7697.github.io)](https://shengyu7697.github.io/linux-sed/)





## webdev

` yum install epel-release`: dependency (install epel-release package)

`yum install httpd`

```
[root@centos7-1 ~]# yum install epel-release
base                                                     | 3.6 kB     00:00
centos-sclo-rh                                           | 3.0 kB     00:00
centos-sclo-sclo                                         | 3.0 kB     00:00
copr:copr.fedorainfracloud.org:vbatts:bazel              | 3.3 kB     00:00
docker-ce-stable                                         | 3.5 kB     00:00
epel/x86_64/metalink                                     | 7.3 kB     00:00
epel                                                     | 4.7 kB     00:00
extras                                                   | 2.9 kB     00:00
nux-dextop                                               | 2.9 kB     00:00
updates                                                  | 2.9 kB     00:00
zabbix                                                   | 2.9 kB     00:00
zabbix-frontend                                          | 2.9 kB     00:00
zabbix-non-supported                                     | 2.9 kB     00:00
(1/6): zabbix/x86_64/primary_db                            | 221 kB   00:01
(2/6): epel/x86_64/updateinfo                              | 1.0 MB   00:03
(3/6): epel/x86_64/primary_db                              | 7.0 MB   00:13
(4/6): zabbix-frontend/x86_64/primary_db                   |  72 kB   00:15
(5/6): updates/7/x86_64/primary_db                         |  21 MB   00:28
(6/6): docker-ce-stable/7/x86_64/primary_db                | 111 kB   00:34
Package epel-release-7-14.noarch already installed and latest version
Nothing to do

```

`httpd -M | grep dav` : check if supported

```
[root@centos7-1 ~]# httpd -M | grep dav
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 192.168.56.101. Set the 'ServerName' directive globally to suppress this message
 dav_module (shared)
 dav_fs_module (shared)
 dav_lock_module (shared)
```

``mkdir /var/www/html/webdav``: make to be shared directory

`cd /var/www/html/webdav`: 

`echo "hello" > hello.txt` 

``vi /etc/httpd/conf.d/webdav.conf``: config webdav

```
DavLockDB /var/www/html/DavLock
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/webdav/
    ErrorLog /var/log/httpd/error.log
    CustomLog /var/log/httpd/access.log combined
    Alias /webdav /var/www/html/webdav
    <Directory /var/www/html/webdav>
        DAV On
        #AuthType Basic
        #AuthName "webdav"
        #AuthUserFile /etc/httpd/.htpasswd
        #Require valid-user
        </Directory>
</VirtualHost>
```



`systemctl status httpd.service`: to apply the modyied config



open a Windows network drive and connect to a Linux IP address

![image-20230609143128176](C:\Users\z22756392z\AppData\Roaming\Typora\typora-user-images\image-20230609143128176.png)



