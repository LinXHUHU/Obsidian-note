# docker 部署owncloud：自己的私有云盘

# 背景

将自己的电脑打造成一个属于自己的私有云盘，暴露公网

# 前提准备

云端服务器： 部署frps

‍

# 步骤

## docker安装

‍

参考 文档 [安装 Docker 和 Docker Compose](Blogs/TechnologyBlog/docker%20部署owncloud：自己的私有云盘/安装%20Docker%20和%20Docker%20Compose.md)

如果遇到下载docker失败，需要考虑apt 换源 参考[Ubuntu 更改apt 源_ubuntu 修改apt源-CSDN博客](https://blog.csdn.net/Hester1999/article/details/108579904)

‍

## docker compose 文件配置

‍

yaml文件

```bash
version: "3"

volumes:
  files:
    driver: local
  mysql:
    driver: local
  redis:
    driver: local

services:
  owncloud:
    image: owncloud/server:${OWNCLOUD_VERSION}
    container_name: owncloud_server
    restart: always
    ports:
      - ${HTTP_PORT}:8080
    depends_on:
      - mariadb
      - redis
    environment:
      - OWNCLOUD_DOMAIN=${OWNCLOUD_DOMAIN}
      - OWNCLOUD_TRUSTED_DOMAINS=${OWNCLOUD_TRUSTED_DOMAINS}
      - OWNCLOUD_DB_TYPE=mysql
      - OWNCLOUD_DB_NAME=owncloud
      - OWNCLOUD_DB_USERNAME=owncloud
      - OWNCLOUD_DB_PASSWORD=owncloud
      - OWNCLOUD_DB_HOST=mariadb
      - OWNCLOUD_ADMIN_USERNAME=${ADMIN_USERNAME}
      - OWNCLOUD_ADMIN_PASSWORD=${ADMIN_PASSWORD}
      - OWNCLOUD_MYSQL_UTF8MB4=true
      - OWNCLOUD_REDIS_ENABLED=true
      - OWNCLOUD_REDIS_HOST=redis
    healthcheck:
      test: ["CMD", "/usr/bin/healthcheck"]
      interval: 30s
      timeout: 10s
      retries: 5
    volumes:
      - files:/mnt/data

  mariadb:
    image: mariadb:10.11 # minimum required ownCloud version is 10.9
    container_name: owncloud_mariadb
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=owncloud
      - MYSQL_USER=owncloud
      - MYSQL_PASSWORD=owncloud
      - MYSQL_DATABASE=owncloud
      - MARIADB_AUTO_UPGRADE=1
    command: ["--max-allowed-packet=128M", "--innodb-log-file-size=64M"]
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-u", "root", "--password=owncloud"]
      interval: 10s
      timeout: 5s
      retries: 5
    volumes:
      - mysql:/var/lib/mysql

  redis:
    image: redis:6
    container_name: owncloud_redis
    restart: always
    command: ["--databases", "1"]
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5
    volumes:
      - redis:/data

```

‍

配置dodker环境变量.env

```bash
OWNCLOUD_VERSION=10.15
OWNCLOUD_DOMAIN=localhost:8080
OWNCLOUD_TRUSTED_DOMAINS="localhost,192.168.33.10,8.153.201.123"  # 这里很重要啊，需要些的并不是外面访问服务的地址，而是服务器自己的地址！！！
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin
HTTP_PORT=8080
```

‍

如果修改了环境变量，所有的volume都需要删除重新启动

```bash
sudo docker compose down -v   # 删除所有的volume， 但是不删除image（其实也没必要）
```

## 一键部署

```bash
sudo docker compose up -d
```

‍

‍

# 参考连接

[Installing with Docker :: Documentation for ownCloud (A Kiteworks Company)](https://doc.owncloud.com/server/next/admin_manual/installation/docker/)

‍
