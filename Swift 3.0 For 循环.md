# Swift 3 For 循环
　　众所周知，Swift 3 抛弃了 C 语言风格的 for 循环，for 循环能实现大多数的循环逻辑，那现在我们应该怎么书写我们的循环流程呢？

## Swift 3 循环
循环答应 1 2 3 ... 100，写法如下：
```
for i in 0...100{ // 前闭后闭区间

}
```

## 遍历数组
### 遍历获取数组值
```
let arr = [1,2,3,4,5]
for i in arr {
    i
}

for i in 0 ..< arr.count{
    arr[i]
}
```

遍历数组获取索引和值
```
for i in arr.enumerated() {
    i.offset // 数组单元索引
    i.element // 数组单元值
}
```

### 逆序遍历数组获取索引和值
```
for ( index , value ) in arr.enumerated().reversed(){
    index
    value
}
```

### 循环时添加条件

> 取出索引是 2 的倍数的元素。

#### 使用闭包获取偶数
```
for ( index , value ) in arr.enumerated().filter({ ( index, value )  in index % 2 == 0}){
    index
    value
}
```

#### 使用 where 关键字
```
for ( index , value ) in arr.enumerated() where index % 2 == 0 {
    index
    value
}
```
























