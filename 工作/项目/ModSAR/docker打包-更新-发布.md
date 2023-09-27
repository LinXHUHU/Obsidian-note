
由于公司使用的平台比较多，每个平台都会给一个带有可编译SDK的虚拟机环境，这样下来，一共5、6个虚拟机，电脑性能又不是很好，虚拟机开多了卡的不行，要是平台切换的话挺麻烦。所以我就想把这些虚拟机制作成docker镜像，使用哪个平台直接切换docker镜像就行了，能提高不少效率。

将虚拟机打包成docker镜像也很简单，分几步吧：

需要进入 tmp目录下 

1、将虚拟机打包
 

tar --numeric-owner --exclude=/proc --exclude=/sys -zcvpf debian-3519.tar /


--numeric-owner:执行所属
--exclude：排除那些文件或者目录 
-zcvf ：打包压缩 p保持文件的绝对路径
2、导入镜像
将打包好的docker镜像放到装有docker的系统上，执行如下命令，导入镜像：

docker import debian-3519.tar(这是上一步打包好的docker镜像) image名字（自己定义）
3、运行镜像
docker run -it  image名字（上一步自己定义的） /bin/bash



docker import /tmp/modsar-system-amd64.tar modsar-docker

docker run -it -d -v /home/lxh/workspace/docker-test/:/home/lxh/ --name modsar-docker --privileged=true modsar-docker /bin/bash

docker ps -a   找到docker的名字

docker start docker的名字

docker exec -it modsar-docker  /bin/bash



---
scp命令的使用

suco scp  src_file username@ip-addr:/path_dir/ 

----


[docker 已有镜像修改更新, 修改容器后生成镜像_docker在已有image上更新_invisible_2018的博客-CSDN博客](https://blog.csdn.net/fkk921912333/article/details/108200394)
