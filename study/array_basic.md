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

普通遍历数据方式

```
for number in numbers{
    number
}
// 想当于
for index in 0..<numbers.count{
    numbers[index]
}
```

遍历数组同时获取数组的索引

```
for (index , value) in vowels.enumerated() {
    print("\(index+1) : \(value)")
}
```

### 数组的比较（比较的是值）

```
var oneToFive = [1, 2, 3, 4, 5]
numbers == oneToFive // true

var oneToFive2 = [1, 2, 4, 3, 5]
numbers == oneToFive2 // false

```

## 数组的增删改操作

假如有如下数组变量。
```
var list = ["Apple", "Orange"]
```
### 新增
#### 新增数组元素
下面列举一些新增数组元素的方法。
```
list.append("Pear")

list += ["Banner"] // 使用 += 的方式添加数组元素必须添加的是一个数组，并且数组中的类型要与之前的一直，比如这里的字符串

list = list + ["Watermelon","Grape"]

list // ["Apple", "Orange", "Pear", "Banner", "Watermelon", "Grape"]
```

#### 新增数组单元到指定索引处

在Swift中可以很方便的将元素添加到某个索引值的位置，换言之填写的索引为新增的元素所在的索引位置。
```
list.insert("Cantaloupe", at: 2)
list // ["Apple", "Orange", "Cantaloupe", "Pear", "Banner", "Watermelon", "Grape"]
```

> 注意：小心数组越界的问题。

### 删除元素
#### 删除第一个元素
快速删除数组的第一个元素。
```
list.removeFirst()
list // ["Orange", "Cantaloupe", "Pear", "Banner", "Watermelon", "Grape"]
```

#### 删除最后一个元素
快速删除数组的最后一个元素
```
list.removeLast()
list // ["Orange", "Cantaloupe", "Pear", "Banner", "Watermelon"]
```

#### 根据索引删除数组单元

```
list.remove(at: 1)
list // ["Orange", "Pear", "Banner", "Watermelon"]
```
> 注意：小心数组越界的问题。

#### 根据范围删除数组单元

```
list.removeSubrange(0..<2)
list // ["Banner", "Watermelon"]
```
> 注意：小心数组越界的问题。

#### 删除所有数组单元

```
list.removeAll()
list // []
```

### 修改
#### 修改具体元素

```
list = ["Apple","Orange","Pear","Watermelon"]
list[0] = "Banner"
print(list) // ["Banner", "Orange", "Pear", "Watermelon"]
```

#### 根据区间范围修改元素
先获取元素的值然后进行赋值修改。
```
list[1...2] = ["Cantaloupe","Grape"]
print( list ) // ["Banner", "Cantaloupe", "Grape", "Watermelon"]
```

#### 修改范围

```
list[1...3] = ["Grape"]
print( list ) // ["Banner", "Grape"]
```

> 无论是使用索引还是使用区间修改数组，都可能产生数组越界的问题。



### 其他操作

#### filter

`filter(includeElement: (T) -> Bool) -> [T]`

```
let bigNumbers = [2, 47, 118, 5, 9].filter({ $0 > 20 }) // bigNumbers = [47, 118]
```


#### map

`map(transform: (T) -> U) -> U`

```
let stringified; [String] = [1, 2, 3].map({ String($0) }) // ["1", "2", "3"]
```

#### refuce

`reduce(initial: U, combine: (U, T) -> U) -> U`

```
let sum: Int = [1, 2, 3].reduce(0){ $0 + $1} // add up the numbers in the Array.
let sum = [1, 2, 3].reduce(0, +) // some thing because `+` is a function in Swift.
```







