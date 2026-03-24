
**Webhook配置**
全局钩子需要在 gerrit.config 配置。
项目级钩子通过 REST API 进行增删改查。（需要有项目的Owner权限）
API文档：{gerrit_host}/plugins/webhooks/Documentation/rest-api-config.md



**属于服务器hook范**畴
[gerrit-webhooks/change-merged.py at master · jtolio/gerrit-webhooks · GitHub](https://github.com/jtolio/gerrit-webhooks/blob/master/change-merged.py) 这里实现了一个gerrit出发的event事件脚本，会发送json 数据给一个Httpserver




# RESTFUL  API接口获取信息
 **列出所有的项目**
```
curl http://192.168.33.10:8081/projects/?d


)]}'
{"All-Projects":{"id":"All-Projects","description":"Access inherited by all other projects.","state":"ACTIVE","web_links":[{"name":"browse","url":"/plugins/gitiles/All-Projects"}]},"All-Users":{"id":"All-Users","description":"Individual user settings and preferences.","state":"ACTIVE","web_links":[{"name":"browse","url":"/plugins/gitiles/All-Users"}]}}

```



**Enabled webhooks for the repository, for example, MyTestRepo:**

```powershell
curl http://192.168.33.10:8081/config/server/webhooks~projects/MyTestRepo/remotes
```



**Add webhook for the repository:** （FAKE XXX）

```powershell
curl --user gerritadmin:jMs/o/hFfcFfs4DKJHxk9ZH3jvUkrxlJYFop68/2jw -H 'Content-Type: application/json' -X PUT -d @webhook.json http://8.153.201.123:8081/a/config/server/webhooks~projects/MyTestRepo/remotes/bbb-webhook
```


# 首先需要Gerrit 搭建，确认认证方式

在搭建 Gerrit 代码审查系统时，有多种用户认证方式可供选择，每种方式适用于不同的企业需求和安全策略。以下是 Gerrit 支持的主要认证方式及其特点：

---

### **1. HTTP 基础认证（Basic Auth）**
- **原理**：通过用户名/密码验证
- **适用场景**：简单的内部测试环境
- **配置方法**：
  ```
  [auth]
    type = HTTP
    httpHeader = Authorization
    httpEmailHeader = Email
  ```
- **缺点**：密码明文传输（需配合 HTTPS）

---

### **2. LDAP / Active Directory 集成**
- **原理**：连接企业 LDAP/AD 目录服务，需要LDAP服务器
- **适用场景**：企业内网统一认证
- **关键配置**：
  ```
  [ldap]
    server = ldap://ldap.example.com
    username = cn=admin,dc=example,dc=com
    password = secret
    accountBase = ou=people,dc=example,dc=com
    groupBase = ou=groups,dc=example,dc=com
  [auth]
    type = LDAP
    allowWindowsLive = false
  ```
- **优点**：支持组同步、企业级权限管理

---

### **3. OAuth 2.0 / OpenID Connect**
- **支持提供商**：
  - Google
  - GitHub
  - GitLab
  - Keycloak
  - 其他标准 OAuth2 服务
- **示例配置（Google）**：
  ```
  [auth]
    type = OAUTH
    allowGoogleAccountUpgrade = true
  [plugin "gerrit-oauth-provider-google"]
    client-id = YOUR_CLIENT_ID.apps.googleusercontent.com
    client-secret = YOUR_SECRET
    domain = example.com
  ```
- **流程**：用户通过第三方登录 → Gerrit 创建关联账号

---

### **4. SAML 2.0**
- **适用场景**：企业单点登录（SSO）
- **需要插件**：`gerrit-saml-plugin`
- **关键配置**：
  ```
  [auth]
    type = SAML
    samlUrl = https://sso.example.com/saml2
    samlKeystorePath = /path/to/keystore.jks
    samlKeystorePassword = changeit
  ```

---

### ==**5. 数据库认证（内置）**==
- **原理**：使用 Gerrit 自带的用户数据库
- **配置**：
  ```
  [auth]
    type = DEVELOPMENT_BECOME_ANY_ACCOUNT  # 仅测试环境
    # 或
    type = HTTP_LDAP  # 混合模式
  ```
- **特点**：需手动创建账号（通过 `gritty` 命令或 API）


---

### **7. 反向代理认证**
- **原理**：通过 Nginx/Apache 等代理传递用户信息
- **典型配置（Nginx）**：
  ```nginx
  location / {
    proxy_set_header X-Forwarded-User $remote_user;
    proxy_pass http://gerrit-server:8080;
  }
  ```
  Gerrit 配置：
  ```
  [auth]
    type = HTTP
    httpHeader = X-Forwarded-User
  ```

---

### **8. 混合认证模式**
可同时启用多种认证方式：
```
[auth]
  type = LDAP
  gitBasicAuthPolicy = LDAP  # 代码克隆允许LDAP密码
[plugin "gerrit-oauth-provider-github"]
  enabled = true
```

---

### **选择建议**
| 认证方式       | 适用场景                  | 安全等级 | 维护成本 |
|----------------|--------------------------|----------|----------|
| LDAP/AD        | 企业内网                  | ★★★★     | 中       |
| OAuth2         | 互联网团队/开源项目       | ★★★☆     | 低       |
| SAML           | 企业SSO集成               | ★★★★☆    | 高       |
| HTTP Basic Auth| 临时测试环境              | ★★☆      | 低       |
| 反向代理认证   | 已有统一网关的企业        | ★★★☆     | 中       |
最终选择使用5数据库认证 调试模式



# 配置webhook

## gerrit webhook介绍
Gerrit 作为一个使用广泛的代码评审平台，我们使用它的时候，往往会希望它能够一次性多完成几件事情，而不是简单的提交代码，合并代码。这个时候就需要用到串联事件的 hook 方法。Hook 作为钩子，能够搭建起事件之间的桥梁，实现在一个事件结束时自动触发我们想要触发的其他事件，从而完成我们对于代码评审相关的其他需求比如通知或者自动触发流水线程序等等。本文就来探讨一下 gerrit 相关的不同 hook 配置方式以及它们的优缺点。

### **1.Gerrit 不同 hook 方式介绍：**

![[Projects/asset/Pasted image 20250426191618.png]]

Gerrit 的 hook 方式按照 hook 事件配置地方的不同主要分为三种方式，客户端 hook，webhook 以及服务端 hook。客户端 hook 顾名思义是在本地客户端仓库配置的 hook 事件，它能够拦截本地仓库的一些事件，并作出相应的反应。

然而，客户端 hook 配置无法影响远程仓库的操作流程，而一般我们更加关注的是远程仓库的代码变化以及 hook 操作，所以客户端 hook 不在本文的讨论重点。Webhook 以及服务端 hook 都能够拦截远程仓库的相关事件，接下来一一介绍 webhook 和服务端 hook 的配置方式以及优劣。

①. 首先将 All-Projects 仓库 clone 下来：
```
git clone "http://admin@<gerrit-address>-:<gerrit-port>/a/All-Projects"
```

②. 然后进入到仓库内并切换到 config 分支

```
cd All-Projects/
git fetch origin refs/meta/config:refs/remotes/origin/meta/config
git checkout meta/config
```

>[!INFO]
>在fetch 代码的时候需要配置一下gerrit 权限，用户加入到Administrator组，在gerrit access权限配置一夜确认自己有拉去这个分支的权限
>![[Projects/asset/Pasted image 20250426192610.png]]
>
![[Projects/asset/Pasted image 20250426192924.png]]

>[!WARNING]
>注意所有的Alluser配置的修改必须使用管理员权限




③. 在 All-Projects 主目录下创建 webhooks.config 文件，并添加以下内容（示例仅作参考）：

```
[remote "events"]
url = http://11.11.11.111:9000/system_hook/v1/events
maxTries = 3
sslVerify = false
event = patchset-created
event = ref-updated
event = project-created
event = change-merged
event = hashtags-changed
```

（其中 url 为 webhook 对应的 url，maxTries 为最大尝试次数，sslVerify 为是否启用 ssl 验证，event 表示哪些事件会触发 webhook 操作）

④. 提交配置修改并重启 gerrit 服务：

```
git commit -am "Add webhooks config file"
git push origin meta/config:meta/config
```

>[!INFO]
>中间可能会遇到push失败的情况，需要按照上面的步骤确认有push的权限

>[!WARNING]
>如果权限有，仍然不行，需要配置一下插件 changeid 开启， 会给你很明白的提示
>按照**Hint**来做就行

![[Projects/asset/Pasted image 20250426193345.png]]

成功之后 
![[Projects/asset/Pasted image 20250426193641.png]]


# 搭建webhook监听服务器

先贴代码：
```
from http.server import BaseHTTPRequestHandler, HTTPServer

import json

  

# 自定义请求处理类

class SimpleHTTPRequestHandler(BaseHTTPRequestHandler):

    def _set_headers(self, status_code=200):

        self.send_response(status_code)

        self.send_header('Content-type', 'application/json')

        self.end_headers()

  

    # 处理 GET 请求

    def do_GET(self):

        self._set_headers()

        response = {

            "message": "GET request received",

            "path": self.path,

            "method": "GET"

        }

        self.wfile.write(json.dumps(response).encode())

  
  

    # 处理 POST 请求

    def do_POST(self):

        content_length = int(self.headers['Content-Length'])

        post_data = self.rfile.read(content_length)

        self._set_headers()

        response = {

            "message": "POST request received",

            "path": self.path,

            "method": "POST",

            "data": post_data.decode()

        }

        self.wfile.write(json.dumps(response).encode())

  

# 启动服务器

def run(server_class=HTTPServer, handler_class=SimpleHTTPRequestHandler, port=8082):

    server_address = ('', port)

    httpd = server_class(server_address, handler_class)

    print(f'Starting httpd server on port {port}...')

    httpd.serve_forever()

  

if __name__ == '__main__':

    run()
```

开启监听
```bash
uv run server.py
```




之后走正常流程提交代码：

```
 git push origin HEAD:refs/for/master
```


最终结果会受到如下POST HTTP报文


![[Projects/asset/Pasted image 20250426193618.png]]



# 集成RAGFLOW




# 返回消息comment在gerrit中
8EhjBkw5js8R0Z+vOjT/c38E5MKY0AwmnO8dg4Ndpw