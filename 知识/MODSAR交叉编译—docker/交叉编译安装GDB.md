1、下载源码压缩包

2、config编译


```
./configure CC="/opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++ -fpermissive" --target=arm-linux --host=arm-linux --prefix="/home/modsar/gdb/install"


./configure CC="/opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-gcc" CXX="/opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++" AR="/opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-ar" --target=arm-linux --host=arm-linux --prefix="/home/modsar/gdb/install" LD="/opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-ld"


export PATH=:${/opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin:${PATH}

```


不用编译发现，在交叉编译工具链中自带有  gdb   `不能用，x86结构的`
![[Pasted image 20231025095004.png]]


export LD_LIBRARY_PATH=/ota/arm64-install/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/ota/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc/usr/lib64/:$LD_LIBRARY_PATH



![[Pasted image 20231025103350.png]]


sudo service docker restart

安装 使用apt
```
apt install libncurses5-dev
 但是只能安装 6  加一个软链接
 ln -s libncursesw.so.6 libncursesw.so.5

缺少libtinfo
sudo ln -s libtinfo.so.6 libtinfo.so.5


apt-get install libpython2.7-dev


一个找库的网站

```
[Packages for Linux and Unix - pkgs.org](https://pkgs.org/)



使用本地 gdb 调试 远程arm板子上的arm程序  XXX




```
export LD_LIBRARY_PATH=/ota/arm64-install/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/ota/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc/usr/lib64/:$LD_LIBRARY_PATH
export MODSAR_APP_CONFIG="123"


set solib-search-path /ota/arm64-install/lib
set sysroot /ota/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc
target remote 172.20.0.9:1235



```




问题解决了：
 ![[Pasted image 20231025153417.png]]

原因：
![[Pasted image 20231025153503.png]]

在使用 这个这个的时候 环境变量为空，导致返回空指针+













"./aos_config/outputcfg/tda4b/VDC_TDA4_2_A_Deployment/PS_VM_SetManagerSlave_VDC_TDA4_2"
