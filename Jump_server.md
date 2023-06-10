## Jump server

there are lots of server, and each of them have there own account and password

* we don't want to remember many account and password

* accounting -- keep the record of action we done
* firewall -- dangerous command jump server can deny it



https://github.com/wojiushixiaobai/Dockerfile

if jump server already installed, and you want to run it

```
docker-compose -f docker-compose-network.yml -f docker-compose-redis.yml -f docker-compose-mariadb.yml -f docker-compose.yml up -d
```



I modify the .env file in Dockerfile change the web  HTTP_PORT to 8080 because when starting docker it produce the error 80 port used



Then went to the ip address, it will show login page (default user/password: admin/admin, )

![image-20230412112309020](./image/image-20230412112309020.png)

![image-20230412114051277](C:\Users\z22756392z\AppData\Roaming\Typora\typora-user-images\image-20230412114051277.png)



1. create "Tom" account
2. setup the asset and system user(z22756392z)
3. link tom to centos7-2



## Record

view other users command

![image-20230609144013981](./image/螢幕擷取畫面 2023-06-09 144005.png)

login to tom account

1. web terminal
2. file manager

login to admin account

1. view -- 審計表
2. can view other user command and record



## Prevent

command filter



login to admin

1. asset -- command filter
2. command filter -- specify the command filter rule

