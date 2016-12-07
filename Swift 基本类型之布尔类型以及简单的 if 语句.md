## Swift 基本类型之布尔类型以及简单的 if 语句

　　在 Swift 语言中，布尔类型有两个 `true` 和 `false` 


### 声明布尔值
```
let myBoolTrue: Bool = true
let myBoolFalse = false
```

### if 流程控制
　　if 关键字后面条件可以不使用 `()` 包裹起来，并且 `{ }` 不允许省略
```
let myBoolTrue: Bool = true

if myBoolTrue {
    print("I am true!") // I am true!
} else if 3 + 4 == 7 {
    print("3 + 4 eq 7!")
} else {
    print("I am false!") // Will never be executed
}
```






























