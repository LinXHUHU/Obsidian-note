# 阿里云部署siyuan service

# 背景信息

‍

‍

# 准备工作

**购买服务器**

	创建，购买，花钱就行，买了一个  99 一年的服务

![image](Blogs/TechnologyBlog/assets/image-20250327081522-o3kzaqj.png)​

[云服务器ECS_云主机_服务器托管_计算-阿里云](https://www.aliyun.com/product/ecs?spm=5176.29677750.nav-v2-dropdown-menu-1.d_main_0_0.5421154amWz8mt&scm=20140722.M_ecs.P_104.ID_ecs-OR_rec-PAR1_2150457b17430546223665344eae1b-V_1-MO_3480-ST_13051)

# 步骤

‍

## 终端连接服务器

首次登录使用aliyun 自带的**workbench**连接

登录的时候可能不知道密码是什么，点击**忘记密码**重新配置一下就好了

登录成功界面:

![image](Blogs/TechnologyBlog/assets/image-20250327081813-hp9xr93.png)

‍

## 创建用户

在连接服务器之后检查**系统镜像**类型为centos

```bash
cat /etc/os-release
```

![image](Blogs/TechnologyBlog/assets/image-20250327082953-wevt83u.png)

所以不能用 ubuntu 类似的命令来操作，应该可以实现系统镜像切换为ubuntu，详细参考[aliyun服务器切换镜像为Ubuntu](Blogs/TechnologyBlog/阿里云部署siyuan%20service/aliyun服务器切换镜像为Ubuntu.md)

---

登录之后当前用户为root，尽量不适用root用户操作

1. 新建用户

    ```bash
    # 新建
    useradd lxh
    # 查看是否创建成功
    cat /etc/passwd
    ```

    ‍
2. 设置新用户密码

    ```bash
    passwd lxh
    ```

    设置新密码

1. 新用户加入sudoer组

    在centos中，sudoer组名字为wheel，确认一下`visudo`​中是否启用wheel

    ![image](Blogs/TechnologyBlog/assets/image-20250327084220-q65r016.png)

    ```bash
    # 加入wheel组
    usermod -aG wheel lxh

    su lxh
    ```

    ‍

    ‍

## docker安装

参考 [安装 Docker 和 Docker Compose](Blogs/TechnologyBlog/docker%20部署owncloud：自己的私有云盘/安装%20Docker%20和%20Docker%20Compose.md)

## 创建docker-compose.yaml

创建docker compose文件

文件树

```bash
[lxh@iZuf64d1k2rx3g02nckzw2Z ~]$ tree 
.
└── workspace
    └── siyuan
        └── docker-compose.yaml
```

‍

文件docker-compose.yaml内容

accessAuthCode 必须设置，用来访问服务

```bash
version: "3.9"
services:
  main:
    image: b3log/siyuan
    command: ['--workspace=/siyuan/workspace/', '--accessAuthCode=lxhalan']
    ports:
      - 6806:6806
    volumes:
      - /siyuan/workspace:/siyuan/workspace
    restart: unless-stopped
    environment:
      # A list of time zone identifiers can be found at https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
      - TZ=${YOUR_TIME_ZONE}
      - PUID=${YOUR_USER_PUID}  # Customize user ID
      - PGID=${YOUR_USER_PGID}  # Customize group ID


```

‍

## 启动服务

```bash
sudo docker compose up -d

```

docker 换源之后速度会很快，不然会拉失败的

‍

## 安全组开放相关端口

docker 服务启动成功之后，并不能直接访问：

	因为aliyun 为了流量保护，禁用了端口，需要开发安全组配置， 参考[aliyun手册](https://help.aliyun.com/zh/ecs/user-guide/manage-security-groups?spm=a2c4g.11186623.help-menu-25365.d_4_6_3.1d1261f4DaCucO)

‍

![image](Blogs/TechnologyBlog/assets/image-20250327085427-spbpw42.png)

出入规则都需要配置

‍

## 完成

‍
