## Zabbix

Zabbix is an open-source network monitoring and management tool. It is designed to monitor and track the performance and availability of network services, servers, applications, and other IT resources. Zabbix provides a centralized platform for collecting, analyzing, and visualizing data from various devices and systems.



## Installation

server

[Centos7系统安装Zabbix 5.0LTS版本教程 - 腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1943154)

mydatabase password:your_zabbix_mysql_password



client

[Install and Configure Zabbix agent 5 on CentOS 7 | ComputingForGeeks](https://computingforgeeks.com/install-and-configure-zabbix-agent-on-centos/)

when create host to be montiered in server the template option select Template OS Linux by Zabbix agent



## Command

##### setup database

`yum install mariadb-server mariadb -y`: install Maria DB

`systemctl start mariadb`

`mysql_secure_installation`: setup config

`mysql -u root -p`

![image-20230609144648516](./image/螢幕擷取畫面 2023-06-09 144644.png)

`create database zabbix_db character set utf8 collate utf8_bin;`: setup database for zabbix to use called zabbix_db

`create user zabbix@localhost identified by 'password';`: create the user

`grant all privileges on zabbix_db.* to zabbix@localhost;`: grant the all privileges to zabbix_db

`quit`: exit



##### setup zabbix

https://www.zabbix.com/

![](./image/螢幕擷取畫面 2023-06-09 144842.png)

[Centos7系统安装Zabbix 5.0LTS版本教程-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1943154)

`yum install zabbix-server-mysql zabbix-agent -y`

`yum install centos-release-scl -y`

`vim /etc/yum.repos.d/zabbix.repo`: enable zabbix front end

```
[zabbix-frontend]
...
enabled=1
...
```



`yum install zabbix-web-mysql-scl zabbix-apache-conf-scl -y`

`zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix_db`: copy mysql data base to zabbix server database

`vim /etc/zabbix/zabbix_server.conf`: change the database config for zabix server to link

```
DBName=zabbix_db    
DBUser=zabbix       
DBPassword=password 
```

`vim /etc/opt/rh/rh-php72/php-fpm.d/zabbix.conf`: modify timezone

to

`php_value[date.timezone] = Asia/Taipei`

`systemctl restart zabbix-server zabbix-agent httpd rh-php72-php-fpm`: restart server

open browser connect to vm ip address ex:

[centos7-1: Zabbix](http://192.168.56.101/zabbix/)

![image-20230609154454889](./image/螢幕擷取畫面 2023-06-09 154447.png)



>  if forget password

> [解决：Zabbix密码忘记不要慌，一招教你搞定_胖胖不胖、的博客-CSDN博客](https://blog.csdn.net/yeyslspi59/article/details/128215418#:~:text=解决：Zabbix密码忘记不要慌，一招教你搞定 1 [root %40SJYS -Test1 ~] %23 mysql,MariaDB monitor. Commands end with %3B or \g.)

>  change linked mariadb user data



![image-20230609154454889](./image/螢幕擷取畫面 2023-06-09 155849.png)
