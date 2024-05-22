
22.04 安装中文输入法

https://www.cnblogs.com/personblog/p/17520243.html




好像主要是有那位 ficx出问题了，有bug




解决方法


忽然不知道什么原因，我的系统无法输入中文了，怎么调整都不行。结果，发现是因为fcitx的原因，好好的卸载了，然后重启动就好了！
第一步，彻底卸载fcitx

sudo apt-get remove fcitx*
sudo apt-get purge fcitx*
1
2
第二步，将输入法系统设置为ibus

打开 设置 —> 语言支持
将键盘输入法系统选项设置为ibus
1
2
第三步 注销重新登录

完美解决，虽然不能再使用搜狗或者百度输入法了，但是稳定了，linux一般都是用来编程的，够了！
