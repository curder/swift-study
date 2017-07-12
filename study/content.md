## Swift 容器类 Collections

所谓的容器类，就是程序中的数据结构，来承载我们app中的数据。

### 数组 Array
* 有序的数据序列

例如：`var numbers = [1, 2, 3, 4, 5]` 或者 `var vowels = ["A", "B", "C", "D", "E"]`

### 字典 Dictionary

* 键 -> 值数据对

例如：`var dir1 = ["key1":"val", "key2":"val2"]`

### 集合 Set

* 无序
* 唯一性
* 快速查找
* 提供集合操作

例如：`var set1 = [1, 2, 3]`



### for-in 遍历

#### 对Range使用for-in
```
for number in 1..<10{
    number
}
```

#### 对String.charcaters使用for-in
```
for c in "Hello".characters {
    c
}
```

#### 对Array使用for-in
```
var vowels = ["a", "b", "c", "d"]
for vowel in vowels {
    vowel
}

for (key, vowel) in vowels.enumerated() {
    key
    vowel
}
```

#### 对Dictionary使用for-in
```
var dict: Dictionary<Int,String> = [1:"a",2:"b",3:"d"]

// 遍历字典键
for key in dict.keys {
    key
}
// 遍历字典值
for value in dict.values {
    value
}
// 遍历字典键值
for (key, value) in dict {
    key
    value
}
```

#### 对Set使用for-in
```
var set = Set(["a", "b", "c", "d"])

for vowel in set {
    vowel
}
```