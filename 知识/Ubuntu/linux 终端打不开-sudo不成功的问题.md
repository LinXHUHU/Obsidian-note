
情况描述：新安装的虚拟机无法打开Terminal，从应用列表中单击Terminal，左上角任务栏会出现Terminal，并且鼠标转圈，但是过一会左上角Terminal消失，就像一切都没有来过。

解决办法：

CTRL + ALT + F3 进入命令行模式（需要返回桌面时CTRL + ALT + F1）  
cd /etc/default  
sudo nano locale  
把文件中的 “en_US” 改成 “en_US.UTF-8”

保存退出  
sudo locale-gen --purge  
reboot 重启虚拟机

---

> 	[如果你在执行 `sudo` 命令时遇到了 “不在 sudoers 文件中” 的错误，这意味着你没有权限以超级用户身份运行命令。要解决这个问题，你需要以其他管理员身份登录到系统，然后将你的用户名添加到 sudoers 文件中](https://blog.csdn.net/bean_business/article/details/112248565)[1](https://blog.csdn.net/bean_business/article/details/112248565)[。具体步骤如下](about:blank#)[2](https://zhuanlan.zhihu.com/p/143388819)[3](https://blog.csdn.net/csdnzouqi/article/details/95499348)：

1. 首先执行`su`命令切换至root用户：

```bash
su root
```

然后输入密码。

2. 查看 `/etc/sudoers` 文件权限，如果只读权限，修改为可写权限：

```bash
chmod u+w /etc/sudoers
```

3. 执行`vim`命令，编辑 `/etc/sudoers` 文件：

```bash
vim
```

4. 按 `i` 键进入编辑模式，在 `root ALL=(ALL) ALL` 的下一行添加代码： `lxh ALL=(ALL) ALL`
    
5. 按 `ESC` 键退出插入模式，然后键盘输入 `:wq` 保存并退出。
    
6. 恢复 `/etc/sudoers` 的权限为440：
    

```bash
chmod 440 /etc/sudoers
```

7. 切换至普通用户：

```bash
su lxh
```

8. 测试该用户的权限，例如使用命令 `sudo ls` 来查看当前目录。

