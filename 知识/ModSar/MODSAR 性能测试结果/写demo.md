
1、内存泄露，之前序列化的时候发现过，但是没解决
2、在管理交叉编译的时候，最好是在同一个项目，不然 会出现版本更新导致做无用功
3、需要写一份 完整的交叉编译过程文档
4、在统计数量的时候使用  局部静态变量非常舒服，不需要使用 全局
5、




# 继续完善新的demo


1、pc
- 运行proxy 1，收到服务器发布的雷达数据，打印出来，并且打印出来
- 运行proxy 2，接收服务器中的监控端，发布的数据，收到之后打印图片数据。
- 还是一个proxy 同时订阅两个 服务器发布的服务

2、s32g  radar发布
- 一个skeleton




```
# 将proto文件替换

# 运行build bash脚本

# 将app 和 库 copy到目的地
scp ./build/arm64/example/show_demo/s32g_monitor_app/s32g_monitor_app bluebox@192.168.10.10:/home/bluebox/s32g_monitor

scp ./build/arm64/example/show_demo/s32g_radar_app/s32g_radar_app bluebox@192.168.10.10:/home/bluebox/s32g_radar

# 库 libradar-upload
scp ./third_party/radar-upload/build/src/libradar-upload.so bluebox@192.168.10.10:/home/bluebox/arm64-install/lib

# 库 libmodsar_so
scp ./build/arm64/src/ara/com/internal/libmodsar_so.so bluebox@192.168.10.10:/home/bluebox/arm64-install/lib


# 配置文件
scp S32G_MONITOR_APP.tar bluebox@192.168.10.10:/home/bluebox/s32g_monitor
scp S32G_RADAR_APP.tar bluebox@192.168.10.10:/home/bluebox/s32g_radar




```





# CPU负载超限bug

主要原因是一个 log，使用LOG_ARRAY 虽然没有达到输出等级，后台也会运行，导致CPU负载极大




# vscode 自动格式化代码

CC++ 插件中自带的有，需要  点击ctrl +，搜索 format   勾上   on save 就可以了



