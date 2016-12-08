## Swift 字符串之 String.index 和 range

```
var str = "hello, swift"

let startIndex = str.startIndex // 指向字符串最开始的索引

let endIndex = str.endIndex // 指向字符串结束的索引

str[startIndex] // 截取字符串第 0 位的字符

str[str.index(startIndex, offsetBy: 5)] // 截取字符串第 5 位的字符 为：","

// 获取空格
let spaceIndex = str.index(startIndex, offsetBy: 6)
str[spaceIndex]

// 如果想寻找一个String.Index的前驱和后继，需要使用String.index(before:)和String.index(after:)方法
str[str.index(before: spaceIndex)]
str[str.index(after: spaceIndex)]

// 获取最后的字符
str[str.index(before: endIndex)]

// 获取字符范围
str[startIndex ..< spaceIndex] // 从开始截取到空白字符

let range = startIndex ..< str.index(before: spaceIndex)

// 字符串替换（改变原字符串）
str.replaceSubrange(range, with: "Hi")

// 字符串追加（改变原字符串）
str.append("!!!")

// 字符串插入（改变原字符串）
str.insert("?", at: str.endIndex)

// 字符串删除（不改变原字符串）
str.remove(at: str.index(before: endIndex))

// 反向截取（改变原字符串）
str.removeSubrange(str.index(endIndex, offsetBy: -2)..<str.endIndex)
```