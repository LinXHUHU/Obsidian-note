- CONST 常量的类型必须是确定的
- Rust 中，并非所有的函数都必须显式指定返回类型
	- 有一些情况下需要显式指定返回类型
		- **多义性的情况：** 当一个函数有多个可能的返回类型时
		- **希望强制函数返回特定的类型：** 如果你想要确保函数返回的类型是特定的
		- 无法指定的时候默认u32
- Rust distinguishes between expressions and statements
	- 可以直接使用return，不用那么麻烦了






**类单元结构体常常在你想要在某个类型上实现 trait 但不需要在类型中存储数据的时候发挥作用。我们将在第 10 章介绍 trait。**




[【Rust基础】Rustlings答案及解析-CSDN博客](https://blog.csdn.net/qq_43840665/article/details/130065993)
