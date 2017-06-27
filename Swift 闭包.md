## Swift 闭包

**Swift 中闭包是引用类型** 有些时候定义一个函数可能只需要使用一次，
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
> 在闭包的定义中，因为不会被外部调用，所以给闭包取外部的参数名没有意义。

闭包的简化写法：
```
arr.sort(by: {(a:Int , b:Int)-> Bool in return a > b}) // 如果闭包的函数体只有一行的情况，我们可以将其写在一行里。

arr.sort(by: {a , b in return a > b}) // Swift type inference.

arr.sort(by: {a , b in a > b})

arr.sort(by: { $0 > $1 })

arr.sort(by: >) // ">" 符号本身就是函数.
```

### 结尾闭包

Trailing Closure

如果需要传递的闭包在函数参数的末尾，我们可以使用结尾闭包的方式书写，如下：
```
arr.sort(by: ){ a , b in
    return a > b
}

// 如果将闭包放到()外部，而原函数调用没有任何参数需要传递，那么这里我们可以将小括号去掉。
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














