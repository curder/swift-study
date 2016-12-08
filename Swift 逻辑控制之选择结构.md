## Swift 逻辑控制之选择结构

### if - else if - else

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


### switch - case - default

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

> **注意：**
> 1. 和其他语言的语法不同的是，`switch`	不强制需要在每次执行完 `case` 中的语句后的写 `break` 。
> 2.  `switch` 语句必须写 `default`

#### switch 的一些其他用法
##### 判断范围
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

##### 判断元组

判断一个点在那个位置，比如 如果横坐标是 0 ，那么我们就认为是在 x 轴坐标上。

```
let point: ( x: Int , y: Int ) = ( 0 , 1 )

switch point {
case ( 0 , 0 ):
    print("It is origin!")
case ( _ , 0 ):
    print("( \(point.x),\(point.y) ) is on the x-axis")
case ( 0 , _ ):
    print("( \(point.x),\(point.y) ) is on the y-axis")
case ( -2...2 , -2...2 ):
    print("( \(point.x),\(point.y) ) is near the origin.")
default:
    print("It is just an ordinary point")
}
```

##### 判断并赋值
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
    print("The point is ( \(x) ,\(y) )")
}
```

