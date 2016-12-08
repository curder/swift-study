## Swift 字符串之Character和Unicode

### Character
字符串字符

#### 遍历字符串
　　调用字符串 `characters` 成员属性获取字符串的每个字符。
```
var str = "Hello,playground"

for c in str.characters{
    print(c)
}
```

#### 字符 Character
```
let englishChar: Character = "a"

let chineseChar: Character = "中"

let smile: Character = "��"

let coolGuy: Character = "\u{1F60E}" // 一个酷脸的表情
```

### 字符串长度判断
```
let str: String = "abcdefg"
let str2: String = "\u{1F60E}\u{1F60E}\u{1F60E}"
let str3: String = "中华人们共和国"

str.characters.count // 7
str2.characters.count // 3
str3.characters.count // 7

var cafe = "cafe\u{0301}"
cafe.characters.count // 4
```







