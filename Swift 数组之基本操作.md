# Swift 数组之基本操作
假如有如下数组变量：
```
var numbers = [1,2,3,4,5]
var vowels = ["A","E","I","O","U"]
var emptyArray = [Int]()
```
## 数组查找
### 获取数组元素个数
```
vowels.count
```

### 判断数组是否为空
```
numbers.isEmpty
emptyArray.isEmpty
```
### 获取数组元素
```
vowels[1] // E
```

### 获取数组中第一个元素，返回的是可选型
```
vowels.first // A
```

### 获取数组中最后一个元素，返回可选型
```
vowels.last // U 或者 vowels[ vowels.count - 1 ]
emptyArray.first // nil

if let firstVowel = vowels.first{
    "The first vowel is " + firstVowel
}
```

### 获取最小，最大值
```
numbers.min() // 1
vowels.max() // U
```

### 使用范围获取数组的子数组
```
numbers[2..<4]
numbers[2..<numbers.count]
```

### 判断某个数组是否包含某个值（返回布尔类型）
```
vowels.contains("A") // true
vowels.contains("B") // false
```

### 遍历数组
```
for number in numbers{
    number
}
// 想当于
for index in 0..<numbers.count{
    numbers[index]
}
```

### 遍历数组同时获取数组的索引
```
for (index , value) in vowels.enumerated() {
    print("\(index+1) : \(value)")
}
```

### 数组的比较（比较的是值）

```
var oneToFive = [1,2,3,4,5]
numbers == oneToFive

var oneToFive2 = [1,2,4,3,5]
numbers == oneToFive
```

## 数组的增删改操作
















