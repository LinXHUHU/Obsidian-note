# Typora Windows版本 免费激活教程

## 一、下载最新版Typora

网址：[Typora 官方中文站 (typoraio.cn)](https://typoraio.cn/)

## 二、安装

双击Typora.exe 安装完成

## 三、破解

1. 安装路径下找到：Typora\resources\page-dist\static\js![img](C:\Users\XNL1WX\Documents\Obsidian-note\知识\Typora\Typora Windows版本 免费激活教程.assets\9d05ab6a2f83458da38ed6d30c433324.png)

   右键用记事本打开这个文件，ctrl+F定位到

   **e.hasActivated="true"==e.hasActivated**

   **替换为**

   **e.hasActivated="true"=="true"**

   **这样就已经后台激活完成，但是每次开软件开始会提醒激活。**

2. 关闭软件每次启动时的已激活弹窗

继续在安装路径下resources\page-dist\**license.html，找到**

依旧ctrl+F 定位到：

**</body></html>**

**替换为** 

**</body><script>window.οnlοad=function(){setTimeout(()=>{window.close();},5);}</script></html>**



3. 去除软件左下角“未激活”提示

按照安装路径，找到 resources\locales\zh-Hans.lproj\**Panel.json** 

**文件中查找**：**"UNREGISTERED":"未激活"，**

**替换为："UNREGISTERED":" "**

**最后，重新打开Typora，手动关掉激活窗口，之后就不会再出现。**



## 四、获取好看的主题



 推荐：[github.com](https://github.com/ruyan-lx/typora-dyzj-theme)

安装步骤：

 1. 点击Download之后会跳转到github网站，点击下载第一个压缩包就好了，下载完后进行解压

    ![img](C:\Users\XNL1WX\Documents\Obsidian-note\知识\Typora\Typora Windows版本 免费激活教程.assets\d4c908340dbf37556b4ced2d1452a564-1722935606080-3.png)

 2. 然后打开我们的Typora和->文件->偏好设置->外观->打开主题文件夹，将解压好的文件拖到这个Typora的主题文件夹，之后重启一下Typora就有啦！

![img](C:\Users\XNL1WX\Documents\Obsidian-note\知识\Typora\Typora Windows版本 免费激活教程.assets\dc0b37b918d5c2748bd1990c328e9189-1722935679373-7.png)



## 五、网络图床搭建



[10分钟搞定Typora——实现免费图床搭建-CSDN博客](https://blog.csdn.net/qq_65034569/article/details/135549306)