## Swift 闭包
Swift 中闭包是引用类型。有些时候定义一个函数可能只需要使用一次，
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
```
arr.sort(by: {a , b in return a > b})

arr.sort(by: {a , b in a > b})

arr.sort(by: { $0 > $1 })

arr.sort(by: >)
```

### 结尾闭包
```
arr.sort(by: ){ a , b in
    return a > b
}

// 或者
arr.sort{ a , b in
    return a > b
}
```

### 内容捕获

```
var arr:[Int] = []

for _ in 0 ..< 100{
    arr.append( Int(arc4random()%1000) )
}
arr
var num = 100

arr.sort{ a , b in
    return abs(a - num ) < abs(b - num)
}
```
> 在闭包内能自动捕获外部变量，但是会有内存泄漏的问题。














