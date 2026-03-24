

CentOS 上安装 Docker 可参考 [官方文档](https://docs.docker.com/engine/install/centos/)。  

完成安装后，建议将用户 `lxh` 添加到 `docker` 组中，这样便无需每次使用 `sudo` 来运行 Docker 命令。

---

## 切换 Docker 源  

在下载 Docker 镜像时，网络环境对效率至关重要。经过多次尝试，发现许多方法都无法成功实现镜像源的切换，最终只找到了一个非常实用的方法：  

参考链接：[Docker 更换镜像源（附国内可用镜像源地址） | Patrick's Blog](https://patzer0.com/archives/configure-docker-registry-mirrors-with-mirrors-available-in-cn-mainland)
‍
