
- cmake默认的生成器是makefile
- 可以切换成Ninja   cmake -G Ninja ..
	- 优点：小，块，适用于大型项目的构建

```
# 切换成Ninja之后 就不能使用make 作为构建命令了
cmake --build .  # 是通用的
```


其他的
![[Pasted image 20230919181856.png]]
