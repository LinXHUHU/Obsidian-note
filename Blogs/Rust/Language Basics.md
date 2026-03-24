

# Pattern Matching and Destructuring
In Rust, "pattern matching" is a robust tool that allows you to destructure data types and perform conditional checks in a succinct and clear way. The main structures used for pattern matching are `match` and `if let`. The `match` keyword can be used to compare a value against a series of patterns and then execute code based on which pattern matches. Patterns can be made up of literal values, variable names, wildcards, and many other things. The `if let` structure allows you to combine `if` and `let` into a less verbose way of handling values that match one specific pattern, rather than a series of patterns. It's basically a nice syntax sugar over a `match` statement.

##### **(1) `match` 表达式**

```
let x = 3;
match x {
    1 => println!("One"),
    2 | 3 => println!("Two or Three"), // 匹配多个值
    _ => println!("Other"),           // 通配符（类似 default）
}
```

##### **(2) `if let` 表达式**
```
// 使用 match（需要处理所有情况）
let y = Some(5);
match y {
    Some(val) => println!("Got {}", val),
    None => (), // 必须明确处理 None
}

// 使用 if let（更简洁）
if let Some(val) = y {
    println!("Got {}", val); // 仅处理 Some 情况
}

```

- 文中提到 `if let` 是 `match` 的语法糖，但未说明其局限性：
    
    - **仅支持单一模式**，无法像 `match` 一样并列多个条件。
        
    - 如果需同时处理多个模式，仍需用 `match`。



# Functions and Method Syntax
https://kaisery.github.io/trpl-zh-cn/ch03-03-how-functions-work.html

Note that we defined `another_function` _after_ the `main` function in the source code; we could have defined it before as well. Rust doesn’t care where you define your functions, only that they’re defined somewhere in a scope that can be seen by the caller.