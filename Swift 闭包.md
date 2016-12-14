## Swift 闭包

闭包本质上是函数

### 闭包写法
一般写法如下：
```
var arr:[Int] = []

for i in 0 ..< 100{
    arr.append( Int(arc4random()%1000) )
}

arr.sort(by: {(a:Int,b:Int) -> Bool in
    return a > b
})
```

闭包的简化写法：
























