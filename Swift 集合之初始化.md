## Swift 集合之初始化
　　像数组一样，将一些元素放在一起，但是是**无序的数据集**，并且集合中**不允许有相同的值**。相关操作如下：
```
var set: Set<String> = ["Swift","C++"]
```

### 空集合
```
var emptySet1: Set<Int> = []
var emptySet2 = Set<Double>()
```

### 获取集合中元素的个数
```
set.count
```
### 判断集合是否为空 返回Bool
```
set.isEmpty
```
### 随机取出一个元素 返回 Optional
```
print( set.first)
```
### 判断一个元素是否存在某个集合中
```
set.contains("C++")
```

### 集合的比较
```
let setA: Set<Int> = [1,2,3]
let setB: Set<Int> = [1,3,2]

setA == setB // 返回 true
```

### 集合是值类型

```
var set1 = [4,23,32]
var set2 = set1

set2.remove(at: 2)
set1 //[4, 23, 32]
set2 //[4, 23]
```