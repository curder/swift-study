## Swift逻辑控制之循环

[TOC]

### for in 循环结构
　　计算 `[ -99 , 99 ]` 相乘，如 `-99 * -99` 或 `-98 * -98` 。
```
for i in -99 ... 99 {
    i*i
}
```
#### 计算 2 的 10 次方
```
var result = 1
var base = 2
var power = 10
for _ in 1...power {
    result *= base
}
result // 1024
```

### for 循环

语法结构：
```
for initialization; condition; increments {
	statements
}
```

> **注意：** 
> 1. `for` 循环的表达式不强制使用 `()`扩起来。
> 2. 必须使用 `{}` 包含循环语句体。
> 3. 在 Swift 3 中这种写法已经被取消了。

### while 循环

```
initialization
while condition {
	statements
    increments
}
```
> **注意：** 
> 1. `while` 循环的表达式不强制使用 `()`扩起来。
> 2. 必须使用 `{}` 包含循环语句体。



### repeat while 循环
　　至少执行一次的循环。
```
initialization
repeat {
	statements
    increments
}while condition
```

### break 与 continue

* break 立即结束当前循环

* continue 结束当前循环体内容，直接下一次循环




















