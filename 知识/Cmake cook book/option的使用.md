option(USE_LIBRARY "Compile sources into a library" OFF)

cmake -D USE_LIBRARY=ON ..


cmake_dependent_option() 命令用来定义依赖于其他选项的选项：
用法：![[Pasted image 20230920102805.png]]

但是必须包含了一个名为 CMakeDependentOption 的模块。 否则不可用