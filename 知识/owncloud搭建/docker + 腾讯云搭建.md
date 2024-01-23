

首先申请一个腾讯云服务器，会自带公网ip，方便


下载docker

下载docker-compose

填充  compose 文件( 注意格式  )

```
version: '3'
  
services:
  owncloud:
    image: "owncloud/server:10.13"
    environment:
      OWNCLOUD_TRUSTED_DOMAINS: "111.229.112.74"
    ports:
      - "8080:8080"

```


启动docker
sudo docker-compose up -d


```
Pulling owncloud (owncloud/server:10.13)...
10.13: Pulling from owncloud/server
Digest: sha256:b516e7aa95114afc7782fdce437353152646e0a6f54bb733edf2647c8f07cef1
Status: Downloaded newer image for owncloud/server:10.13
Creating lighthouse_owncloud_1 ... done
```

