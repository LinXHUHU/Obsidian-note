
## 前言
Halo 是一款现代化、高性能的开源博客系统，支持多平台部署。本文将介绍如何通过 Docker Compose 快速搭建一个个人博客，并展示如何更换博客的主题。

---

## 一、环境准备

1. **Docker 和 Docker Compose 安装**
   - 确保服务器已安装 Docker 和 Docker Compose。
   - 安装方法参考[[Blogs/TechnologyBlog/docker 部署owncloud：自己的私有云盘/安装 Docker 和 Docker Compose|安装 Docker 和 Docker Compose]]
   
1. **域名和 SSL 证书**
   - 如果需要绑定域名并启用 HTTPS，请提前准备好域名解析和 SSL 证书（可选）。

---

## 二、搭建步骤

### 1. 创建工作目录

在服务器上创建一个目录用于存放配置文件和数据：

```bash
mkdir ~/halo-blog
cd ~/halo-blog
```

### 2. 编写 `docker-compose.yml` 文件

在 `~/halo-blog` 目录下创建 `docker-compose.yml` 文件，内容如下：

```yaml
version: "3"

services:
  halo:
    image: registry.fit2cloud.com/halo/halo:2.20
    restart: on-failure:3
    # 因为这里要求mysql安全否则启动失败，注释掉，忽视错误
    #depends_on:
    #  halodb:
    #    condition: service_healthy
    depends_on: -halodb
    networks:
      halo_network:
    volumes:
      - ./halo2:/root/.halo2
    ports:
      - "8090:8090"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8090/actuator/health/readiness"]
      interval: 30s
      timeout: 5s
      retries: 5
      start_period: 30s
    environment:
      # JVM 参数，默认为 -Xmx256m -Xms256m，可以根据实际情况做调整，置空表示不添加 JVM 参数
      - JVM_OPTS=-Xmx256m -Xms256m
    command:
      - --spring.r2dbc.url=r2dbc:pool:postgresql://halodb/halo
      - --spring.r2dbc.username=halo
      # PostgreSQL 的密码，请保证与下方 POSTGRES_PASSWORD 的变量值一致。
      - --spring.r2dbc.password=openpostgresql
      - --spring.sql.init.platform=postgresql
      # 外部访问地址，请根据实际需要修改
      - --halo.external-url=http://localhost:8090/
  halodb:
    image: postgres:15.4
    restart: on-failure:3
    networks:
      halo_network:
    volumes:
      - ./db:/var/lib/postgresql/data
    healthcheck:
      test: [ "CMD", "pg_isready" ]
      interval: 10s
      timeout: 5s
      retries: 5
    environment:
      - POSTGRES_PASSWORD=openpostgresql
      - POSTGRES_USER=halo
      - POSTGRES_DB=halo
      - PGUSER=halo

networks:
  halo_network:
```

> 注意：
> - 替换 `MYSQL_USER`, `MYSQL_PASSWORD`, `root_password` 等为实际使用的数据库凭据。
> - 如果不需要 MySQL 数据库持久化，请移除 `volumes` 配置。

### 3. 启动服务

执行以下命令启动博客服务：

```bash
sudo docker-compose up -d
```

等待容器启动完成后，访问服务器的 IP 地址或域名（如 `http://<your-server-ip>:8080`），进入 Halo 的初始化页面完成博客的初始设置。

---

## 三、更换主题

Halo 支持通过插件系统更换主题，以下是具体操作步骤：

### 1. 登录 Halo 后台管理界面

- 打开浏览器访问 `http://<your-server-ip>:8080`。
- 使用初始登录信息，首次登录会让你注册超级管理员的。

### 2. 安装新主题
1. 在后台导航栏中选择 **插件** -> **主题**。
2. 点击右上角的 **安装插件** 按钮。
3. 在搜索框中输入主题名称（例如：`Butterfly`），点击安装。
4. 安装完成后，启用新主题。

### 3. 自定义主题

部分主题可能提供自定义选项，如颜色、布局等。请根据提示进行个性化设置。

---

## 四、其他注意事项

1. **备份数据**
   - 定期备份 `./data` 和 `./mysql-data` 目录，以防止数据丢失。

1. **更新博客**
   - 当 Halo 发布新版本时，只需更新 `docker-compose.yml` 中的镜像版本即可：
     ```bash
     docker-compose pull
     docker-compose up -d
     ```

1. **启用 HTTPS**
   - 如果需要启用 HTTPS，可以结合 Nginx 或 Caddy 进行反向代理配置。

---

## 五、参考链接
- [Halo 官方文档](https://docs.halo.run/)



[^1]: 
