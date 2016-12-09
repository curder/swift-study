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
```
var list = ["Apple","Orange"]
```
### 新增数组元素
```
list.append("Pear")
list += ["Banner"]
list = list + ["Watermelon","Grape"]
list // ["Apple", "Orange", "Pear", "Banner", "Watermelon", "Grape"]
```
### 新增数组单元到指定索引处
```
list.insert("Cantaloupe", at: 2)
list // ["Apple", "Orange", "Cantaloupe", "Pear", "Banner", "Watermelon", "Grape"]
```
### 删除第一个元素
```
list.removeFirst()
list // ["Orange", "Cantaloupe", "Pear", "Banner", "Watermelon", "Grape"]
```
### 删除最后一个元素
```
list.removeLast()
list // ["Orange", "Cantaloupe", "Pear", "Banner", "Watermelon"]
```
### 根据索引删除数组单元
```
list.remove(at: 1)
list // ["Orange", "Pear", "Banner", "Watermelon"]
```
### 根据范围删除数组单元
```
list.removeSubrange(0..<2)
list // ["Banner", "Watermelon"]
```
### 删除所有数组单元
```
list.removeAll()
list // []
```
### 修改具体元素
```
list = ["Apple","Orange","Pear","Watermelon"]
list[0] = "Banner"
print(list) // ["Banner", "Orange", "Pear", "Watermelon"]
```
### 根据区间范围修改元素
```
list[1...2] = ["Cantaloupe","Grape"]
print( list ) // ["Banner", "Cantaloupe", "Grape", "Watermelon"]
```
### 修改范围
```
list[1...3] = ["Grape"]
print( list ) // ["Banner", "Grape"]
```
> 无论是使用索引还是使用区间修改数组，都可能产生数组越界的问题


















