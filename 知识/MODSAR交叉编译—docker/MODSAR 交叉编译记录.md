

## 2023.10.16 日周一

- [x] 搭建docker环境，暂时使用AOS
- [ ] 交叉编译boost （暂时不做，docker SDK中有现成的 老版本的boost，后面又可能需要）
- [x] 编译vsomeip，并install到相对应的位置
1、如何 添加cmake参数：解决：在使用add_subdirectory之前，通过set设置变量
```Cmake
set(DEFAULT_CONFIGURATION_FOLDER ../aos_config/outputcfg/tda4b/VDC_TDA4_2_A_Deployment/PS_VM_SetManagerSlave_VDC_TDA4_2)

set(DEFAULT_CONFIGURATION_FILE ../aos_config/outputcfg/tda4b/VDC_TDA4_2_A_Deployment/PS_VM_SetManagerSlave_VDC_TDA4_2/PS_VM_SetManagerSlave_VDC_TDA4_2/vsomeip.json)

add_subdirectory(modsar-middleware/third_party/vsomeip)
```

- [x] 编译logger， 并install
1、一般来说，头文件放到include中，库文件放到lib中，二进制文件放到bin中
2、logger，安装头文件的时候，按照vsomeip安装过程进行

- [x] 交叉编译  foonathan_memory_vendor库
	编译的时候需要联网，docker不知道怎么联网，有点难受啊
	sudo service docker restart，重启所有docker，，就可以联网了，神奇（最重要的就是换网！！）

- [x] 交叉编译Fast-CDR 完成
- [x] 交叉编译ASIO
- [x] 交叉编译Fast-DDS
	1、在编译的时候发现，ASIO库需要
		解决：由于ASIO库，并不是动态库，只需要头文件即可，所以直接在docker环境中使用apt install libasio-dev即可
	2、到时候转移到VDC上的时候，该怎么处理？需要将asio的头文件转移板子上
		（使用）解决1：将docker环境中的所有头文件转移到板子上/usr/include，手动转移
			cp -a /usr/include/asio* ./
		解决2：写一个install ，同时编译asio，将所有的头文件安装 XXX 可能会有错误，暂时不用
	3、（使用）在这里打开了所有的警告转 error，需要修改，或删除，编译fast-dds的时候 
	add_compile_options(-Wall -Werror -Wno-unused-variable)
	
- [x] 交叉编译tinyxml
- [x] 交叉编译abseil 库
	1、会出现报错，表示存在不被 clang支持 的参数（去掉 -maes  # "-msse4.1"）
	2、这两个参数的目的只是，精简指令集使用的，去掉无所谓
- [x] 交叉编译protobuf
	1、首先git 源码，仓库
	2、直接git 的话，会没有第三方仓库，所以之后需要运行 git submodule update --init --recursive  下载依赖的第三方库源码
	3、添加 宏  set(protobuf_BUILD_TESTS OFF)，如果下了 第三方库，就可以不需要了
	4、出现错误，表示clang不支持：`PROTOBUF_EXPORT` 宏的定义导致的，它使用了 `__attribute__((visibility("default")))`，这个属性尝试将符号标记为默认的可见性。然而，Clang 编译器可能不支持 `visibility` 属性应用于 C++11 枚举类。这导致了编译错误。（解决：删除这 `-Werror`）





#交叉编译坑 在交叉编译转正常编译的时候，需要删除缓存，直接删掉build目录


'
## docker apt 换源
https://blog.csdn.net/moshiyaofei/article/details/122159325



# 交叉编译 boost

[Boost 源代码交叉编译 - 采男孩的小蘑菇 - 博客园 (cnblogs.com)](https://www.cnblogs.com/flyinggod/p/12871298.html)





# 建立新的docker进行交叉编译

- 交叉编译boost的时候
	- 注意需要哪些库，就装哪些，否则太大了
	- 在Cmake中指定库查找目录，set(CMAKE_FIND_ROOT_PATH /home/modsar/install)
```
using gcc : : /home/modsar/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++ ;

using gcc : : /opt/SDK/aos/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++ ;

using gcc : : /opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++ ;


./bootstrap.sh --with-libraries=filesystem,thread,system --prefix=/home/modsar/install
./bootstrap.sh --with-libraries=filesystem,thread,system --prefix=/home/faw_vdc/arm64-intsll
```

- 交叉编译vsomeip
	- 遇到错误，-fpermissive
	- boost库版本与vsomeip版本不兼容的问题，更换boost库换成[1.66.0版本](https://sourceforge.net/projects/boost/files/latest/download),
- 编译foono的
	- 遇到无法下载git的错误---换源，换了[清华园](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/)
	- 最后还是使用之前交叉编译成的版本，放到install中
```
# bin中的一个文件
sudo cp -a bin /home/lxh/workspace/DDS-branch/install/
# lib 中静态库
sudo cp -a libfoonathan_memory-0.7.3.a /home/lxh/workspace/DDS-branch/install/lib
# cmake文件
sudo cp -a foonathan_memory /home/lxh/workspace/DDS-branch/install/lib

```
- 编译 Fast-CDR
	- 使用高版本cmake
```
/home/modsar/cmake-3.28.0-rc1-linux-x86_64/bin/cmake ..
/home/modsar/cmake-3.28.0-rc1-linux-x86_64/bin/cmake --build . --target install
```

- 编译FastDDS
	- 需要先安装libasio-dev ，因为全是头文件，所以可以直接使用asio，无需交叉编译
	- 提示找不到asio.hpp文件，安装了也不行，修改cmake 加入include_directoeys()(没用)

-  编译example  
	- 会出现proto文件过期的问题，因此，需要重新生成
	- 因此，可能会要安装protoc，但是交叉编译的protoc是不能使用的，所以需要x86的



export LD_LIBRARY_PATH=  /home/modsar/install/lib:$LD_LIBRARY_PATH




# 2023.10.20 全盘崩溃

重新开始，一个一个开始编译，每个第三方库一个单位，自己的项目自己一个库


CMAKE_CXX_COMPILER=/home/modsar/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++





[交叉编译 OpenSSL_openssl 交叉编译_iBlackAngel的博客-CSDN博客](https://blog.csdn.net/bluebird_shao/article/details/123553089)
export PATH=$PATH:/home/modsar/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin
./config no-asm  --cross-compile-prefix=aarch64-none-linux-gnu-


[fastdds交叉编译-CSDN博客](https://blog.csdn.net/qq_41281601/article/details/122827385)






> 猜测可能是因为使用了不同版本的cmake导致的找不到库。
> 	很大可能,  也不对劲，为什么X86上就可以正确执行？
> 	

/home/modsar/cmake-3.28.0-rc1-linux-x86_64/bin/cmake ..
/home/modsar/cmake-3.28.0-rc1-linux-x86_64/bin/cmake --build . --target install



> 如果还是不行，则使用aoscocker 重新搞一次


```
sudo service docker restart
sudo docker start 6ce7ce77fb0d
sudo docker exec -it aosap /bin/bash

```



```
#配置C++编译器

set(CMAKE_CXX_COMPILER /opt/SDK/aos/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++)

#配置C编译器

set(CMAKE_C_COMPILER /opt/SDK/aos/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-gcc)

#配置系统路径
set(CMAKE_SYSROOT /opt/SDK/aos/arm64/common/sysroot)

#配置库文件头文件搜索路径
set(CMAKE_FIND_ROOT_PATH /home/faw_vdc/arm64-intsllarm64-intsll)

#配置安装路径
set(CMAKE_INSTALL_PREFIX /home/faw_vdc/arm64-intsll)

SET(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)

SET(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)

SET(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
```

```

/opt/cmake-3.22.1-linux-x86_64/bin/cmake .. -DCMAKE_INSTALL_PREFIX=/home/faw_vdc/arm64-intsll -DBUILD_SHARED_LIBS=ON
/opt/cmake-3.22.1-linux-x86_64/bin/cmake --build . --target install
```

```bash
/opt/cmake-3.22.1-linux-x86_64/bin/cmake .. -DFOONATHAN_MEMORY_BUILD_EXAMPLES=OFF -DFOONATHAN_MEMORY_BUILD_TESTS=OFF -DFOONATHAN_MEMORY_BUILD_TOOLS=OFF -DCMAKE_INSTALL_PREFIX=/home/faw_vdc/arm64-intsll -DCMAKE_C_COMPILER=/opt/SDK/aos/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-gcc -DCMAKE_CXX_COMPILER=/opt/SDK/aos/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++ -DCMAKE_SYSTEM_PROCESSOR=arm -DCMAKE_SYSTEM_NAME=Linux


/opt/cmake-3.22.1-linux-x86_64/bin/cmake --build . --target install
```



在编译foo的时候u，会出现编译的结果不是  arm架构的，CMAKE_CXX没有传递下去，奇怪












```

#配置C++编译器

set(CMAKE_CXX_COMPILER /home/modsar/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++)

#配置C编译器

set(CMAKE_C_COMPILER /home/modsar/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-gcc)

#配置库文件头文件搜索路径
set(CMAKE_FIND_ROOT_PATH /usr/local)

#配置安装路径
set(CMAKE_INSTALL_PREFIX /usr/local)

SET(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)

SET(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)

SET(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
```

```
export CXX=/home/modsar/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++
```

```
/home/modsar/cmake-3.28.0-rc1-linux-x86_64/bin/cmake ..
/home/modsar/cmake-3.28.0-rc1-linux-x86_64/bin/cmake --build . --target install
```





```
/opt/cmake-3.22.1-linux-x86_64/bin/cmake .. -DCMAKE_INSTALL_PREFIX=/home/faw_vdc/arm64-intsll -DBUILD_SHARED_LIBS=ON -DABSL_PROPAGATE_CXX_STD=ON


/opt/cmake-3.22.1-linux-x86_64/bin/cmake --build . --target install
```






总结：
为什么链接不上

1、在编译第三方库的时候  没有指定正确的  glibc

2、在编译modsar.so的时候，没有指定动态库的路径。

大概就是这两个了





```
#配置C++编译器
set(CMAKE_CXX_COMPILER /opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++)

#配置C编译器

set(CMAKE_C_COMPILER /opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-gcc)

#配置系统路径
set(CMAKE_SYSROOT /opt/modsar/SDK/arm64/gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc/)

#配置库文件头文件搜索路径
set(CMAKE_FIND_ROOT_PATH /opt/modsar/arm64-install)

#配置安装路径
set(CMAKE_INSTALL_PREFIX /opt/modsar/arm64-install)

SET(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)

SET(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)

SET(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
```








