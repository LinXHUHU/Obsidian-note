
# What is Rust?
Rust is a modern system programming language focused on performance, **safety**, and **concurrency**. It accomplishes these goals **without having a garbage collector**, making it a useful language for a number of use cases other languages aren’t good at. Its syntax is **similar to C++**, but Rust offers better **memory safety** while maintaining high performance.




# Why use Rust?

Rust is a system programming language that aims to provide **memory safety**, **concurrency**, and **performance** with a focus on **zero cost abstractions**. It was originally created by **Graydon Hoare** at Mozilla Research, with contributions from **Brendan Eich**, the creator of JavaScript. Rust is appreciated for the solutions it provides to common programming language issues. Its emphasis on **safety**, **speed**, and support for **concurrent programming**, as well as its **robust type system**, are just a few reasons why developers choose Rust.



# Memory Safety and Zero-Cost Abstractions

**Memory Safety**: Rust ensures memory safety through its ownership system, which enforces rules at compile time to prevent memory leaks and dangling pointers, eliminating the need for garbage collection or manual memory management. This system also supports concurrent programming and thread safety.

**Zero-Cost Abstractions**: Rust provides abstractions like iterators and closures that do not introduce runtime overhead, allowing high-level code to be optimized to run as efficiently as low-level code.



# EnvSetup

[[Blogs/Cargo Env Setup and change source|Cargo Env Setup and change source]]


# Rust REPL (Rust Playground)

**Rust 官方没有内置 REPL**  
由于 Rust 是静态编译型语言，需要完整的编译和所有权检查，因此官方未提供标准 REPL 工具。不过，社区有一些替代方案：

- **`evcxr`**：最流行的 Rust REPL 工具（[GitHub](https://github.com/google/evcxr)），支持 Jupyter Notebook。
    
- **`irust`**：另一个简单的交互式 Rust 环境（[GitHub](https://github.com/sigmaSd/IRust)）。
    
```
>> let x = 5;
>> println!("{}", x * 2);
10
```


[Rust Playground](https://play.rust-lang.org/) 是一个**在线沙盒环境**，允许用户直接在浏览器中编写、编译和运行 Rust 代码，无需本地安装。它的功能包括

### **REPL 与 Playground 的区别**

|特性|REPL|Rust Playground|
|---|---|---|
|**交互性**|逐行执行|完整编译后运行|
|**是否需要安装**|需要（如 `evcxr`）|无需，在线使用|
|**适用场景**|快速实验语法|测试完整代码、分享示例|
|**依赖管理**|有限支持|支持 `Cargo.toml`|
|**调试支持**|简单输出|可查看 ASM/LLVM IR|



