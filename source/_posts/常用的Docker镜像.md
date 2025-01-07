---
updated: '2025-01-07T13:47:00.000Z'
date: '2024-06-03T15:17:00.000Z'
categories: Docker
urlname: commonly-used-docker-images
tags:
  - Docker
title: 常用的Docker镜像
cover: 'https://cn.bing.com/th?id=OHR.LupinIceland_ZH-CN5329147708_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

## Webdav


[link_preview](https://github.com/hacdias/webdav)

<details>
<summary>`docker-compose.yml`</summary>

```yaml
services:
  webdav:
    image: ghcr.io/hacdias/webdav:latest
    ports:
      - 6161:6065
    volumes:
      - ./config.yml:/config.yml:ro
      - /Users/kai:/data
    restart: unless-stopped
    container_name: webdav
```


</details>

<details>
<summary>`config.yml`</summary>

```yaml
address: 0.0.0.0
port: 6065

# TLS-related settings if you want to enable TLS directly.
tls: false
cert: cert.pem
key: key.pem

# Prefix to apply to the WebDAV path-ing. Default is '/'.
prefix: /

# Enable or disable debug logging. Default is 'false'.
debug: false

# Disable sniffing the files to detect their content type. Default is 'false'.
noSniff: false

# Whether the server runs behind a trusted proxy or not. When this is true,
# the header X-Forwarded-For will be used for logging the remote addresses
# of logging attempts (if available).
behindProxy: false

# The directory that will be able to be accessed by the users when connecting.
# This directory will be used by users unless they have their own 'directory' defined.
# Default is '.' (current directory).
directory: .

# The default permissions for users. This is a case insensitive option. Possible
# permissions: C (Create), R (Read), U (Update), D (Delete). You can combine multiple
# permissions. For example, to allow to read and create, set "RC". Default is "R".
permissions: R

# The default permissions rules for users. Default is none. Rules are applied
# from last to first, that is, the first rule that matches the request, starting
# from the end, will be applied to the request.
rules: []

# The behavior of redefining the rules for users. It can be:
# - overwrite: when a user has rules defined, these will overwrite any global
#   rules already defined. That is, the global rules are not applicable to the
#   user.
# - append: when a user has rules defined, these will be appended to the global
#   rules already defined. That is, for this user, their own specific rules will
#   be checked first, and then the global rules.
# Default is 'overwrite'.
rulesBehavior: overwrite

# Logging configuration
log:
  # Logging format ('console', 'json'). Default is 'console'.
  format: console
  # Enable or disable colors. Default is 'true'. Only applied if format is 'console'.
  colors: true
  # Logging outputs. You can have more than one output. Default is only 'stderr'.
  outputs:
  - stderr

# CORS configuration
cors:
  # Whether or not CORS configuration should be applied. Default is 'false'.
  enabled: true
  credentials: true
  allowed_headers:
    - Depth
  allowed_hosts:
    - http://localhost:6065
  allowed_methods:
    - GET
  exposed_headers:
    - Content-Length
    - Content-Range


users:
  # 这里输入你的用户名
  - username: usename
  # 这里输入你的密码
    password: password
    permissions: CRUD
    directory: /data
```


</details>


## Portainer


[bookmark](https://docs.portainer.io/)

<details>
<summary>`docker-compose.yml`</summary>

```sql
services:
  portainer:
    restart: always
    container_name: portainer
    image: portainer/portainer-ce:latest
    ports:
      - 9000:9000   # Portainer Web UI
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./data:/data
```


</details>

