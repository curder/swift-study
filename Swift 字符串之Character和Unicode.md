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

let smile: Character = "������"

let coolGuy: Character = "\u{1F60E}"
```












