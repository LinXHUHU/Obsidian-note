
1、创建一个新的镜像，基于aosap的 镜像吧
2、将aos仓库的build架构复制一下
3、删除内部所有的代码
4、将所有的第三方库都放在code中




# 下载安装 **Portainer**

```
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer


这个命令将从Docker Hub下载Portainer镜像，然后在后台运行一个名为"portainer"的容器。Portainer将在9000端口上运行，你可以在浏览器中访问`http://localhost:9000`来访问Portainer的Web界面。

- `-d`：以后台模式运行容器。
- `-p 9000:9000`：将容器的9000端口映射到主机的9000端口。
- `--name portainer`：指定容器的名称为"portainer"。
- `--restart always`：设置容器在启动时自动重新启动。
- `-v /var/run/docker.sock:/var/run/docker.sock`：将主机的Docker套接字映射到容器内，以便Portainer可以与主机的Docker守护进程通信。
- `portainer/portainer`：要运行的Portainer镜像。

```



# git的坑

新建一个分支之后，删除了一个文件夹，如果不提交，那么这个改变会  update到  其他分支，如果要避免
使用  
```
git stash 

git stash apply
```

在删除文件的时候，需要手动指定，不能使用通配符 * 指定

