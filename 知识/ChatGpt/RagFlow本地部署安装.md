## sysctl vm.max_map_count  这个东西有什么作用吗？

`vm.max_map_count` 是 Linux 内核的一个系统参数，用于控制单个进程能够创建的最大内存映射数（即 map count）。这个参数主要用于防止系统因为过多的内存映射而变得不稳定。

内存映射（memory mapping）是指将文件或其他对象的地址空间与进程的虚拟地址空间相关联，这样就可以像访问内存一样访问文件数据。例如，当一个程序加载动态链接库（shared libraries）或者通过 mmap() 系统调用来映射文件时，就会增加内存映射计数。

如果一个进程创建了太多的内存映射区域，可能会导致性能下降或者其他问题。为了防止这种情况，内核允许管理员或者系统设置 `vm.max_map_count` 参数来限制每个进程能拥有的最大映射数。

当你执行 `sysctl vm.max_map_count` 命令时，你会看到当前的设置值。例如：

```sh
$ sysctl vm.max_map_count
vm.max_map_count: 65536
```

这表示当前系统设置的每个进程的最大内存映射数为 65536。

如果你发现某些应用运行时出现问题，尤其是那些需要大量内存映射的应用（如 Elasticsearch、Chrome 浏览器等），可能需要调整这个参数。调整方法可以通过下面的命令临时修改：

```sh
$ sudo sysctl -w vm.max_map_count=262144
```

要永久更改这个设置，可以在 `/etc/sysctl.conf` 文件中添加或修改这一行：

```sh
vm.max_map_count = 262144
```

然后重启系统或者运行 `sysctl --system` 使更改生效。

请注意，增加 `vm.max_map_count` 可能会引入新的问题，因为它增加了系统的内存管理负担。因此，在做出任何改变之前，最好先了解应用程序的具体需求，并根据实际情况调整该参数。



### 修改步骤

```
sudo sysctl -w vm.max_map_count=262144
```





## 在启动各种docker服务的时候出现由于内存溢出导致的内存损坏问题

1、 进入uniram 界面

2、内存恢复操作

```
fsck /dev/sdaX

```

3、重启虚拟机

```
reboot
poweroff
```







## 虚拟机硬件要求

![image-20240917165752750](C:\Users\XNL1WX\Documents\Obsidian-note\知识\ChatGpt\assets\image-20240917165752750.png)

### CPU信息

```
lscpu  # 查看CPU数量以及，每一个CPU的核心数量


```



### RAM 空间信息

`free` 命令可以显示系统中总内存、已用内存和空闲内存的信息。这是最常用的方法之一：

```
1free -m

cat /proc/meminfo
```

这里的 `-m` 选项表示以 MB（兆字节）为单位显示内存大小。输出类似于以下内容：



### 磁盘空间DIsk

```
df -h 
lsblk 
```



## 内存损坏之后，重新恢复，服务启动失败

1、停止所有 服务

```
sudo docker compose down
```

2、查看所有docker 的volume

```
sudo docker volume ls
```

3、重新启动所有docker服务

```
sudo docker compose up -d
```

4、成功



