---
updated: '2025-01-07T13:47:00.000Z'
date: '2024-03-02T11:25:00.000Z'
categories: Docker
urlname: commonly-docker-command
tags:
  - Docker
title: 常用的Docker命令
cover: 'https://cn.bing.com/th?id=OHR.KokinoMacedonia_ZH-CN6029529601_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# Docker相关


```shell
# 列出所有正在运行的Docker
docker ps -a

# 停止对应的任务
docker stop ${CONTAINER ID}

# 列出所有的容器
docker container ls

# 删除指定的容器
docker container rm e67459bab484

# 列出所有的镜像
docker images

# 删除指定ID对应的镜像
docker rmi 3ba9cfc06314

# 进入容器内部， 容器ID
docker exec -it 3ba9cfc06314 /bin/sh

# 删除无用的镜像(image)
docker image prune
```


# docker compose相关


```shell
# 安装docker镜像
# 创建docker-compose.yaml文件，里面填好docker相关的配置
# 执行下面命令即可安装
docker compose up -d

# 更新镜像: 先停止镜像
docker stop ${CONTAINER ID}
docker compose pull # 更新镜像
docker compose up -d # 重新运行docker

```


# 打包镜像


打包本地镜像，保存成`myimage.tar`


```shell
docker save -o myimage.tar myimage/test:latest

```


将tar文件导入服务器，使用如下命令导入镜像


```shell
docker load < myimage.tar

```

