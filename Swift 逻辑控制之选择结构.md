## Swift 逻辑控制之选择结构

### `if - else if - else`

语法如下

```
if condition1 {
	statements
} else if conditon2 {
	statements
} else {
	statements
}
```
> **注意：** 
> 1. `if` 判断的条件不强制使用 `()`扩起来。
> 2. 必须使用 `{}` 包含循环语句体。


### `switch - case - default`

语法如下

```
switch <#value#> {

case <#pattern#>:
    <#code#>

case <#pattern2#>:
    <#code2#>

default:
    <#code#>
}
```

几个举例：

```
switch rating {
case "a","A":
    print("Great!")
case "b","B":
    print("Just So so!")
case "c","C":
    print("Its Bad")
default:
    print("Error")
}

// 使用switch判断浮点数
let x = 2.5
switch x{
case 2.5:
    print("I'm 2.5")
default:
    print("I'm not 2.5")
}

// 使用switch判断布尔值
let y = false
switch y{
case true:
    print("I'm true")
case false:
    print("I'm false")
}
```

> **注意：**
> 1. 和其他语言的语法不同的是，`switch`	不强制需要在每次执行完 `case` 中的语句后的写 `break` 。
> 2.  `switch` 语句如果不能完全穷举完数据，那么必须写 `default`。
> 3. 如果运行完一个 `case` 语句后想继续运行下一个 `case` 语句，请添加 `fallthrough` 关键字。

### switch 的一些其他用法

#### 判断范围
```
let score = 9

switch score {
case 1..<60:
    print("You got an egg!")
case 60:
    print("Juse passed")
case 61 ..< 80:
    print("Just so so!")
case 80 ..< 90:
    print("Good!")
case 90 ..< 100:
    print("Great!")
case 100:
    print("Perfect!")
default:
    print("Error.")
}
```

#### 判断元组

判断一个点在那个位置，比如 如果横坐标是 0 ，那么我们就认为是在 x 轴坐标上。

```
let point: ( x: Int , y: Int ) = ( 0 , 1 )

switch point {
case ( 0 , 0 ):
    print("It is origin!")
case ( _ , 0 ): // 忽略元祖数据
    print("( \(point.x),\(point.y) ) is on the x-axis")
case ( 0 , _ ):
    print("( \(point.x),\(point.y) ) is on the y-axis")
case ( -2...2 , -2...2 ): // 对于元祖元素使用区间运算符匹配
    print("( \(point.x),\(point.y) ) is near the origin.")
default:
    print("It is just an ordinary point")
}
```

#### 判断并赋值
解包元组并赋值给常量。
```
let point: ( x: Int , y: Int ) = ( 1 , 0 )

switch point {
case ( 0 , 0 ) :
    print("It is origin!")
case ( let x ,0 ) :
    print("It is on the x-axis.")
    print("The x value is \(x)")
case ( 0 , let y ):
    print("It is on the y-axis.")
    print("The y value is \(y)")
case ( let x , let y ):
    print("It is just an ordinary point.")
    print("The point is (\(x),\(y))")
}
```

#### `fallthrough` 关键字

```
let point: ( x: Int , y: Int ) = ( 0 , 0)

switch point {
case ( 0 , 0 ):
    print("It is origin!")
    fallthrough
case ( _ , 0 ): 
    print("( \(point.x),\(point.y) ) is on the x-axis")
    fallthrough
case ( 0 , _ ):
    print("( \(point.x),\(point.y) ) is on the y-axis")
default:
    print("It is just an ordinary point")
}
```
上面的程序执行将打印出如下结果：
```
It is origin!
( 0,0 ) is on the x-axis
( 0,0 ) is on the y-axis
```

> Swift中的`switch case`和其他语言中的不同，它不是必须强制的使用`break`中断上一次判断，如果需要在判断语句中使用类似c、c++、java类似的 `switch case` 判断的效果，可以通过`fallthrough`关键字实现。使用这个关键字后，将在执行完当前分支成功后跳到下一个分支，而不是跳出判断分支。



#### 控制转移

查找 `x^4 - y^2 = 15 * x * y` 在300以内的正整数解。

我们可以很方便的使用`for in` 写出程序代码，如下：
```
var getAnswer = false
for m in 1...300 {
    for n in 1...300 {
        if m*m*m*m - n*n == 15*m*n {
            print(m, n)
            getAnswer = true
            break
        }
    }
    if getAnswer {
        break
    }
}
```
> 上面的代码能很快的找出符合结果的答案，但是有太多的冗余代码。

在Swift中，我们可以给循环取一个别名，在使用`break`、`continue`等关键词时停止这个循环
```
findAnswer: for m in 1...300 {
    for n in 1...300 {
        if m*m*m*m - n*n == 15*m*n {
            print(m, n)
            
            break findAnswer
        }
    }
}
```
> 上面的循环将在找到一个符合的值之后跳出最外层的循环


### case 的一些用法

#### where 与匹配模式
语法如下
```
switch some value to consider {
case value1:
    respond to value1
case value2 where condition:
    respond to value2
case value3:
    respond to value3
default:
    otherwise,do something else
}
```

##### 具体`switch`的例子如下：
```
let point: ( x: Int , y: Int ) = ( 1 , 1 )

switch point {
case let ( x , y ) where x == y :
    print("It is on the line x == y!")
    print("The point is (\(x),\(y))")

case let ( x , y ) where x == -y :
    print("It is on the line x == -y!")
    print("The point is (\(x),\(y))")

case let ( x , y ):
    print("It is just an ordinary point.")
    print("The point is (\(x),\(y))")
}
```

> 在`case`后面使用匹配模式限定条件后再使用where进行限定。


##### `if case`

使用`if`语句简化如下代码：
```
switch age {
case 10...19:
    print("You're a teenager")
default:
    print("You're not a teenager")
}

// 使用if case简化写法
if case 10...19 = age {
    print("You're a teenager")
}

// 使用if case简化写法，再加上where进行限定
if case 10...19 = age , age >= 18 {
    print("You're a teenager abd in a college.")
}

// 再如
let vector = (4, 0)
if case (let x , 0) = vector , x > 2 && x < 5 {
    print("It's the vector!")
}

```

> 注意使用 `,` 分割where限定条件

##### `for case`

// 求1 ... 100 以内被3整除的数
```
for i in 1...100 {
    if i%3 == 0{
        print(i)
    }
}

// 使用 for case 简写
for case let i in 1...100 where i%3 == 0{
    print(i)
}
```

