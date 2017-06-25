## Swift 集合之基本操作
假如有如下集合：
```
var a: Set<String> = ["Swift","Object-C"]
var b: Set<String> = ["HTML","CSS","JS"]
var c: Set<String> = []
```
### 新增
```
a.insert("PHP") // 新增后 a 的值为：["Object-C", "PHP", "Swift"]

b.insert("HTML") // 新增后 b 的值不变，因为集合中元素是唯一的
```

### 删除
```
a.remove("PHP") // 返回值删除的元素的值。删除指定元素后， a 的值为 ["Object-C", "Swift"]

c.remove("JS") // 删除不存在的元素，返回 nil

a.removeAll() // 清空集合中所有元素
```

使用`remove()`组建自己的业务逻辑
```
if let remove = a.remove("Swift") {
    print("Swift is removed")
}
```

> 使用 `remove()` 方法对集合删除操作时，如果删除的元素不存在的话，则返回nil。

### 其他操作
假如有如下集合：
```
var setA: Set<String> = ["Swift","Object-C"]
var setB: Set<String> = ["HTML","CSS","JS"]
var setC = Set(["Swift","HTML","CSS"])
```
#### 并集

Swift 提供了两个并集操作
* union()
* unionInPlace()

它们的区别在于`union()` 并不改变集合的值，而 `unionInPlace` 则会改变集合的值

`setA` 与 `setB` 的并集
```
setA.union(setB) // ["JS", "CSS", "Object-C", "HTML", "Swift"]
```

#### 交集
```
setA.intersection(setC) // Swift
```

#### 减法

```
setA.subtract(setC) // Object-C
```
> 集合 `setA` 拥有的元素， `setC`  不拥有的元素。