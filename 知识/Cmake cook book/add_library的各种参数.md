
# 重要的
STATIC

SHARED

OBJECT 直接连接到目标程序中，不需要生成静态或动态库

MOUDULE 不进行任何的链接，但是可在程序执行的时候进行加载，类似vsomeip中的插件

可以不输入字符，使用cmake的一个全局彬良控制静态库还是i动态库BUILD_SHARED_LIBS

---
# 不重要的：
IMPORTED：此类库目标表示位于项目外部的库。此类库的主要用途是，对现有依赖项进行构建。

因此， IMPORTED 库将被视为不可变的。我们将在本书的其他章节演示使用 IMPORTED 库的示

例。参见:

https://cmake.org/cmake/help/latest/manual/cmakebuildsystem.7.html#impo

rted-targets

INTERFACE：与 IMPORTED 库类似。不过，该类型库可变，没有位置信息。它主要用于项目之外

的目标构建使用。我们将在本章第5节中演示 INTERFACE 库的示例。参见:

https://cmake.org/cmake/help/latest/manual/cmake

buildsystem.7.html#interface-libraries

ALIAS：顾名思义，这种库为项目中已存在的库目标定义别名。不过，不能为 IMPORTED 库选择

别名。参见: https://cmake.org/cmake/help/latest/manual/cmake

buildsystem.7.html#alias-libraries


---
同名的静态动态库怎么生成

``` c++
1. add_library(message-shared

2. SHARED

3. $<TARGET_OBJECTS:message-objs>

4. )

5.

6. set_target_properties(message-shared

7. PROPERTIES

8. OUTPUT_NAME "message"

9. )

10.

11. add_library(message-static

12. STATIC

13. $<TARGET_OBJECTS:message-objs>

14. )

15.

16. set_target_properties(message-static

17. PROPERTIES

18. OUTPUT_NAME "message"

19. )
```