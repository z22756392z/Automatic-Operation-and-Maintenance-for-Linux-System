##  Reference

[linux-note/Ansible.md at 107-2 · istar0me/linux-note (github.com)](https://github.com/istar0me/linux-note/blob/107-2/Ansible.md#ansible-playbooks)

## Ansible

Ansible is an open-source automation tool written in Python that simplifies the management and configuration of computer systems. It is designed to automate repetitive tasks, streamline application deployment, and orchestrate complex IT workflows. Ansible uses YAML (YAML Ain't Markup Language), a simple and human-readable language, to define automation tasks and playbooks.

## Installation

To install Ansible on CentOS, follow these steps:

1. Enable the EPEL Repository:

   ```
   arduinoCopy code
   sudo yum install epel-release
   ```

2. Install Ansible:

   ```
   Copy code
   sudo yum install ansible
   ```

3. Verify the Installation:

   ```
   cssCopy code
   ansible --version
   ```

   This command will display the installed version of Ansible.

## SSH No Password Login

To enable SSH login without a password, you need to set up public key authentication. Here's how you can do it:

1. Generate SSH Key Pair: On the machine you want to SSH from, generate an SSH key pair using the `ssh-keygen` command.
2. Copy Public Key to the Remote Server: Copy the public key (`id_rsa.pub`) to the remote server using the `ssh-copy-id` command or manually by appending it to the `~/.ssh/authorized_keys` file on the remote server.
3. Test SSH Login: Verify that you can SSH to the remote server without entering a password using the `ssh` command.

### Configuring Ansible Hosts

To configure Ansible hosts, you need to create an inventory file. Here's an example of an inventory file configuration:

1. Open the Inventory File:

   ```
   vim /etc/ansible/hosts
   ```

2. Define Hosts and Groups: Add the hosts and groups to the inventory file. Here's an example:

   ```
   [server1]
   192.168.56.103
   
   [server2]
   192.168.56.109
   
   [servers]
   192.168.56.103
   192.168.56.109
   ```

   In this example, "server1" and "server2" are individual hosts, and "servers" is a group containing both hosts.

By following these steps, you can install Ansible, set up SSH login without a password, and configure your Ansible hosts using an inventory file. This will allow you to automate tasks and manage your systems effectively using Ansible.



## Ansible Command

`ansible server1 -m command -a "rpm -q vsftpd"` query if package is installed on ovther server



`ansible server1 -m command -a "getent passwd user"`: check if user exist



## Ansible playbook

create yml file

```
ansible-playbook playbook.yml
```

Ansible will read the playbook file, connect to the specified hosts, and execute the tasks defined in the playbook.

##### hello world

```
---
- hosts: server1 # 應用在哪個主機，hosts:前後需有空白
  remote_user: root # 遠端使用哪個使用者操作

  tasks:
    - name: hello world # 工作名稱
      command: /usr/bin/wall hello world # 執行的指令
```

run

```
ansible-playbook playbook.yml
```

##### auto generate html file

create html file

`echo hello > hello.htm`

`vim test.yml`

```
---
- hosts: server1
  remote_user: root
  tasks:
    - name: create new file
      file: name=/tmp/newfile state=touch
    - name: create new user
      user: name=test2 system=yes shell=/sbin/nologin
    - name: install package # 安裝 httpd 套件
      yum: name=httpd
    - name: copy html # 將檔案複製到 app2 的指定資料夾
      copy: src=a.html dest=/var/www/html
    - name: start service # 啟動 httpd 服務
      service: name=httpd state=started
```

