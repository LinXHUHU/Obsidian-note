

```bash
sudo docker start modsar
sudo docker start modsar-2.0

sudo docker exec -it modsar /bin/bash
sudo docker exec -it modsar-2.0 /bin/bash
sudo docker exec -it modsar-3.0 /bin/bash


# docker 打包
sudo docker commit modsar modsar-ubuntu20.04:lasted
sudo docker commit modsar-2.0 modsar-2.0:show_demo

# 查看所有的image 
sudo docker image list

sudo docker save -o modsar-ubuntu20.04.tar modsar-ubuntu20.04:lasted


```


```
# 加载docker 镜像
docker load -i modsar-ubuntu20.04.tar

# 运行镜像，制造容器 并映射到代码仓库 
docker run -it -v /本地文件夹路径:/home/modsar --name modsar modsar-ubuntu20.04:lasted
docker run -it -v /path/to/host/folder:/path/in/container modsar-docker:1.0
docker run -it -v /home/lxh/workspace/dockers:/home/modsar --name m111 modsar-docker:1.0
docker run -it -v /home/lxh/workspace:/home/modsar --name modsar-2.0 modsar-ubuntu20.04:lasted

docker run -it -v /home/lxh/workspace:/home/modsar --name modsar-3.0 modsar-3.0:unified-compile




docker run -d -v /home/lxh/aosap-docker:/home/modsar --name m111 modsar-ubuntu20.04:lasted

# 启动docker
sudo docker start modsar
sudo docker exec -it modsar /bin/bash


```



```bash

# docker 修改名字
# 停止要修改名称的容器
docker stop old-container-name

# 使用 docker rename 命令修改容器名称
docker rename old-container-name new-container-name

# 重新启动容器（如果需要的话）
docker start new-container-name

```



```
# 删除docker的镜像

docker rmi image_name:tag

# 删除所有没有用到的镜像
docker image prune
```






```
cp -f ./build/example/radar_proxy/radar_proxy_main ./build/example/radar_skeleton/radar_skeleton_main /media/sf_shared/radar_modsar_demo_no_method/
```


bash脚本需求：
1、要求判断是否能够ping通 另外一台机器 ip为 192.168.10.10
2、连接成功之后，通过scp命令 将当前机器上的文件  copy到另外一个机器的某个文件夹
3、copy成功之后，输出提示

```bash
#!/bin/bash

# 设置目标服务器的IP地址
target_ip="192.168.10.10"

# 设置要传输的本地文件和目标文件夹
local_file="your_local_file"
remote_folder="your_remote_folder"

# 检查目标服务器是否可以ping通
if ping -c 1 $target_ip &> /dev/null; then
    echo "Ping成功：$target_ip 可达"
else
    echo "Ping失败：$target_ip 不可达"
    exit 1
fi

# 使用scp将本地文件拷贝到目标服务器
scp "$local_file" "$target_ip:$remote_folder"

# 检查scp命令的返回状态
if [ $? -eq 0 ]; then
    echo "文件拷贝成功：$local_file 已拷贝到 $target_ip:$remote_folder"
else
    echo "文件拷贝失败"
    exit 1
fi

# 脚本执行完成
exit 0


```



