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
var setD: Set<String> = ["Swift"]
```
#### 集合的并集操作

Swift提供两种操作
* `union()`
* `formUnion()`
它们的区别是，`union()`的操作不影响原集合，而`formUnion()`则会已影响原集合。

求`setA` 与 `setB` 的并集

```
setA.union(setB) // ["JS", "CSS", "Object-C", "HTML", "Swift"]


setA.formUnion(setB) // ["JS", "CSS", "Object-C", "HTML", "Swift"] ，此时 setA的值也等于这个返回值
```

#### 集合的交集操作

Swift提供两种操作
* `intersection()`
* `formIntersection()`
它们的区别是，`Intersection()`的操作不影响原集合，而`formIntersection()`则会已影响原集合。

```
setA.intersection(setC) // Swift

setA.formIntersection(setC) // Swift
```

#### 集合的差集操作

```
setA.subtract(setC) // Object-C 表示setA独有的而setC不具备的元素
setC.subtract(setA) // "Swift","HTML","CSS" 表示setC独有而setA不具备的元素
```
> 集合 `setA` 拥有的元素， `setC`  不拥有的元素。


#### 集合的抑或操作
Swift提供两种操作
* `symmetricDifference()`
* `formSymmetricDifference()`
它们的区别是，`symmetricDifference()`的操作不影响原集合，而`formSymmetricDifference()`则会已影响原集合。

```
setA.symmetricDifference(setC) // "Object-C","HTML","CSS"
setA.formSymmetricDifference(setC) // "Object-C","HTML","CSS"
```


#### 集合的子集、真子集判断

```
setD.isSubset(of: setA)
setD.isStrictSubset(of: setA)

```


#### 集合的超集、超子集判断
子集、真子集的反方向判断
```
setA.isSuperset(of: setD)
setA.isStrictSuperset(of: setD)
```


#### 集合的相离判断

两个集合毫无相同的元素

```

```