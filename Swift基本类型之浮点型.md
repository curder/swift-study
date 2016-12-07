## Swift基本类型之浮点型

 　　浮点数在 Swift 中有两种表达方式 `Float` 、 `Double` 。其中 Float 使用 32 位进行数据存储而 `Double` 则是使用 64 位进行数据的存储。

　　在计算机上使用不同的表现方式中的差异就是浮点数精度上的差异。
 
```
let myFloat: Float = 3.1415926 // 得到的结果是 3.1415925
let myDouble: Double = 3.1415926 // 得到的结果是 3.1415926000000001
let x = 3.1415926 // 默认使用 Double 进行存储
```
###  使用科学计数法来表示一个数
```
var a = 1.25e10 // 1.25乘以10的10次方 = 12500000000.0
```

###  截断浮点数的位置 使程序更加可读
```
var b = 1.00_0000_0001 // 1.0000000001
```

### 在浮点型运算中 Swift 不允许隐式的类型转换
```
let a: Double = 2.1
let b: Float = 1.1

a + b // binary operator '+' cannot be applied to operands of type 'Double' and 'Float'

let x = a + Double(b) // 3.20000002384186

let y = Float(a) + b // 3.2
```
```
let w: Float = 3
let v: Int = 3.1 // cannot convert value of type 'Double' to specified type 'Int'

let v: Int = Int(3.1) // 3
```

### 整型与浮点数的运算
```
let integer = 3
let fraction = 0.1415926

print(Double(integer) + fraction) // 3.1415926
```
