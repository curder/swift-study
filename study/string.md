## Swift 字符串

### 字符串的声明
* 字符串常见的声明方式

```
let string = "Hello"
var str: String = "Hello" // 常用这种方式
let hello = String("Hello")
```

* 空字符串声明

```
var emptyString = ""
var emptyStr = String()
```

### 字符串成员变量 isEmpty

```
let str = "String"
str.isEmpty // 返回 false
```

### 字符串插值

```
let name = "curder"
let age = 25
let height = 178

let str = "My name is \(name). I am \(age) years old. I am \(height) meters tall." // My name is curder. I am 25 years old. I am 178 meters tall.
```