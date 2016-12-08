## Swift 逻辑控制之选择结构

### if - else if - else
语法如下
```
if condition1 {
	statements
} else if conditon2 {
	statements
} else {
	statements
}
```
> **注意：** 
> 1. `if` 判断的条件不强制使用 `()`扩起来。
> 2. 必须使用 `{}` 包含循环语句体。


### switch - case - default
语法如下
```
switch <#value#> {

case <#pattern#>:
    <#code#>

case <#pattern2#>:
    <#code2#>

default:
    <#code#>
}
```

>**注意：**
和其他语言的语法不同的是，`switch`	不强制需要在每次执行完 `case` 中的语句后的写 `break` 。








