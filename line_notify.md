## Line Notify

[﹝Linux﹞Zabbix LINE Notify 警報通知 | 工程師的江湖 - 點部落 (dotblogs.com.tw)](https://dotblogs.com.tw/xerion30476/2019/08/28/153643)



![img](./image/line_notify_script.png)



```
[root@centos7-1 alertscripts]# vim line_notify.sh
[root@centos7-1 alertscripts]# chmod +x line_notify.sh
[root@centos7-1 alertscripts]# chown  zabbix:zabbix line_notify.sh
[root@centos7-1 alertscripts]# ./line_notify.sh test "Sent from cnetos7"
{"status":200,"message":"ok"}[root@centos7-1 alertscripts]# cat line_notify.sh
#!/bin/bash
# LINE Notify Token - Media > "Send to".
TOKEN="HFUumxSJhTmve9boElwTRFkjBm1FvyjEhYrt8KafXeO"

# {ALERT.SUBJECT}
subject="$1"

# {ALERT.MESSAGE}
message="$2"

curl https://notify-api.line.me/api/notify -H "Authorization: Bearer ${TOKEN}" -F "message=${message}"

```



line and script is connected



then we need to setup the connection between zabbix server and line through the just created script -- line_notify.sh

![img](./image/zabbix_line_notify.png)