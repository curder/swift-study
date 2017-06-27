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

使用结尾闭包的一个例子。
```
var arr:[Int] = []

for i in 0 ..< 100{
    arr.append( Int(arc4random()%1000) )
}

var r = arr.map(){(number)-> String in
    var number = number
    var res = ""
    repeat {
        res = String(number%2) + res
        number /= 2
    }while number != 0
    
    return res
}
```


### 内容捕获

一下是demo，随机取100个数字，以100为中心，将离100最近的数字越靠前
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



### 闭包和函数都有引用类型

```
// 计算跑步的里程数，单位m
func runningMetersWithMetersPerDay(metersPerDay: Int) -> () -> Int {
    
    var totalMeters = 0 // 跑步的总数
    return {
        totalMeters += metersPerDay // 两个变量都是通过闭包外部的内容捕获获得值的。
        return totalMeters
    } // 返回闭包
}

var planA = runningMetersWithMetersPerDay(metersPerDay: 5000)
planA() // 5000
planA() // 10000

var planB = runningMetersWithMetersPerDay(metersPerDay: 1000)
planB() // 1000
planB() // 2000


var anotherPlan = planA // 将闭包赋值给另一个变量

anotherPlan() // 15000 在调用的过程中它们的值会累加，说明是引用类型
planA() // 20000 在调用的过程中它们的值会累加，说明是引用类型


let planC = runningMetersWithMetersPerDay(metersPerDay: 2000) // 对于引用类型，不代表里面的值不能被修改
planC() // 2000
planC() // 4000

//planC = runningMetersWithMetersPerDay(metersPerDay: 3000) // 这句赋值会报错
```








