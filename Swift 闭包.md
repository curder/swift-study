## Swift 闭包
有些时候定义一个函数可能只需要使用一次，
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
























