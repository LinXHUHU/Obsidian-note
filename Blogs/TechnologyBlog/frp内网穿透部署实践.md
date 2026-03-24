# frp内网穿透部署实践

# 背景

[frp 部署及使用（内网穿透）_frp内网穿透-CSDN博客](https://blog.csdn.net/m0_62160083/article/details/144805346)

# 方法

‍

# 步骤

‍

## 下载软件

```bash
wget https://github.com/fatedier/frp/releases/download/v0.32.1/frp_0.32.1_linux_amd64.tar.gz
tar -zxvf frp_0.61.1_linux_amd64.tar.gz
mv frp_0.61.1_linux_amd64 /usr/local/frp
```

‍

## 服务器/客户端用户配置

### 服务端配置

```bash
# 直接执行覆盖原来的配置
tee /usr/local/frp/frps.toml > /dev/null << 'EOF'
[common]
# 服务端绑定的端口，用于客户端与服务端通信的核心端口。需要确保该端口对外网开放。
bind_port = 7000
 
# HTTP 代理的虚拟主机端口。用于通过域名访问客户端的 HTTP 服务，需配置 DNS。
vhost_http_port = 80
 
# HTTPS 代理的虚拟主机端口。用于通过域名访问客户端的 HTTPS 服务，需配置 DNS。
vhost_https_port = 443
 
# 密钥，是自定义的，想怎么填写就怎么填写，但客户端和服务端必须保持一致，确保安全通信。
token = "Frp20241129"
 
# 仪表板端口，用于查看 frps 服务端的运行状态和管理客户端连接。访问地址：服务器IP:7500
dashboard_port = 7500
EOF
```

‍

```bash
# 加入系统服务
cat <<EOF | tee /etc/systemd/system/frps.service
[Unit]
Description=FRP Server
After=network-online.target
Wants=network-online.target
[Service]
User=frp
WorkingDirectory=/usr/local/frp
ExecStart=/usr/local/frp/frps -c /usr/local/frp/frps.toml
Environment=FRP_LOG_LEVEL=info
Restart=always
RestartSec=5s
StandardOutput=journal
StandardError=journal
[Install]
WantedBy=multi-user.target
EOF
 
 
# 重载配置使其生效
systemctl daemon-reload
 
# 启动 frps 服务
systemctl start frps.service
 
# 设置开机自启
systemctl enable frps.service
```

但是因为占用了80端口，80端口为特殊端口，需要特殊权限

```bash
# 查看service详细日志
sudo journalctl -u frps.service





```

发现是因为80端口权限不足导致

有两种解决方法

**方法一**：使用大于 1024 的端口

你可以在 Frp 配置文件里将 HTTP 监听端口修改为大于 1024 的端口，这样普通用户就有权限绑定该端口了。

步骤

1. **编辑** **​`frps.toml`​**​ **文件**：

bash

```bash
sudo nano /usr/local/frp/frps.toml
```

2. **修改** **​`vhost_http_port`​**​ **参数**：  
    把 `vhost_http_port`​ 从 `80`​ 修改为大于 1024 的端口，例如 `8080`​。

toml

```toml
[common]
bind_port = 7000
vhost_http_port = 8080
```

3. **保存文件并重启 Frp 服务**：

bash

```bash
sudo systemctl restart frps.service
```

**方法二**：使用 `setcap`​ 命令赋予权限

​`setcap`​ 命令能够为可执行文件赋予特定的能力，比如绑定特权端口的能力。

步骤

1. **为** **​`frps`​**​ **可执行文件赋予绑定特权端口的能力**：

bash

```bash
sudo setcap 'cap_net_bind_service=+ep' /usr/local/frp/frps
```

此命令会让 `frps`​ 可执行文件拥有绑定特权端口的权限。

2. **重启 Frp 服务**：

bash

```bash
sudo systemctl restart frps.service
```

‍

选用了第一种方法成功登录

‍

‍

‍

### 客户端配置

客户端的主要作用是在服务端注册服务，开放本地端口和服务器端口的映射

‍

‍

#### 下载安装包并解压

```bash
# 解压到当前目录
tar -zxvf frp_0.61.1_linux_amd64.tar.gz
 
# 移动并改名
mv frp_0.61.1_linux_amd64 /usr/local/frp
 
# 创建 frp 用户
useradd -r -s /usr/sbin/nologin -M frp
 
# 授权文件夹
chown -R frp:frp /usr/local/frp
```

‍

#### 修改ifrpc配置文件

```bash
cp /usr/local/frp/frpc.toml /usr/local/frp/frpc.tomlbak
```

```bash
# 直接执行覆盖原来的配置
tee /usr/local/frp/frpc.toml > /dev/null << 'EOF'
[common]
server_addr = "此处引号内填写外网服务器的公网IP"
# 服务端口
server_port = 7000
# 密钥，需要和 frps 配置一致
token = "Frp20241129"
 
# 配置每个内网服务
 
# 服务名称，随便写，自己能看懂就行
[ssh_test]
type = "tcp"
local_ip = "127.0.0.1"
# 家用服务器上暴露的端口
local_port = 22
# 外网服务器上暴露的端口，ssh时候，使用外网 IP 和这个端口可以远程访问家里的服务器
remote_port = 2299
 
# 服务名称，随便写，自己能看懂就行
[web_server]
type = "http"
local_ip = "127.0.0.1"
# 家用服务器上暴露的端口
local_port = 80
# 外网服务器上暴露的端口，使用外网 IP 和这个端口可以远程访问家里web服务，这个配置和域名
#remote_port = 6001
# 用于 HTTP 和 HTTPS 域名的代理。填写自己的域名，没有就注释这个配置，启用 remote_port 配置
custom_domains = "www.adbc.cn"
 
 
#remote_port 和 custom_domains 配置冲突，只能使用一个
 
EOF
```

‍

填充自己的服务器公网ip， 谢谢自己想要开放的服务端口， 修改token 必须和frps配置i保持一直

‍

#### 系统服务开机自启

```bash
# 加入系统服务
cat <<EOF | tee /etc/systemd/system/frpc.service
[Unit]
Description=FRP Client
After=network-online.target
Wants=network-online.target
[Service]
User=frp
WorkingDirectory=/usr/local/frp
ExecStart=/usr/local/frp/frpc -c /usr/local/frp/frpc.toml
Environment=FRP_LOG_LEVEL=info
Restart=always
RestartSec=5s
StandardOutput=journal
StandardError=journal
[Install]
WantedBy=multi-user.target
EOF
 
 
# 重载配置使其生效
systemctl daemon-reload
 
# 启动 frps 服务
systemctl start frpc.service
 
# 设置开机自启
systemctl enable frpc.service
```

‍

 之后应该就成功了

‍

#### 验证是否成功

打开公网部署的frps服务的网址

在proxy中看是否有client 注册的tannel，有的话就成功了

![image](Blogs/TechnologyBlog/assets/image-20250330065112-9l3w03k.png)

‍
## 配置文件配置方法

[新版frp（frp.toml）配置文件详情 - 贰叁肆](https://www.ersansi.top/index.php/archives/1194/)
