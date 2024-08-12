# 一、linux 文件属性

```bash
ls -al
```

命令 显示当前目录下的所有文件及文件夹的详细信息。

![image-20240808104544021](C:\Users\XNL1WX\Documents\Obsidian-note\知识\cpp\嵌入式linux 完全开发手册.assets\image-20240808104544021.png)

# 二、常用指令介绍

- cp命令

```bash
cp -rfd dir_a dir_b
# r:recursive ，递归地，即复制所有文件
# f:force ，强制覆盖
# d:如果源文件为链接文件，也只是把它作为链接文件复制过去，而不是复制实际文件
```

-  chgrp

```bash
chgrp lxh filename
# 要求lxh 必须在 /etc/group 中，所以这里记录了所有的组信息
```

- chmod

```bash
chmod -R 755 filename
# -R 递归修改
# 数字类型修改
# 使用 ugo a=all方式修改， 
chmod u=rwx,go=rx .bashrc
# 使用+- 方式修改
chmod a+w .bashrc
```

- grep

  命令的作用是 查找文件中符合条件的字符串

  ```bash
  grep -rn "字符串" 文件名 
  # r(recursive) recursive)：递归查找 n(number) number)：显示行号
  ```

  文件名：文件名是必须的，但是可以通配符匹配多个文件

  字符串：这里可以使用-w 进行全词匹配

  使用管道来过滤

- 压缩解压

  压缩单个文件：

  ​	gzip：压缩小文件用

  ```Bash
  # l(list) 列出压缩文件的内容。
  # k(keep) 在压缩或解压时，保留输入文件。
  # d(decompress) 将压缩文件进行解压缩。
  ```

  

  ​	bzip2：压缩大文件用，压缩率高

  压缩多个文件：

  ​	tar：底层实际调用gzip 或者 bzip2

  ```Bash
  tar czvf dira.tar.gz dira
  #c(create) create)：表示创建用来生成文件包 。
  #x ：表示提取，从文件包中提取文件。
  #t ：可以查看压缩的文件。
  #z ：使用 gzip 方式进行处理，它与 ” 结合就表示压缩，与 ” 结合就表示解压缩。
  #j ：使用 bzip2 方式进行处理，它与 ” 结合就表示压缩，与 ” 结合就表示解压缩。
  #v(verbose) verbose)：详细报告 tar 处理的信息。
  #f(file) file)：表示文件，后面接着一个文件名。 C < 指定目录 > 解压到指定目录。
  ```

  

  

- 网络配置命令

  - ifconfig

     [linux.pdf](嵌入式linux 完全开发手册.assets\linux.pdf) 

    - 查看当前网卡
    - 查看所有网卡
    - 设置网卡IP

  - route 和DNS

    不能上网原因，路由和DNS

    原因查找

    ```Bash
    ping 8.8.8.8 
    # 不通代表路由不行
    ping www.baidu.com
    # 但是 p ing www.baidu.com ”不成功，则是 D NS 没设置好：
    ```

    1. 配置DNS服务器
    2. 配置路由信息
       1. 路由信息表内容含义
       2. 手动配置路由表
          1. 添加
          2. 删除

    

    

  - vi 文本编辑器

    - 模式切换

    <img src="C:\Users\XNL1WX\Documents\Obsidian-note\知识\cpp\嵌入式linux 完全开发手册.assets\image-20240808133516807.png" alt="image-20240808133516807" style="zoom:65%;" />

    - 文件的create，open，save
    - 

    

  

  









