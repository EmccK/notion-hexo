---
updated: '2025-01-07T13:46:00.000Z'
date: '2024-10-14T13:41:00.000Z'
categories: Linux
urlname: linux-open-ssh
tags:
  - Linux
title: Linux开启密码访问SSH
cover: 'https://cn.bing.com/th?id=OHR.AspensColorado_EN-US9105602602_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# 开启SSH访问

1. 检查是否已安装OpenSsh服务器

```bash
sshd -V
```


如果显示了OpenSsh的版本信息，则表示已安装，如果未安装，则先安装

1. 安装OpenSsh服务器
- 对于Debian/Ubuntu服务器：

```bash
sudo apt-get install openssh-server
```

- 对于CentOS/RHEL服务器：

```shell
sudo yum install openssh-server
```

1. 启动SSH服务

```bash
sudo service ssh start
```

1. 验证是否已启动

```bash
sudo service ssh status
```


# 允许密码连接

1. 使用文本编辑器编辑SSH配置文件

```bash
sudo vim /etc/ssh/sshd_config
```

1. 找到以下行，并去掉注释，重启sshd即可

```bash
# PasswordAuthentication yes
```


# 允许Root访问和开机启动

1. 使用文本编辑器编辑SSH配置文件

```bash
sudo vim /etc/ssh/sshd_config
```

1. 在打开的文件中，找到以下行：

```bash
#PermitRootLogin yes
```

1. 将该行的注释符号”#”去掉，并将其更改为：

```bash
PermitRootLogin yes
```

1. 启动SSH的开机启动
- 对于Debian/Ubuntu服务器：

```bash
sudo systemctl enable ssh
```

- 对于CentOS/RHEL服务器：

```bash
sudo systemctl enable sshd
```


# Oracle开启密码登录


编辑.ssh/authorized_keys文件，删除下面的代码，保留后面的ssh-


```text
no-port-forwarding,no-agent-forwarding,no-X11-forwarding,command="echo 'Please login as the user \"ubuntu\" rather than the user \"root\".';echo;sleep 10"
```

1. 使用文本编辑器编辑SSH配置文件

```shell
sudo vim /etc/ssh/sshd_config
```

1. 把下面的改成yes

```shell
KbdInteractiveAuthentication no
```

