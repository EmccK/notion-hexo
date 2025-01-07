---
updated: '2025-01-07T13:45:00.000Z'
date: '2024-11-16T05:50:00.000Z'
categories: Docker
urlname: docker-navidrome
tags:
  - Docker
  - 实用教程
title: Navidrome 音乐服务器
cover: 'https://cn.bing.com/th?id=OHR.YiPengLanterns_EN-US2889801198_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# 介绍


![image.png](/images/f2776085b4c1173b317626c98b5208b8.png)


## Github地址


[link_preview](https://github.com/navidrome/navidrome/)


## 官网


[bookmark](https://www.navidrome.org/)


## 安装教程


[bookmark](https://www.navidrome.org/docs/installation/docker/)


# 搭建步骤


## 创建文件夹


```shell
mkdir Navidrome && cd Navidrome
```


## Docker Compose文件


```yaml
services:
  navidrome:
    image: deluan/navidrome:latest
    ports:
      - "4533:4533"
    restart: unless-stopped
    environment:
      ND_SCANSCHEDULE: 1h
      ND_LOGLEVEL: info
      ND_SESSIONTIMEOUT: 24h
      ND_BASEURL: "music.emcck.com"
    volumes:
      - "./data:/data"
      # 这里映射的音乐文件夹, "/path/to/your/music/folder:/music:ro"
```


## 运行


执行下面命令即可


```yaml
docker compose up -d
```


然后访问`IP:5433` 即可

