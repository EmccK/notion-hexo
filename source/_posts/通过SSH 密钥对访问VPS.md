---
updated: '2025-01-07T13:46:00.000Z'
date: '2024-10-14T13:48:00.000Z'
categories: Linux
urlname: ssh-key-access-vps
tags:
  - Linux
title: 通过SSH 密钥对访问VPS
cover: 'https://cn.bing.com/th?id=OHR.ElbePhilharmonic_EN-US8658450086_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# 1. 本地生成公钥


```shell
ssh-keygen
```


会生成`id_rsa`和`id_rsa.pub`两个文件


# 2. 获取本地的公钥


```shell
cat ~/.ssh/id_rsa.pub
```


# 3. 将公钥添加到VPS的authorized_keys文件


```shell
# 如果authorized_keys不存在，则先创建吧
touch ~/.ssh/authorized_keys

# 编辑authorized_keys文件，添加本地公钥
vim ~/.ssh/authorized_keys
```


# 4. 添加完成之后即可不用密码连接VPS


通过SSH 密钥对访问VPS

