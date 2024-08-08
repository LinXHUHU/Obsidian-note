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

  





